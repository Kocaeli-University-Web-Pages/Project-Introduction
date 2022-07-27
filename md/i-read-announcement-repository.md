## IReadAnnouncementRepository

```csharp
    public interface IReadAnnouncementRepository : IModelReadRepository<Announcement, AnnouncementTranslation>
    {
        #region Methods

        Task<List<GetAllAnnouncementViewModel>> GetAllAnnouncementWithTranslationCodeAsync(
                                                    RelationTypes relationTypes,
                                                    TranslationCode translationCode = TranslationCode.tr_TR,
                                                    bool tracking = true);

        Task<GetByIdAnnouncementViewModel> GetByIdAnnouncementWithTranslationCodeAsync(
                                                    Guid id,
                                                    RelationTypes relationTypes,
                                                    TranslationCode translationCode = TranslationCode.tr_TR,
                                                    bool tracking = true);

        Task<List<Features.Dashboard.Announcements.ViewModels.GetAllAnnouncementViewModel>> GetAllDashboardAnnouncementWithTranslationCodeAsync(
                                                    RelationTypes relationTypes,
                                                    TranslationCode translationCode = TranslationCode.tr_TR,
                                                    bool tracking = true);

        #endregion Methods
    }
```