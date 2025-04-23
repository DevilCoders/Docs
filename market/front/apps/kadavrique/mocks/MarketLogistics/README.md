# Market Logistics (Market TPL)

## Swagger оригинального бекенда

[Трекинг курьера | Яндекс.Покупки Touch](https://tpl-int.tst.vs.market.yandex.net/swagger-ui.html#/tracking-controller)

[Курьеры | Партнёрские интерфейсы](https://tpl-int.tst.vs.market.yandex.net/swagger-ui.html#/partner-user-controller)

[Компании-партнёры | Партнёрские интерфейсы](https://tpl-int.tst.vs.market.yandex.net/swagger-ui.html#/partner-company-controller)

## Замоканные пути

- **Трекинг курьера | Яндекс.Покупки Touch**
    - `GET` /internal/tracking/\<trackingId\>
    - `GET` /internal/tracking/\<trackingId\>rescheduleDates
    - `POST` /internal/tracking/\<trackingId\>/cancel
    - `POST` /internal/tracking/\<trackingId\>/reschedule
    - `GET` /internal/tracking/\<trackingId\>/courier-location
    - `POST` /internal/tracking/\<trackingId\>/confirmDeliveryReschedule


- **Курьеры | Партнёрские интерфейсы**
    - `GET` /internal/partner/users
    - `POST` /internal/partner/users
    - `GET` /internal/partner/users/\<id\>
    - `PUT` /internal/partner/users/\<id\>


- **Заказы | Партнёрские интерфейсы**
    - `GET` /internal/partner/orders/\<orderId\>
    - `GET` /internal/partner/orders/\<orderId\>/events
    - `POST` /internal/partner/orders/\<orderId\>/reopen
    - `GET` /internal/partner/orders/\<orderId\>/cancel/reasons
    - `PATCH` /internal/partner/v2/orders/\<orderId\>/reopen
    - `GET` /internal/partner/orders/\<orderId\>/rescheduleDates
    - `PATCH` /````internal/partner/orders/\<orderId\>/update-coords


- **Фильтры | Партнёрские интерфейсы**
    - `GET` /internal/partner/filters/courierToReassign
    - `GET` /internal/partner/filters
    - `GET` /internal/partner/filters/cities
    - `GET` /internal/partner/filters/sorting-center


- **Компании-партнёры | Партнёрские интерфейсы**
    - `GET` /internal/partner/companies
    - `POST` /internal/partner/companies
    - `GET` /internal/partner/companies/\<id\>
    - `PUT` /internal/partner/companies/\<id\>


- **Маршрутизация | Партнёрские интерфейсы**
    - `GET` /internal/partner/routing
    - `POST` /internal/partner/routing


-  **Типы транспортных средств | Партнёрские интерфейсы**
    - `GET` /internal/partner/transportTypes
    - `POST` /internal/partner/transportTypes
    - `GET` /internal/partner/transportTypes/\<id\>
    - `PUT` /internal/partner/transportTypes/\<id\>


- **Дропшипы | Партнёрские интерфейсы**
    - `GET` /internal/partner/dropships/\<dropshipId\>
    - `POST` /internal/partner/dropships/\<movementId\>/cancel
    - `POST` /internal/partner/dropships/\<movementId\>/reopen
    - `POST` /internal/partner/dropships/\<movementId\>/cancel-task'
    - `POST` /internal/partner/dropships/\<movementId\>/reopen-task

- **Список LifePos транзакций | Партнёрские интерфейсы**
    - `GET` /internal/partner/transaction
