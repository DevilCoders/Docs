# Ресурс /licensors/[licensorId]/modelEdit/params/colors

## GET /licensors/[licensorId]/modelEdit/params/colors

Получение вендорских цветов. Если по заданной в парамтерах связке brandId-categoryId найден вендор, то работаем с цветами найденного вендора.

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - **brandId** `<Number>` - идентификатор бренда, по которому будет выбран соответствующий вендор в КВ, цвета которого нужно выбрать
  - **categoryId** `<Number>` - категория в рамках которой создан вендорский цвет
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


## GET /licensors/[licensorId]/modelEdit/params/colors/[colorId]

Получение вендорского цвета по его идентификатору

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - **brandId** `<Number>` - идентификатор бренда, по которому будет выбран соответствующий вендор в КВ, цвета которого нужно выбрать
  - **categoryId** `<Number>` - категория в рамках которой создан вендорский цвет
    
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


## POST /licensors/[licensorId]/modelEdit/params/colors

Создание вендорского цвета

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - **brandId** `<Number>` - идентификатор бренда, по которому будет выбран соответствующий вендор в КВ, для которого будет создан цвет
  - **categoryId** `<Number>` - категория в рамках которой создан вендорский цвет
  
### Данные
  - **name** `<String>` - название вендорского цвета
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


## PUT /licensors/[licensorId]/modelEdit/params/colors/[colorId]

Изменение существующего вендорского цвета

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - **brandId** `<Number>` - идентификатор бренда, по которому будет выбран соответствующий вендор в КВ, для которого будет изменён цвет
  - **categoryId** `<Number>` - категория в рамках которой создан вендорский цвет
  
### Данные
  - **name** `<String>` - название вендорского цвета
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


## DELETE /licensors/[licensorId]/modelEdit/params/colors/[colorId]

Удаление существующего вендорского цвета

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - **brandId** `<Number>` - идентификатор бренда, по которому будет выбран соответствующий вендор в КВ, из цветов которого нужно удалить цвет
  - **categoryId** `<Number>` - категория в рамках которой создан вендорский цвет
  
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