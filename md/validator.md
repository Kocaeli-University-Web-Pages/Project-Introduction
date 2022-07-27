## CreateAnnouncementCommandValidator

```csharp
    public class CreateAnnouncementCommandValidator : AbstractValidator<CreateAnnouncementCommandRequest>
    {
        #region Constructors

        public CreateAnnouncementCommandValidator()
        {
            RuleFor(x => x.StartDate).NotNull().WithMessage("Başlangıç tarihi boş olamaz.");
            RuleFor(x => x.EndDate).NotNull().WithMessage("Bitiş tarihi boş olamaz.");
            RuleForEach(x => x.AnnouncementTranslations).SetValidator(new CreateAnnouncementTransactionValidator());
        }

        #endregion Constructors
    }

    public class CreateAnnouncementTransactionValidator : AbstractValidator<AnnouncementTranslationDto>
    {
        #region Constructors

        public CreateAnnouncementTransactionValidator()
        {
            RuleFor(x => x.Content).NotEmpty().WithMessage("İçerik boş olamaz.");
            RuleFor(x => x.Title).NotNull().WithMessage("Başlık boş olamaz.");
            RuleFor(x => x.TranslationCode).NotNull().WithMessage("Dil kodu boş olamaz.");
        }

        #endregion Constructors
    }
```