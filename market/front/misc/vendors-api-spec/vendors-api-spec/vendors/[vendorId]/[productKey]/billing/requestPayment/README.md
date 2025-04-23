# Ресурс /vendors/[vendorId]/[productKey]/billing/requestPayment

## POST /vendors/[vendorId]/[productKey]/billing/requestPayment

Формирование недовыставленного счета 

### Примечания
  - Запрос летит в баланс через "коробку". В балансе формируется, так называемый, недовыставленный счет на указанную сумму.
  Баланс возвращает ссылку на страницу со сформированным недовыставленным счетом, пользователь может по ней перейти и продолжить
  процесс пополнения балансового счета уже в балансе.

### Параметры
  - **uid** `<UID>` - UID пользователя
  - **sumInCents** `<Long>` - сумма в фишко-центах, на которую требуется сформировать недовыставленный счет
  
### Идентификаторы
  - **vendorId** `<ID>` - вендорский ID
  - **productKey** `<ProductKey>` - перечислимый тип для ключей списка платных услуг, описанный [тут](/_entities/ProductKey.md)
  
### Ответ
  - **url** `<String>` - ссылка на страницу со сформированным недовыставленным счетом в балансе

### Ошибки

#### Попытка сформировать счёт по НЕ-предоплатной кампании
  - statusCode: `400`
  - code: `NON_PREPAID_CONTRACT_TYPE_PRODUCT_PAYMENT`
  - message: `Cannot request payment for non-prepaid contract type product!`

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет активной кампании для типа продукта productKey](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение productKey](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Некорректное значение sumInCents: должен быть от 0 до миллиарда рублей](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Некорректное значение vendorId: у vendorId есть админское или офертное отключение](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

