# Ресурс /vendors/[vendorID]/recommended/shops/[shopId]

## DELETE /vendors/[vendorID]/recommended/shops/[shopId]

Удаление магазина из списка рекомендованных

### Параметры
  - **uid** `<UID>`

### Ответ
  - **meta** `<Object>`
  - errors `<Error[]>`
  - result `<Object>`
    - **status** `<Boolean>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такого магазина у этого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
