# Ресурс /vendors/[vendorId]/modelEdit/requests/[requestId]/comments

## GET /vendors/[vendorId]/modelEdit/requests/[requestId]/comments

Получение комментариев к заявке на создание/изменение модели.

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - [Параметры пагинации](/_entities/Pager.md#Параметры)
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
      - **item** `<Object>`
        - **pager** [`<Pager>`](/_entities/Pager.md)
        - **items** `Array[`[`ModelEditRequestComment`](/_entities/model-editor/ModelEditRequestComment.md)`]` - комментарии к заявке, упорядоченные по дате написания (сначала свежие).
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
