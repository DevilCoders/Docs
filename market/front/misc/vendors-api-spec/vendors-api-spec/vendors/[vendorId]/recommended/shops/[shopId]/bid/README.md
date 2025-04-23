# Ресурс /vendors/[vendorID]/recommended/shops/[shopId]/bid

## PUT /vendors/[vendorID]/recommended/shops/[shopId]/bid

Изменение ставки магазина

### Параметры
  - **uid** `<UID>`
  - **bid** `<String>` - https://st.yandex-team.ru/VNDMARKET-19
    - значение ставки имеет ограничение в пределах [0, 9999]
    - [Сброс ставки магазина до дефолтной пока не поддерживается](https://st.yandex-team.ru/VNDMARKET-19#1468226269000)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **bid** `<null|Integer>` - новая ставка магазина
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такого магазина у этого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверное значение ставки](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

## DELETE /vendors/[vendorID]/recommended/shops/[shopId]/bid

Сброс ставки магазина на дефолтную

### Параметры
  - **uid** `<UID>`

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **status** `<Boolean>`
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такого магазина у этого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
