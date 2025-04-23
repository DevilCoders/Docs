# Ресурс /entries/[ID]/status

## PUT /entries/[ID]/status

Cмена статуса заявки

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  - **status** `IN_WORK|ACCEPTED|CANCELLED`

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **status** `IN_WORK|ACCEPTED|CANCELLED`
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такой заявки](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверно указан status](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
