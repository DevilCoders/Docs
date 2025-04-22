# Ресурс /vendors/[vendorId]/modelEdit/params/colors

## GET /vendors/[vendorId]/modelEdit/params/colors

Получение вендорских цветов

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - **categoryId** `<Long>` - категория в рамках которой создан вендорский цвет
  - text `<String>` - поиск по имени цвета
  - [Параметры пагинации](/_entities/Pager.md#Параметры)
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array[`[`ModelColor`](/_entities/model-editor/ModelColor.md)`]>` - список доступных вендорских цветов
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
 
##### Примечания
Цвета в списке сортируются по имени в лексикографическом порядке.


## GET /vendors/[vendorId]/modelEdit/params/colors/[colorId]

Получение вендорского цвета по его идентификатору

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** [`ModelColor`](/_entities/model-editor/ModelColor.md) - вендорский цвет
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такого цвета](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## POST /vendors/[vendorId]/modelEdit/params/colors

Создание вендорского цвета

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Данные
  - **name** `<String>` - название вендорского цвета
  - **categoryId** `<Long>` - категория в рамках которой будет создан вендорский цвет
  - **baseColors** `<Array[<Integer>]>` - идентификаторы базовых цветов
  - pickers `<Array[`[`ModelImage`](/_entities/model-editor/ModelImage.md)`]>` - картинки-пикеры (тип PICKER)
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** [`ModelColor`](/_entities/model-editor/ModelColor.md) - созданный вендорский цвет
  - errors `<Error[]>`
  
### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## PUT /vendors/[vendorId]/modelEdit/params/colors/[colorId]

Изменение существующего вендорского цвета

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Данные
  - **name** `<String>` - название вендорского цвета
  - **categoryId** `<Long>` - категория в рамках которой создан вендорский цвет
  - **baseColors** `<Array[<Integer>]>` - идентификаторы базовых цветов
  - pickers `<Array[`[`ModelImage`](/_entities/model-editor/ModelImage.md)`]>` - картинки-пикеры (тип PICKER)
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** [`ModelColor`](/_entities/model-editor/ModelColor.md) - изменённый вендорский цвет
  - errors `<Error[]>`
  
### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такого цвета](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## DELETE /vendors/[vendorId]/modelEdit/params/colors/[colorId]

Удаление существующего вендорского цвета

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** [`ModelColor`](/_entities/model-editor/ModelColor.md) - удалённый вендорский цвет
  - errors `<Error[]>`
  
### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такого цвета](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
