# Ресурс /tariffs

## GET /tariffs

Получение списка тарифов услуги "Рекомендованные магазины" - **@deprecated**

### Параметры
  - **uid** `<UID>` - сейчас необязательный параметр из-за [бага](https://st.yandex-team.ru/VNDMARKET-53)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **tariffs** `<Array[Object]>` - список тарифов
        - **id** `<Integer>` - идентификатор тарифа
        - **name** `<String>` - название тарифа
        - **details** `<Object>` - описание тарифа
          - **minShops** `<Integer>` - минимальное кол-во магазинов, предусмотренных тарифом
          - maxShops `<Integer>` - максимальное кол-во магазинов, предусмотренных тарифом
          - **cost** `<Integer>` - стоимость тарифа в центах
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
