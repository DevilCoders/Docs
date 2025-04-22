# Ресурс /vendors/[vendorID]/recommended/blacklist/[shopId]

## DELETE /vendors/[vendorID]/recommended/blacklist/[shopId]

Удаление магазина из чёрного списка услуги "Рекомендованные магазины"

### Параметры
  - **uid** `<UID>`

### Ответ
  - **meta** `<Object>`
  - status `<Boolean>` - статус удаления
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Такого магазина нет в черном списке](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
