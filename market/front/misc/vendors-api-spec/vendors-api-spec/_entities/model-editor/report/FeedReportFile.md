# Сущность "FeedReportFile"

Переданный вендором VendorYML файл

### Поля:
  - url `<String>` - ссылка на файл
  - status `<String>` - статус обработки файла (OK | DOWNLOAD_ERROR | WRONG_FORMAT | EMPTY_FILE)
  - statusText `<String>` - дополнительное описание статуса обработки 
  - message [`<FeedReportMessage>`](/_entities/model-editor/report/FeedReportMessage.md) - сообщение с описанием файла
  - problems `[`[`<FeedReportProblem>`](/_entities/model-editor/report/FeedReportProblem.md)`]` - список ошибок файла
  - metrics `[`[`<FeedReportMetric>`](/_entities/model-editor/report/FeedReportMetric.md)`]` - список метрик файла
