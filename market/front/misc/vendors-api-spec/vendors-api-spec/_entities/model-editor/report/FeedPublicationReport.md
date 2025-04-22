# Сущность "FeedPublicationReport"

Отчёт по публикации VendorYML файлов

### Поля:
  - **categoryId** `<Long>` - идентификатор маркетной категории
  - categoryName `<String>` - полное имя категории
  - report `<Object>` - отчёт по качеству для категории
    - categoryId `<Number>` - идентификатор маркетной категории
    - sourceId `<Number>` - идентификатор источника в МБО
    - rawId `<String>` - идентификатор модели
    - title `<String>` - заголовок модели
    - published `<Boolean>` - была ли опубликована модель
    - requestId `<Number>` - идентификатор запроса в КВ
    - autoModelId `<Number>` - идентификатор авто-карточки
    - vendorModelId `<Number>` - идентификатор вендор-модели
    - guruModelId `<Number>` - идентификатор гуру-модели
  