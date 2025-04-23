# Ресурс /vendors/[vendorID]/recommended/bid

## GET /vendors/[vendorID]/recommended/bid

Получение текущей общей ставки услуги "Рекомендованные магазины" для выбранного вендора

### Параметры
  - **uid** `<UID>`

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - bid `<Integer>` - общая ставка в центах (не передаётся в случае дефолтной ставки)
  - errors`<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)

## PUT /vendors/[vendorID]/recommended/bid

Изменение текущей общей ставки услуги "Рекомендованные магазины" для выбранного вендора

### Параметры
  - **uid** `<UID>`

### Данные
  - **bid** `<Integer>` - новое значение общей ставки в центах
      - значение ставки имеет ограничение в пределах [0, 9999]

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **bid** `<Integer>` - общая ставка в центах (изменённая)
  - errors`<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение bid](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
