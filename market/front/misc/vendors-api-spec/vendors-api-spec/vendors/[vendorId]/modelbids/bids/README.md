# Ресурс /vendors/[vendorID]/modelbids/bids

## POST /vendors/[vendorID]/modelbids/bids

Получение данных из Репорта по фильтру и ставок по моделям из Биддинга

### Параметры
  - **uid** `<UID>`
  
### Данные
  - **filter** `<String>` - параметры запроса к Репорту одной строкой, как описано [тут](https://wiki.yandex-team.ru/Market/Verstka/report-query-params/)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **reportResponse** `<JSON>` - ответ от Репорта как есть
      - bidsFromBidding `<Array[Object]>` - список ставок по моделям со статусами из Биддинга, элемент отсутствует если Биддинг не доступен или возвращает ошибки
        - **datasourceId** `<Long>` - вендорский айдишник по ставкам, соответствует datasourceId вендора и кампании
        - **modelId** `<Long>` - айдишник модели
        - **value** `<Integer>` - значение ставки
        - **status** `<Enum>` - статус ставки, может принимать значения APPLIED|PENDING|NOT_ALLOWED|NOT_FOUND|WRONG_BID_VALUE
  - errors`<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора или нет такой услуги у данного вендора](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Ошибки Репорта вида 4XY транслируются в 'Неверные параметры вызова' для параметра filter](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### HTTP ошибки Репорта, **отличные** от 4XY, транслируются в REPORT_HTTP_FAILED с соответствующим статусом от Репорта
#### Не HTTP ошибки, связанные с вызовом Репорта, транслируются в REPORT_UNKNOWN_FAILED со статусом 500
#### Ошибки, связанные с обработкой ответа Репорта, транслируются в REPORT_UNEXPECTED_RESPONSE со статусом 500

## PUT /vendors/[vendorID]/modelbids/bids

Установка ставок на модели (или категории) для выбранного вендора

### Параметры
  - **uid** `<UID>`

### Данные
  - **bids** `<Map<Long, Integer>>` - словарь айдишек моделей (или категорий) и их ставок
      - значение ставки имеет ограничение в пределах [0, 8400]
  - bidsTarget `MODELS|CATEGORIES` - в зависимости от значения этого параметра ставки будут применены к моделям либо к категориям 
    - к моделям, если bidsTarget=MODELS 
    - к категориям, если bidsTarget=CATEGORIES
    - значение параметра по умолчанию bidsTarget=MODELS

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **status** `<boolean>` - если все ставки применены, то вернется true, в противном случае прилетит ошибка
  - errors`<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора или нет такой услуги у данного вендора](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Некорректное значение bids](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
    Варианты:
    1. Значение ставки из недопустимого диапазона ("bid should be in range [0, 8400]")
    2. Модель или категория не относятся к вендору ("model '%id' doesn't belong to vendor's categories" или "category '%id' doesn't belong to vendor")
#### [Неизвестное значение bidsTarget](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Услуга "Ставки на модели" для данного вендора отключена и манипуляции со ставками невозможны](https://github.yandex-team.ru/market/vendors-api-spec#Есть-активные-отключения)

## DELETE /vendors/[vendorID]/modelbids/bids

Сброс ставок на модели (или категории) для выбранного вендора

### Параметры
  - **uid** `<UID>`
  - **ids** `<String>` - строка со списком айдишек моделей (или категорий), перечисленных через запятую 
  - bidsTarget `MODELS|CATEGORIES` - в зависимости от значения этого параметра ставки будут сброшены у моделей либо у категорий 
    - у моделей, если bidsTarget=MODELS 
    - у категорий, если bidsTarget=CATEGORIES
    - значение параметра по умолчанию bidsTarget=MODELS

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **status** `<boolean>` - если все ставки cброшены, то вернется true, в противном случае прилетит ошибка
  - errors`<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора или нет такой услуги у данного вендора](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Некорректное значение bids](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
    Варианты:
    1. Значение ставки из недопустимого диапазона ("bid should be in range [0, 8400]")
    2. Модель или категория не относятся к вендору ("model '%id' doesn't belong to vendor's categories" или "category '%id' doesn't belong to vendor")
#### [Неизвестное значение bidsTarget](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Услуга "Ставки на модели" для данного вендора отключена и манипуляции со ставками невозможны](https://github.yandex-team.ru/market/vendors-api-spec#Есть-активные-отключения)
