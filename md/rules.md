## AnnouncementRules

```csharp
public class AnnouncementRules : IBusinessRule
    {
        #region Fields

        private readonly IModelReadRepository<Announcement, AnnouncementTranslation> _readRepository;

        public AnnouncementRules(IModelReadRepository<Announcement, AnnouncementTranslation> readRepository)
        {
            _readRepository = readRepository;
        }

        #endregion Fields

        #region Methods

        public async Task<IResult> IsExistAsync(Guid id)
        {
            if (!await _readRepository.IsExistAsync(p => p.Id == id))
            {
                return new ErrorResult(AnnouncementConstants.ANNOUNCEMENT_IS_NOT_EXIST);
            }

            return new SuccessResult();
        }

        public IResult DateRangeControl(DateTime start, DateTime end)
        {
            if (end < start)
            {
                return new ErrorResult(AnnouncementConstants.ANNOUNCEMENT_DATE_RANGE);
            }

            return new SuccessResult();
        }

        #endregion Methods
    }
```