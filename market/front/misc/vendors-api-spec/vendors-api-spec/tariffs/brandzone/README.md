# Ресурс /tariffs/brandzone

## GET /tariffs/brandzone

Получение списка тарифов услуги "Бренд-зона"

### Параметры
  - **uid** `<UID>` - обязательный параметр для авторизации

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **tariffs** `<Array[`[Tariff](/_entities/Tariff.md)`]>` - список доступных тарифов услуги "Бренд-зона"
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
