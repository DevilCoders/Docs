# Ресурс /vendors/[vendorId]/[productKey]/billing/makeTransfer/[toVendorId]/[toProductKey]

## POST /vendors/[vendorId]/[productKey]/billing/makeTransfer/[toVendorId]/[toProductKey]

Перевод средств между офертными кампаниями вендора или агенства

### Примечания
  - Запрос на перевод средств между кампаниями вендора летит в баланс через "коробку". 
  Баланс осуществляет перевод средств и в коробку летят нотификации по обеим кампаниям на зачисление и списание указанной суммы.
  Перевод средств разрешен только для существующих кампаний вендора или агенств без админских и офертных отключений, 
  с одинаковым балансовым клиентом и предоплатным типом контракта. У заказа источника должно быть достаточно средств для перевода на целевой заказ.  
  Операция разрешена только для балансовых пользователей.

### Идентификаторы
  - **vendorId** `<ID>` - ID виртуального вендора источника
  - **productKey** `<ProductKey>` - указывает на кампанию источник для перевода, перечислимый тип для ключей списка платных услуг, описанный [тут](/_entities/ProductKey.md)
  - **toVendorId** `<ID>` - ID целевого виртуального вендора
  - **toProductKey** `<ProductKey>` - указывает на целевую кампанию для перевода, перечислимый тип для ключей списка платных услуг, описанный [тут](/_entities/ProductKey.md)

### Параметры
  - **sumInCents** `<Long>` - сумма в фишко-центах, которую требуется перевести с заказа источника на целевой заказ
  - **uid** `<UID>` - UID пользователя
  
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
        - **status** `<Boolean>` - если перевод средств успешно завершен, то вернется true, в противном случае прилетит ошибка
  - errors `<Error[]>`
  
### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение productKey](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Некорректное значение toProductKey](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [У вендора {vendorId} нет активной кампании для типа продукта productKey](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [У вендора {toVendorId} нет активной кампании для типа продукта toProductKey](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение sumInCents: должен быть от 0 до миллиарда рублей](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [У вендора {vendorId} есть админское или офертное отключение для кампании по продукту productKey](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
  - statusCode: `400`
  - code: `CUTOFF_PRODUCT_MAKE_TRANSFER_FROM`
  - message: `vendor {vendorId} has open ADMIN or OFFER cutoff and is not allowed to make transfer`
  - details - список неверных/отсутствующих параметров
    - "productKey": "INVALID"
#### [У вендора {toVendorId} есть админское или офертное отключение для кампании по продукту toProductKey](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
  - statusCode: `400`
  - code: `CUTOFF_PRODUCT_MAKE_TRANSFER_TO`
  - message: `vendor {toVendorId} has open ADMIN or OFFER cutoff and is not allowed to make transfer`
  - details - список неверных/отсутствующих параметров
    - "toProductKey": "INVALID"
#### [Кампания вендора {vendorId} для продукта productKey не является предоплатной](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
  - statusCode: `400`
  - code: `NON_PREPAID_CONTRACT_TYPE_PRODUCT_FOR_TRANSFER_FROM`
  - message: `Cannot make transfer from non-prepaid contract type product!`
  - details - список неверных/отсутствующих параметров
    - "productKey": "INVALID"
#### [Кампания вендора {toVendorId} для продукта toProductKey не является предоплатной](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
  - statusCode: `400`
  - code: `NON_PREPAID_CONTRACT_TYPE_PRODUCT_FOR_TRANSFER_TO`
  - message: `Cannot make transfer to non-prepaid contract type product!`
  - details - список неверных/отсутствующих параметров
    - "toProductKey": "INVALID"
#### [Балансовые клиенты для кампании источника и целевой кампании различаются](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
  - statusCode: `400`
  - code: `CLIENT_ID_DIFFERS`
  - message: `Cannot make transfer to destination product with client id differs from source product!`
  - details - список неверных/отсутствующих параметров
    - "toProductKey": "INVALID"
#### [На счете кампании источнике по продукту productKey нет указанной суммы {sumInCents}](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
  - statusCode: `400`
  - code: `BUSINESS_RULE_VIOLATION`
  - message: `Not enough balance {fromCampaignOldBalance} for campaign {fromServiceId}-{fromCampaignId} to transfer {transferSumInCents}`
  - details - список неверных/отсутствующих параметров
    - "sumInCents": "INVALID"
#### [Баланс не может перевести указанную сумму {sumInCents} с заказа на заказ (причины разные)](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
  - statusCode: `400`
  - code: `BALANCE_SERVICE_ERROR`
  - message: `<error><msg><сообщение от баланса></msg>...<contents><описание></contents></error>`
     (пример ответа от баланса: `<error><msg>QTY for order_id = 221347010 do not match (balance value=0.000000, service value=828.333333</msg><balance-consume-qty ></balance><order-id>221347010</order-id><wo-rollback>0</wo-rollback><service-consume-qty>828.333333</service-consume-qty><method>Balance2.CreateTransferMultiple</method><code>ORDERS_NOT_SYNCHRONIZED</code><parent-codes><code>EXCEPTION</code></parent-codes><contents>QTY for order_id = 221347010 do not match (balance value=0.000000, service value=828.333333</contents></error>`)
  - details - список неверных/отсутствующих параметров
    - "sumInCents": "INVALID"


