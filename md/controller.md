## Controller

* [CreateAnnouncementCommandRequest](./create-command-request.md)

* [GetAllAnnouncementQueryWithTranslationCodeRequest](./get-command-request.md)

```csharp
    public class AnnouncementController :  CustomBaseController
    {
        #region Methods

        [Authorize(Roles = "Administrator,Announcement.Create")]
        [HttpPost("Create")]
        public async Task<IActionResult> Create(CreateAnnouncementCommandRequest request)
        {
            return Ok(await Mediator.Send(request));
        }

        [HttpPost("UploadAnnouncementImage")]
        [Authorize(Roles = "Administrator,Announcement.Update,Announcement.Create")]
        public async Task<IActionResult> UploadAnnouncementImage(List<IFormFile> images, [FromQuery] Guid id)
        {
            return Ok(await Mediator.Send(new UploadAnnouncementImageCommandRequest { Id = id, Images = images }));
        }

        [HttpPost("UploadAnnouncementFiles")]
        [Authorize(Roles = "Administrator,Announcement.Update,Announcement.Create")]
        public async Task<IActionResult> UploadAnnouncementFile(List<IFormFile> files, [FromQuery] Guid id)
        {
            return Ok(await Mediator.Send(new UploadAnnouncementFileCommandRequest { Id = id, Files = files }));
        }

        [HttpPost("UploadAnnouncementWebsiteLinks")]
        [Authorize(Roles = "Administrator,Announcement.Update,Announcement.Create")]
        public async Task<IActionResult> UploadAnnouncementWebsite(List<string> websiteLinks, [FromQuery] Guid id)
        {
            return Ok(await Mediator.Send(new UploadAnnouncementWebsiteCommandRequest { Id = id, WebsiteLinks = websiteLinks }));
        }

        [HttpGet("GetAllAnnouncementWithTranslationCode")]
        [Authorize(Roles = "Administrator,Announcement.Get")]
        public async Task<IActionResult> GetAllAnnouncementWithTranslationCode(TranslationCode translationCode)
        {
            return Ok(await Mediator.Send(new GetAllAnnouncementQueryWithTranslationCodeRequest(translationCode)));
        }

        [HttpGet("GetByIdWithTranslationCode")]
        [Authorize(Roles = "Administrator,Announcement.Get")]
        public async Task<IActionResult> GetByIdWithTranslationCode(Guid id, TranslationCode translationCode)
        {
            var result = await Mediator.Send(new GetByIdAnnouncementWithTranslationCodeQueryRequest(id, translationCode));
            return Ok(result);
        }

        [HttpGet("GetById")]
        [Authorize(Roles = "Administrator,Announcement.Get")]
        public async Task<IActionResult> GetById(Guid id)
        {
            var result = await Mediator.Send(new GetByIdAnnouncementQueryRequest(id));
            return Ok(result);
        }

        [HttpGet("GetByIdImages")]
        [Authorize(Roles = "Administrator,Announcement.Get")]
        public async Task<IActionResult> GetByIdImages(Guid id)
        {
            var result = await Mediator.Send(new GetByIdAnnouncementImageQueryRequest(id));
            return Ok(result);
        }

        [HttpGet("GetByIdFiles")]
        [Authorize(Roles = "Administrator,Announcement.Get")]
        public async Task<IActionResult> GetByIdFiles(Guid id)
        {
            var result = await Mediator.Send(new GetByIdAnnouncementFileQueryRequest(id));
            return Ok(result);
        }

        [HttpGet("GetByIdWebsiteLinks")]
        [Authorize(Roles = "Administrator,Announcement.Get")]
        public async Task<IActionResult> GetByIdWebsiteLinks(Guid id)
        {
            var result = await Mediator.Send(new GetByIdAnnouncementWebsiteLinkQueryRequest(id));
            return Ok(result);
        }

        [HttpPut("Update")]
        [Authorize(Roles = "Administrator,Announcement.Update")]
        public async Task<IActionResult> Update(UpdateAnnouncementCommandRequest request)
        {
            return Ok(await Mediator.Send(request));
        }

        [HttpPut("Active")]
        [Authorize(Roles = "Administrator,Announcement.Update")]
        public async Task<IActionResult> Active(ActiveAnnouncementCommandRequest request)
        {
            var result = await Mediator.Send(request);
            return Ok(result);
        }

        [HttpDelete("Delete")]
        [Authorize(Roles = "Administrator,Announcement.Delete")]
        public async Task<IActionResult> Delete([FromQuery] Guid id)
        {
            return Ok(await Mediator.Send(new DeleteAnnouncementCommandRequest(id)));
        }

        #endregion Methods
    }
```