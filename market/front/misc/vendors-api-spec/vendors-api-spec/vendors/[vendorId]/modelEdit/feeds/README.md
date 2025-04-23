# Ресурс /vendors/[vendorId]/modelEdit/feeds

## POST /vendors/[vendorId]/modelEdit/feeds

Сохранение заданного вендором списка файлов с данными о моделях.

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Данные
  - feeds `Array[`[`ModelEditFeed`](/_entities/model-editor/ModelEditFeed.md)`]` - список файлов с данными о моделях
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **feeds** `Array[`[`ModelEditFeed`](/_entities/model-editor/ModelEditFeed.md)`]` - актуальный список файлов с данными о моделях
      - **updateTime** [`<DateTime>`](/_entities/DateTime.md) - дата последнего изменения списка файлов с данными о моделях
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## GET /vendors/[vendorId]/modelEdit/feeds

Получение заданного вендором списка файлов с данными о моделях.

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **feeds** `Array[`[`ModelEditFeed`](/_entities/model-editor/ModelEditFeed.md)`]` - последний заданный вендором список файлов с данными о моделях
      - **updateTime** [`<DateTime>`](/_entities/DateTime.md) - дата последнего изменения списка файлов с данными о моделях
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## GET /vendors/[vendorId]/modelEdit/feeds/templates

Получение шаблона файла с данными о моделях (для категории).

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - **categoryId** `<Number>` - идентификатор категории
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **url** `<String>` - ссылка на файл с данными о моделях
      - **text** `<String>` - имя файла с данными о моделях
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
