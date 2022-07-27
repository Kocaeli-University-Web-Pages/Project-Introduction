## GetAllAnnouncementQueryWithTranslationCodeRequest

* [GetAnnouncementDto](./get-announcement-dto.md)

* [IReadAnnouncementRepository](./i-read-announcement-repository.md)

```csharp
public class GetAllAnnouncementQueryWithTranslationCodeRequest : IRequest<IDataResult<List<GetAnnouncementDto>>>
    {
        #region Constructors

        public GetAllAnnouncementQueryWithTranslationCodeRequest(TranslationCode translationCode)
        {
            TranslationCode = translationCode;
        }

        #endregion Constructors

        #region Properties

        public TranslationCode TranslationCode { get; set; }

        #endregion Properties
    }

    public class GetAllAnnouncementQueryWithTranslationCodeHandler
        : IRequestHandler<GetAllAnnouncementQueryWithTranslationCodeRequest,
        IDataResult<List<GetAnnouncementDto>>>
    {
        #region Fields

        private readonly IReadAnnouncementRepository _readRepository;
        private readonly IMapper _mapper;

        #endregion Fields

        #region Constructors

        public GetAllAnnouncementQueryWithTranslationCodeHandler(IReadAnnouncementRepository readRepository, IMapper mapper)
        {
            _readRepository = readRepository;
            _mapper = mapper;
        }

        #endregion Constructors

        #region Methods

        public async Task<IDataResult<List<GetAnnouncementDto>>> Handle(GetAllAnnouncementQueryWithTranslationCodeRequest request,
            CancellationToken cancellationToken)
        {
            var datas = await _readRepository.GetAllWithTranslationCodeAsync(
                                request.TranslationCode,
                                tracking: false);

            var dto = _mapper.Map<List<GetAnnouncementDto>>(datas);

            return new SuccessDataResult<List<GetAnnouncementDto>>(dto);
        }

        #endregion Methods
    }
```
