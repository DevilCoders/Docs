# Сущность "FeedQualityReport"

Отчёт по качеству VendorYML файлов

### Поля:
  - **categoryId** `<Long>` - идентификатор маркетной категории
  - categoryName `<String>` - полное имя категории
  - report `<Object>` - отчёт по качеству для категории
    - accepted `<Boolean>` - ???
    - paramsAccepted `<Boolean>` - приняты ли параметры категории
    - createdTimestamp `<DateTime>`(/_entities/DateTime.md)
    - params `[<Object>]` - отчёты по параметрам категории
      - paramId `<Integer>` - идентификатор параметра
      - name `<String>` - имя параметра
      - filledValueCount `<Integer>` - количество моделей с заполненным параметром
      - correctValueCount `<Integer>` - количество моделей с корректно заполненным параметром
      - allValueCount `<Integer>` - количество моделей с параметром
      - values `[<Object>]` - значения параметра
        - modelId `<Long>` - идентификатор модели
        - modelName `<String>` - заголовок модели
        - receivedValue `<String>` - полученное значение
        - correctValue `<String>` - исправленное значение
    - picture `<Object>` - отчёт по картинкам категории
      - accepted `<Boolean>` - приняты ли картинки в категории
      - goodPicturesCount `<Integer>` - количество хороших картинок
      - badPicturesCount `<Integer>` - количество плохих картинок
      - pictures `[<Object>]` - список картинок
        - url `<String>` - url картинки
        - message `<String>` - текстовое сообщение
        - watermark `<Boolean>` - признак присутствия ватермарков
        - relevant `<Boolean>` - признак релевантности картинки
        - cropped `<Boolean>` - признак применения crop
        - blur `<Boolean>` - признак применения blur
