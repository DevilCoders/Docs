# Ресурс /vendors/[vendorId]/[productKey]/billing/availableTransfer

## GET /vendors/[vendorId]/[productKey]/billing/availableTransfer

Запрос суммы в фишко-центах, доступной для перевода средств между офертными кампаниями вендора или агенства

### Примечания
  - Доступная сумма может отличаться от текущего баланса для кампаний с предоплатой, в случае, если тариф еще полностью не выбран.  
  В случае наличия админского или офертного отключения кампании, а также если кампания не является офертной - возвращается 0.
  Операция разрешена только для балансовых пользователей.

### Идентификаторы
  - **vendorId** `<ID>` - ID виртуального вендора источника
  - **productKey** `<ProductKey>` - указывает на кампанию источник для перевода, перечислимый тип для ключей списка платных услуг, описанный [тут](/_entities/ProductKey.md)

### Параметры
  - **uid** `<UID>` - UID пользователя
  
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
        - **centsAvailableForTransfer** `<Long>` - сумма в фишко-центах, доступная для перевода средств
  - errors `<Error[]>`
  
### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение productKey](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [У вендора {vendorId} нет активной кампании для типа продукта productKey](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)


