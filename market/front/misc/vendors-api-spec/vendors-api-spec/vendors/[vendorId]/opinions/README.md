# Ресурс /vendors/[vendorId]/opinions

## GET /vendors/[vendorId]/opinions

Получение отзывов на товары вендора по его vendorId

### Доступы
vnd:feedback:read

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - modelId `<Number>` - идентификатор модели
  - from [`<DateTime>`](/entries/DateTime) - левая граница фильтра по дате
  - to [`<DateTime>`](/entries/DateTime) - правая граница фильтра по дате
  - grade `<Integer>` - фильтрация по оценке
  - withoutAnswer `<Boolean>` - только отзывы без ответа
  - onlyCpa `<Boolean>` - отзывы только проверенных покупателей
  - orderBy `<String>` - сортировка результата (`date` - по дате)
  - orderDirection `<String>` - направление сортировки (`asc`|`desc`. По-умолчанию - `asc`.)
  - [Параметры пагинации](/_entities/Pager.md#Параметры)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array[`[ModelOpinion](/_entities/opinions/ModelOpinion.md)`]>` - отзывы на модели вендора
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## GET /vendors/[vendorId]/opinions/count

Получение количества отзывов на товары вендора по его vendorId

### Доступы
vnd:feedback:read

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Number>` - количество отзывов на модели вендора
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## POST /vendors/[vendorId]/opinions/[opinionId]/comment

Создание комментария к отзыву или комментарию на отзыв

### Доступы
vnd:feedback:write

### Параметры
  - **modelId** `<Number>` - id модели для которой создаётся комментарий
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  - **text** `<String>` - текст комментария от вендора
  - parentId `<Number>` - идентификатор родительского комментария (если отвечаем на комментарий)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Number>` - идентификатор созданного комментария
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## PUT /vendors/[vendorId]/opinions/[opinionId]/comment/[commentId]

Изменение комментария к отзыву или комментарию на отзыв.

### Примечания

Работает только для коментариев без ответа.

### Доступы
vnd:feedback:write

### Параметры
  - **modelId** `<Number>` - id модели для которой изменяется комментарий
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  - **text** `<String>` - новый текст комментария от вендора

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Boolean>` - признак успешности изменений
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## DELETE /vendors/[vendorId]/opinions/[opinionId]/comment/[commentId]

Удаление комментария к отзыву или комментарию на отзыв.

### Примечания

Работает только для коментариев без ответа.

### Доступы
vnd:feedback:write

### Параметры
  - **modelId** `<Number>` - id модели для которой удаляется комментарий
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Boolean>` - признак успешности удаления
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
