# Ресурс /vendors/[vendorID]/recommended/shops

## GET /vendors/[vendorID]/recommended/shops

Получение магазинов, привязанных к вендору

### Параметры
  - **uid** `<UID>` - ID пользователя для аутентификации
  - text `<String>` - строка поиска по домену/имени/shopId
  - [Параметры пагинации](/_entities/Pager.md#Параметры)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array>`
        - **id** `<Integer>` - shopId магазина
        - **domain** `<String>` - домен магазина
        - name `<String>` - название магазина
        - **rating** `<Integer>` - рейтинг магазина
        - clones `<Array[Object]>`
          - **id** `<Integer>` - shopId клона
          - name `<String>` - название клона
          - **domain** `<String>` - домен клона
          - **status** `<VendorShopStatus>` - перечислимый тип для статуса рекомендованного магазина, описанный [тут](/_entities/VendorShopStatus.md)
        - bid `<Integer>` - ставка в центах (не передаётся в случае дефолтной ставки)
        - **status** `<VendorShopStatus>` - перечислимый тип для статуса рекомендованного магазина, описанный [тут](/_entities/VendorShopStatus.md)
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)

## POST /vendors/[vendorID]/recommended/shops

Привязка магазинов к услуге вендора "Рекомендованные магазины"

### Параметры
  - **uid** `<UID>` - ID пользователя для аутентификации

### Данные
  - **identifiers** `<Array[String]>` - идентификаторы (домены) магазинов, которые предлагается привязать

### Ответ
  - **meta** `<Object>`
  - result `<Array[Object]>` - результаты привязки магазина
    - **item** `<Array[Object]>`
      - **identifier** `<String>` - идентификатор (домен) магазина
      - **status** `<Boolean>` - статус привязки
      - reason `<Error>` - в случае неуспешной привязки, причина
      - shop `<Object>` - в случае успешной привязки, данные магазина
         - **id** `<Integer>` - shopId магазина
         - name `<String>` - название магазина
         - **domain** `<String>` - домен магазина
         - **status** `<VendorShopStatus>` - перечислимый тип для статуса рекомендованного магазина, описанный [тут](/_entities/VendorShopStatus.md)
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Не передан параметр identifiers](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
