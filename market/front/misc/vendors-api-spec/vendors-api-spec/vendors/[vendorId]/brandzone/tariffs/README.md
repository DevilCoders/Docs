# Ресурс /vendors/[vendorId]/brandzone/tariffs

## GET /vendors/[vendorId]/brandzone/tariffs

Получение текущего тарифа услуги "Бренд-зона на Сервисе Яндекс.Маркет" для вендора

### Параметры
  - **uid** `<UID>`

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Array[`[Tariff](/_entities/Tariff.md)`]>` - список текущих тарифов вендора по услуге "Бренд-зона"
  - errors`<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)


## POST /vendors/[vendorId]/brandzone/tariffs

Добавление/изменение следующего тарифа услуги "Бренд-зона на Сервисе Яндекс.Маркет" для вендора (пока доступно только менеджерам)

### Примечания
  - Если передан тариф, совпадающий с текущим, то следующий тариф удаляется (если он был задан)

### Параметры
  - **uid** `<UID>`

### Данные
  - **id** `<Integer>` - идентификатор нового тарифа

### Ответ
- [см GET /vendors/[vendorId]/brandzone/tariffs](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/brandzone/tariffs#get-vendorsvendoridbrandzonetariffs#Ответ)

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неправильно указан ID тарифа](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

