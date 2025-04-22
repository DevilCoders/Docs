# Ресурс /vendors/[vendorId]/questions

## GET /vendors/[vendorId]/questions

Получение вопросов на товары вендора по его vendorId

### Доступы
vnd:questions:read

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - modelId `<Number>` - идентификатор товара
  - from [`<DateTime>`](/entries/DateTime) - левая граница фильтра по дате
  - to [`<DateTime>`](/entries/DateTime) - правая граница фильтра по дате
  - withoutAnswer `<Boolean>` - только вопросы без ответа, только с ответом или все вопросы (если параметр не задан)
  - orderBy `<String>` - сортировка результата (`date` - по дате, `id` - по id вопроса)
  - orderDirection `<String>` - направление сортировки (`asc`|`desc`. По-умолчанию - `desc`.)
  - [Параметры пагинации](/_entities/Pager.md#Параметры)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array[`[ModelQuestion](/_entities/questions/ModelQuestion.md)`]>` - вопросы на товары вендора
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## GET /vendors/[vendorId]/questions/count

Получение количества вопросов на товары вендора по его vendorId

### Доступы
vnd:questions:read

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Number>` - количество вопросов на товары вендора
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## POST /vendors/[vendorId]/questions/[questionsId]/answer

Создание ответа на вопрос по товару

### Доступы
vnd:questions:write

### Параметры
  - **modelId** `<Number>` - id товара для которой создаётся ответ
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  - **text** `<String>` - текст ответа от вендора (максимум 5000 символов)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Number>` - идентификатор созданного ответа
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## PUT /vendors/[vendorId]/questions/[questionsId]/answer/[answerId]

Изменение ответа на вопрос по товару

### Примечания

Работает только для коментариев без ответа.

### Доступы
vnd:questions:write

### Параметры
  - **modelId** `<Number>` - id товара для которой изменяется ответ
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  - **text** `<String>` - новый текст ответа от вендора (максимум 5000 символов)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Boolean>` - признак успешности изменений
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## DELETE /vendors/[vendorId]/questions/[questionsId]/answer/[answerId]

Удаление ответа на вопрос по товару

### Примечания

Работает только для ответов без комментариев.

### Доступы
vnd:questions:write

### Параметры
  - **modelId** `<Number>` - id товара для которой удаляется ответ
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

## POST /vendors/[vendorId]/questions/[questionId]/answer/[answerId]/comment

Создание комментария к ответу на вопрос по товару

### Доступы
vnd:questions:write

### Параметры
  - **modelId** `<Number>` - id товара для которой создаётся комментарий
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  - **text** `<String>` - текст комментария от вендора (максимум 5000 символов)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Number>` - идентификатор созданного комментария
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## PUT /vendors/[vendorId]/questions/[questionId]/answer/[answerId]/comment/[commentId]

Изменение комментария к ответу на вопрос по товару

### Доступы
vnd:questions:write

### Параметры
  - **modelId** `<Number>` - id товара для которой изменяется комментарий
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  - **text** `<String>` - новый текст комментария от вендора (максимум 5000 символов)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Boolean>` - признак успешности изменений
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## DELETE /vendors/[vendorId]/questions/[questionId]/answer/[answerId]/comment/[commentId]

Удаление комментария к ответу на вопрос по товару

### Доступы
vnd:questions:write

### Параметры
  - **modelId** `<Number>` - id товара для которой удаляется комментарий
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
