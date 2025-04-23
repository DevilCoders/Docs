# Ресурс /vendors/[vendorId]/modelEdit/feeds/reports

## GET /vendors/[vendorId]/modelEdit/feeds/reports

Получение отчётов по обработке файлов с данными о моделях

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - validationReport [`<FeedValidationReport>`](/_entities/model-editor/report/FeedValidationReport.md) - отчёт по валидации переданных VendorYML файлов
      - parametersReport `[`[`<FeedParametersReport>`](/_entities/model-editor/report/FeedParametersReport.md)`]` - отчёт по параметрам категорий для переданных VendorYML файлов
      - qualityReport `[`[`<FeedQualityReport>`](/_entities/model-editor/report/FeedQualityReport.md)`]` - отчёт по качеству категорий для переданных VendorYML файлов
      - publicationReport `[`[`<FeedPublicationReport>`](/_entities/model-editor/report/FeedPublicationReport.md)`]` - отчёт по публикации моделей в категориях для переданных VendorYML файлов
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
