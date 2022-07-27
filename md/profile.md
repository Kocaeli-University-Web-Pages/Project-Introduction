## AnnouncementProfile

```csharp
 public class AnnouncementProfile : Profile
    {
        #region Constructors

        public AnnouncementProfile()
        {
            CreateMap<AnnouncementTranslationDto, AnnouncementTranslation>().ReverseMap();
            CreateMap<CreateAnnouncementCommandRequest, Announcement>().ReverseMap();
            CreateMap<UpdateAnnouncementCommandRequest, Announcement>().ReverseMap();
            CreateMap<Announcement, GetByIdAnnouncementDto>()
                .ForMember(p => p.AnnouncementTranslations, member => member.MapFrom(p => p.Translations))
                .ReverseMap();
            CreateMap<CreateAnnouncementResultDto, Announcement>().ReverseMap();

            CreateMap<ModelMergeDto<Announcement, AnnouncementTranslation>, GetAnnouncementDto>()
                .ForMember(p => p.Id, member => member.MapFrom(p => p.Table.Id))
                .IncludeMembers(s => s.Table, s => s.TableTranslation).ReverseMap();
            CreateMap<AnnouncementTranslation, GetAnnouncementDto>().ReverseMap();
            CreateMap<Announcement, GetAnnouncementDto>().ReverseMap();
        }

        #endregion Constructors
    }
```