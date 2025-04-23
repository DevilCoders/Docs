# Сущность "FeedParametersReport"

Отчёт по параметрам VendorYML файлов

### Поля:
  - **categoryId** `<Long>` - идентификатор маркетной категории
  - categoryName `<String>` - полное имя категории
  - report `<Object>` - отчёт по параметрам для категории
    - responseStatus `<Object>` - статус обработки
      - result `<String>` - код статуса (OK | ILLEGAL_ARGUMENT | INTERNAL_ERROR)
      - errorMessage `<String>` - текст сообщения об ошибке
    - vendorParams `[`[`<FeedVendorParam>`](/_entities/model-editor/report/FeedVendorParam.md)`]` - список полученных параметров
    
