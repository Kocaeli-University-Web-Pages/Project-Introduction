## AnnouncementConstants

```csharp
    public static class AnnouncementConstants
    {
        #region Fields

        public static readonly string ANNOUNCEMENT_IS_NOT_EXIST = "Duyuru mevcut değil.";
        public static readonly string ANNOUNCEMENT_CREATE_SUCCESS = "Duyuru başarıyla oluşturuldu.";
        public static readonly string ANNOUNCEMENT_DELETE_SUCCESS = "Duyuru başarıyla silindi.";
        public static readonly string ANNOUNCEMENT_UPDATE_SUCCESS = "Duyuru başarıyla güncellendi.";
        public static readonly string ANNOUNCEMENT_UPLOAD_FILE_SUCCESS = "Duyuru dosya(ları) başarıyla yüklendi.";
        public static readonly string ANNOUNCEMENT_UPLOAD_IMAGE_SUCCESS = "Duyuru resim(leri) başarıyla yüklendi.";
        public static readonly string ANNOUNCEMENT_UPLOAD_WEB_SITES_SUCCESS = "Duyuru web site(leri) başarıyla yüklendi.";
        public static readonly string ANNOUNCEMENT_DATE_RANGE = "Bitiş tarihi başlangıç tarihinden küçük olamaz.";

        public static string ANNOUNCEMENT_ISACTIVE_SUCCESS(bool status) => status ? ANNOUNCEMENT_ISACTIVE_TRUE_SUCCESS : ANNOUNCEMENT_ISACTIVE_FALSE_SUCCESS;
        public static readonly string ANNOUNCEMENT_ISACTIVE_TRUE_SUCCESS = "Duyuru aktif edildi.";
        public static readonly string ANNOUNCEMENT_ISACTIVE_FALSE_SUCCESS = "Duyuru pasif edildi.";

        #endregion Fields
    }
```
