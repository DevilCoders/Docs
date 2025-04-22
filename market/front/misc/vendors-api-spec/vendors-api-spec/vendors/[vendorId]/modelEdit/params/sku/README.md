# Ресурс /vendors/[vendorId]/modelEdit/params/sku

## GET /vendors/[vendorId]/modelEdit/params/sku

Получение списка SKU модели

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - requestId `<Number>` - идентификатор заявки
  - modelId `<Number>` - идентификатор модели (если не задан идентификатор заявки)
  - text `<String>` - поиск по имени SKU
  - [Параметры пагинации](/_entities/Pager.md#Параметры)
 
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array[`[`ModelSku`](/_entities/model-editor/ModelSku.md)`]>` - список доступных SKU модели
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой модели](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
 

## GET /vendors/[vendorId]/modelEdit/params/sku/[skuId]

Получение SKU модели по его идентификатору

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** [`ModelSku`](/_entities/model-editor/ModelSku.md) - SKU модели
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такого SKU](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

 
## POST /vendors/[vendorId]/modelEdit/params/sku

Создание нового SKU модели

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
 
### Данные
  - **categoryId** `<Number>` - идентификатор категории
  - **parameters** `<Array[`[`ModelParameter`](/_entities/model-editor/ModelParameter.md)`]>` - параметры SKU 
  - requestId `<Number>` - идентификатор заявки
  - modelId `<Number>` - идентификатор модели (если не задан идентификатор заявки)
  - vendorColor [`<ModelColor>`](/_entities/model-editor/ModelColor.md) - вендорский цвет SKU модели
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** [`ModelSku`](/_entities/model-editor/ModelSku.md) - созданный SKU модели
  - errors `<Error[]>`
  
### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## PUT /vendors/[vendorId]/modelEdit/params/sku/[skuId]

Изменение существующего SKU модели

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Данные
  - **categoryId** `<Number>` - идентификатор категории
  - **parameters** `<Array[`[`ModelParameter`](/_entities/model-editor/ModelParameter.md)`]>` - параметры SKU 
  - requestId `<Number>` - идентификатор заявки
  - modelId `<Number>` - идентификатор модели (если не задан идентификатор заявки)
  - vendorColor [`<ModelColor>`](/_entities/model-editor/ModelColor.md) - вендорский цвет SKU модели
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** [`ModelSku`](/_entities/model-editor/ModelSku.md) - изменённый SKU модели
  - errors `<Error[]>`
  
### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такого SKU](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## DELETE /vendors/[vendorId]/modelEdit/params/sku/[skuId]

Удаление существующего SKU модели

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** [`ModelSku`](/_entities/model-editor/ModelSku.md) - удалённый SKU модели
  - errors `<Error[]>`
  
### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такого SKU](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
