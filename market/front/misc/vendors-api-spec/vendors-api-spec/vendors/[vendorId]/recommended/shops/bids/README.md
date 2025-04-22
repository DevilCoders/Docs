# Ресурс /vendors/[vendorID]/recommended/shops/bids

## POST /vendors/[vendorID]/recommended/shops/bids

Изменение ставок магазинов

### Параметры
  - **uid** `<UID>`

### Данные
 - **bids** `<Array[Object]>`
    - **shopId** `<Integer>` - идентификтор магазина
    - **bid** `<null|Integer>` - новая ставка в центах
      - значение ставки имеет ограничение в пределах [0, 9999]
      - значение `null` означает сброс ставки до ставки по умолчанию

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Array[Object]>`
      - **shopId** `<Integer>` - идентификатор магазина
      - **status** `<Boolean>` - статус операции
      - bid `<null|Integer>` - в случае успешного выставления ставки - новое значение ставки, иначе отсутствует
        - Для ставки по умолчанию используется значение null
      - reason `<Error>` - в случае неуспешного выставления ставки - причина, иначе отсутствует
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такого магазина у этого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверное значение ставки](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
