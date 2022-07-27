## Create Announcement Command Request

* [CreateAnnouncementResultDto](./create-result-dto.md)

* [IModelWriteRepository](./i-model-write-repository.md)

* [AnnouncementRules](./rules.md)

* [IBusinessRuleFactory](./i-business-rule-factory.md)

* [AnnouncementProfile](./profile.md)

* [AnnouncementConstants](./constants.md)

* [CreateAnnouncementCommandValidator](./validator.md)

```csharp
 public class CreateAnnouncementCommandRequest : IRequest<IDataResult<CreateAnnouncementResultDto>>
    {
        #region Properties

        public string Email { get; set; }
        public string Phone { get; set; }
        public string Fax { get; set; }
        public DateTime StartDate { get; set; }
        public DateTime EndDate { get; set; }
        public IEnumerable<AnnouncementTranslationDto> AnnouncementTranslations { get; set; }

        #endregion Properties
    }

    public class CreateAnnouncementCommandHandler : IRequestHandler<CreateAnnouncementCommandRequest, IDataResult<CreateAnnouncementResultDto>>
    {
        #region Fields

        private readonly IMapper _mapper;
        private readonly IModelWriteRepository<Announcement, AnnouncementTranslation> _announcementWriteRepository;
        private readonly IWriteRepository<AnnouncementTranslation> _translationWriteRepository;
        private readonly IUnitOfWork _unitOfWork;
        private readonly TranslationRules _translationRules;
        private readonly AnnouncementRules _announcementRules;
        private readonly IHttpContextAccessor _httpContextAccessor;
        private readonly UserManager<AppUser> _userManager;

        #endregion Fields

        #region Constructors

        public CreateAnnouncementCommandHandler(IBusinessRuleFactory businessRuleFactory,
            IModelWriteRepository<Announcement, AnnouncementTranslation> announcementWriteRepository, IMapper mapper,
            IUnitOfWork unitOfWork, IWriteRepository<AnnouncementTranslation> translationWriteRepository, IHttpContextAccessor httpContextAccessor, UserManager<AppUser> userManager)
        {
            _announcementWriteRepository = announcementWriteRepository;
            _mapper = mapper;
            _unitOfWork = unitOfWork;
            _translationWriteRepository = translationWriteRepository;
            _translationRules = businessRuleFactory.GetBusinessRule(typeof(TranslationRules)) as TranslationRules;
            _announcementRules = businessRuleFactory.GetBusinessRule(typeof(AnnouncementRules)) as AnnouncementRules;
            _httpContextAccessor = httpContextAccessor;
            _userManager = userManager;
        }

        #endregion Constructors

        #region Methods

        public async Task<IDataResult<CreateAnnouncementResultDto>> Handle(CreateAnnouncementCommandRequest request, CancellationToken cancellationToken)
        {
            var businessResult = BusinessRules.Run(_announcementRules.DateRangeControl(request.StartDate, request.EndDate),
                _translationRules.IsExist(request.AnnouncementTranslations),
                _translationRules.IsCheckTranslationCode(request.AnnouncementTranslations),
                            _translationRules.IsNotEmpty(request.AnnouncementTranslations),
                            _translationRules.IsRequiredLangTheList(request.AnnouncementTranslations, new[] { TranslationCode.tr_TR }),
                            _translationRules.IsThereDublicateTranslationCode(request.AnnouncementTranslations));

            if (businessResult != null)
            {
                return new ErrorDataResult<CreateAnnouncementResultDto>(businessResult.Message);
            }
            Announcement announcement = _mapper.Map<Announcement>(request);
            var announcementTranslation = _mapper.Map<List<AnnouncementTranslation>>(request.AnnouncementTranslations);
            _announcementWriteRepository.Add(announcement);
            announcement.StartDate = announcement.StartDate.Date;
            announcement.EndDate = announcement.EndDate.Date;
            
            var userId = _httpContextAccessor.HttpContext.User.Claims.FirstOrDefault(p => p.Type == ClaimTypes.NameIdentifier).Value;
            var user = await _userManager.FindByIdAsync(userId);
            announcement.Contact = user.FullName;


            announcement.Translations.AddRange(announcementTranslation);
            
            await _translationWriteRepository.AddRangeAsync(announcementTranslation);
            await _unitOfWork.SaveAsync();
            return new SuccessDataResult<CreateAnnouncementResultDto>(_mapper.Map<CreateAnnouncementResultDto>(announcement), AnnouncementConstants.ANNOUNCEMENT_CREATE_SUCCESS);
        }

        #endregion Methods
    }
```