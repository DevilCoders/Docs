# Ресурс /vendors/[vendorId]/modelbids/promotion
## GET /vendors/[vendorId]/modelbids/promotion/models

Получение моделей, исторической информации по кликам, заказам и показам и прогнозу по их категориям

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - orderBy `<Enum>` - поле сортировки: "POPULARITY"|"PRICE"|"DATE"|"QUALITY"|"OPINIONS". По-умолчанию: "POPULARITY"
  - orderDirection `<Enum>` - направление сортировки: "ASC"|"DESC". По-умолчанию: "DESC"
  - modelName `<String>` - фильтр по названию товара
  - categoryId `<Number>` - фильтр по id категории
  - bidFrom `<Number>` - фильтр по нижней границе ставки (в фишкоцентах)
  - bidTo `<Number>` - фильтр по верхней границе ставки (в фишкоцентах)
  - priceFrom `<Number>` - фильтр по нижней границе цены (в рублях)
  - priceTo `<Number>` - фильтр по верхней границе цены (в рублях)
  - page `<Number>` - номер страницы
  - pageSize `<Number>` - количество элементов на странице (по-умолчанию - 30)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **models** `<Array[`[ModelForecast](/_entities/modelbids/ModelForecast.md)`]>` - список товаров вендора
      - hidForecast `<Array[`[CategoryForecast](/_entities/modelbids/CategoryForecast.md)`]>` - прогноз по кликам в
        категориях вендора
  - errors `<Error[]>`

### Примечания
 - Возможные комбинации сортировки: POPULARITY+DESC, PRICE+ASC, PRICE+DESC, DATE+DESC, QUALITY+DESC, OPINIONS+DESC
 - hidForecast включает в себя только категории из текущей страницы товаров

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

## GET /vendors/[vendorId]/modelbids/promotion/categories/[categoryId]

Получение исторических данных и прогноза по потраченным средствам, кликам, показам и заказам в категории

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - categoryId `<Number>` - идентификатор категории
      - categoryName `<String>` - название категории
      - spentInCents `<Number>` - количество потраченных фишкоцентов на продвижение товаров в выбранной категории 
      - clicksCount `<Number>` - количестве кликов на товары в выбранной категории (только аукцион)
      - showsCount `<Number>` - количество показов товара в выбранной категории (только аукцион)
      - ordersCount `<Number>` - количество заказов товара в выбранной категории (только аукцион)
      - hidForecast [`CategoryForecast`](/_entities/modelbids/CategoryForecast.md) - прогноз по кликам, показам 
          и покупкам в выбранной категории (только аукцион)
  - errors `<Error[]>`
