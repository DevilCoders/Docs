# Ресурс /tariffs/analytics

## GET /tariffs/analytics

Получение списка тарифов услуги "Маркет.Аналитика"

### Параметры
  - **uid** `<UID>` - обязательный параметр для авторизации

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **tariffs** `<Array[`[Tariff](/_entities/Tariff.md)`]>` - список доступных тарифов услуги "Маркет.Аналитика"
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)