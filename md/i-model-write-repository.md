## IModelWriteRepository

```csharp
    public interface IModelWriteRepository<TModelEntity, TTranslationEntity> : IRepository<IModelEntity>
        where TModelEntity : IModelEntity
        where TTranslationEntity : TranslationEntity<TModelEntity>
    {
        #region Methods

        IModelEntity Add(IModelEntity entity);

        Task AddRangeAsync(IEnumerable<IModelEntity> entities);

        void Delete(IModelEntity entity);

        void DeleteRange(IEnumerable<IModelEntity> entities);

        IModelEntity Update(IModelEntity entity);

        void UpdateRange(IEnumerable<IModelEntity> entities);

        #endregion Methods
    }

    public interface IModelWriteRepository<TModelEntity> : IRepository<IModelEntity>
    where TModelEntity : IModelEntity
    {
        #region Methods

        IModelEntity Add(IModelEntity entity);

        Task AddRangeAsync(IEnumerable<IModelEntity> entities);

        void Delete(IModelEntity entity);

        void DeleteRange(IEnumerable<IModelEntity> entities);

        IModelEntity Update(IModelEntity entity);

        void UpdateRange(IEnumerable<IModelEntity> entities);

        #endregion Methods
    }
```