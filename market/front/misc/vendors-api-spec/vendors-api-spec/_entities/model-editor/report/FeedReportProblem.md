# Сущность "FeedReportProblem"

Группа однотипных ошибок в переданном вендором VendorYML файле

### Поля:
  - priority `<String>` - приоритет ошибок (WARNING | CRITICAL)
  - count `<Integer>` - количество аналогичных ошибок
  - text `<String>` - текстовое описание ошибок
  - messages `[`[`<FeedReportMessage>`](/_entities/model-editor/report/FeedReportMessage.md)`]` - список сообщений об ошибках
