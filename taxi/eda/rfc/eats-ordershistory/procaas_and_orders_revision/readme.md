## Перевод eats-ordershistory на получение ордеров из procaas
### Задача
+ Избавиться от механизма получения ордеров из stq, перейти на procaas (через logbroker)
+ Расширить информацию об ордерах, добавить статусы, помимо корзины хранить информацию о дополнительных услугах (чаевые, сервис фи, и т.д.), добавить информацию об изменения в заказе (разница между начальной и конечной корзиной), потребитель плнируется пока один: eats-orders-info (подэпик: [EDAEATERS-1510](https://st.yandex-team.ru/EDAEATERS-1510))
### Решение
1. Для получения ордеров из логброкера будем использовать [библиотеку eats-procaas-orders-client](https://wiki.yandex-team.ru/taxi/backend/userver/libraries/eats-procaas-orders-client/#poleznajainformacija)
2. За корзиной и стоимостью услуг будем ходить в [сервис eats-order-revision](https://wiki.yandex-team.ru/eda/team/backend/platformteams/team-prime-time/proekty-komandy/eats-order-revision/) при создании и закрытии ордера
3. Для получения адресов доставки будем ходить в [ручку коры /internal/v1/order/address](https://st.yandex-team.ru/EDACOMMON-1694) при создании заказа 

#### Изменения в api:
Основные изменения: 
* замена статусов на [статусы из procaas](https://wiki.yandex-team.ru/eda/dev/backend/services/procaas/#klientskijjzakaz) (за исключением `finished`, вместо него оставили `delivered` для обратной совместимости)   
* удаление из корзины `place_menu_item_id` (вместо него преполагается использование `origin_id`), т.к. в сервисе `eats-orders-revision` его нет.
* удаление `flow_type` (сейчас нет потребителей), `flow_type` был нужен в основном для определения самовывоза, для этого можно будет использовать `shipping_type` 
* удаление `product_id` (дублировал `origin_id`)

Следующие изменения необходимы для реализации [EDAEATERS-1510](https://st.yandex-team.ru/EDAEATERS-1510) и не ломают обратную совместимость:
* В ручку `/internal/v1/get-orders/list` добавлены флаги `cart` и `delivery_address` 
* Флаг `include_refund` добавлен в запросы `/internal/v1/get-orders/list` и `/v1/get-orders`, отвечает за то, будут ли в корзину (`cart`) включены позиции удаленные из заказа
* В корзине появляются поля `original_quantity` и `original_total_amount`, отражающие первоначальное состояние. И `quantity` и `total_amount` — финальное состояние. Соответственно для добавленных `original_*` == 0, а для удаленных `original_*` > 0 и финальные == 0
* В респонсы обеих ручек добавлены поля: `shipping_type`, `delivery_type`, `order_type`, `currency`, `original_total_amount`, `last_revision_id` для корзины: `measure_unit`, `weight`, `original_quantity`, `cost_for_customer`, `refunded_amount`, `parent_origin_id`, `stand_alone_parent_origin_id` (не для всех позиций есть `origin_id`, например соус для пиццы)

```
paths:
    /v2/get-orders:
        post:
            description: |
                Возвращает коллекцию «последних» заказов пользователя.
                Последние заказы можно выбирать или за последние `days` дней
                или просто последние `orders` заказов.
                Если в объекте запроса указаны оба параметра,
                то будут возвращены не больше `orders` заказов из заказов за
                последние `days`.
                Если `days` и `orders` отсутсвуют, будут возвращены все
                имеющиеся заказы пользователя.
                Заказы выбираются в обратном хронологическом порядке
                по времени создания заказа (`created_at`).
                В объектое запроса может присутствовать один и только один из
                следующих ключей - `eats_user_id`, `taxi_user_id`, `yandex_uid`.
                Вместе с `yandex_uid` может быть передан дополнительно
                `bound_uids` со списком связанных фонишей.
            requestBody:
                required: true
                content:
                    'application/json':
                        schema:type: object
                            description: get orders request
                            additionalProperties: false
                            properties:
                                eats_user_id:
                                    description: идентификатор пользователя я.еда
                                    type: integer
                                    format: int32
                                taxi_user_id:
                                    description: идентификатор пользователя я.такси
                                    type: string
                                yandex_uid:
                                    description: идентификатор пользователя я.паспорт
                                    type: string
                                bound_uids:
                                    description: идентификаторы связанных пользователей я.паспорт
                                    type: array
                                    items:
                                        type: string
                                sources:
                                    description: источник заказов
                                    type: array
                                    items:
                                        description: источник заказа
                                        type: string
                                        enum:
                                          - eda
                                          - lavka
                                          - pharmacy
                                days:
                                    description: количество дней за которое возвращается история заказов
                                    type: integer
                                    format: int32
                                orders:
                                    description: количество заказов которое необходимо вернуть
                                    type: integer
                                    format: int32
                                cart:
                                    description: флаг, должны ли заказы содержать корзины
                                    default: false
                                    type: boolean
+                               include_refund:
+                                   description: флаг, включать ли в корзину возвраты
+                                   default: false
+                                   type: boolean
                                delivery_address:
                                    description: флаг, должны ли заказы содержать адреса
                                    default: false
                                    type: boolean
                        examples:
                            eats-user:
                                summary: по идентификатору в еде, за последние 5 дней,
                                    для еды и лавки
                                value:
                                    eats_user_id: 12456
                                    sources:
                                      - eda
                                      - lavka
                                    days: 5
                            taxi-user:
                                summary: по идентификатору в такси, только заказы
                                    лавки, все заказы
                                value:
                                    taxi_user_id: "12456"
                                    sources:
                                      - lavka
                            ya-user:
                                summary: по yandex uid, только заказы еда, за последние
                                    7 дней, но не больше 20 заказов
                                value:
                                    yandex_uid: "12456"
                                    bound_uids: ["123", "456"]
                                    sources:
                                      - eda
                                    days: 7
                                    orders: 20
            responses:
                "200":
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/GetOrdersResponse'
                "400":
                    description: Неверный запрос
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/Error'
    /internal/v2/get-orders/list:
        post:
            description: |
                Возвращает список заказов.
                Пустые фильтры -> возвращает все заказы.
                Заказы выбираются в обратном хронологическом порядке
                по времени создания заказа (`created_at`).
            requestBody:
                required: true
                content:
                    'application/json':
                        schema:
                            type: object
                            additionalProperties: false
                            properties:
                                filters:
                                    type: object
                                    description: Запрос на получение заказов
                                    additionalProperties: false
                                    properties:
                                        order_ids:
                                            description: список идентификаторов заказов
                                            type: array
                                            items:
                                                type: string
                                        place_ids:
                                            description: список идентификаторов ресторанов
                                            type: array
                                            items:
                                                type: integer
                                                format: int64
                                        statuses:
                                            description: статусы заказов
                                            type: array
                                            items:
                                                type: string
                                                enum:
                                                  - in_progress
                                                  - cancelled
                                                  - delivered
-                                       flow_types:
-                                           description: флоу заказов
-                                           type: array
-                                           items:
-                                               $ref: "#/components/schemas/FlowType"
+                                       shipping_type:
+                                           description: тип доставки (курьерская/самовывоз)
+                                           type: string
+                                           enum:
+                                             - pickup
+                                             - delivery
                                        period:
                                            $ref: "#/components/schemas/Period"
                                        pagination:
                                            $ref: "#/components/schemas/Pagination"
                                projection:
                                    type: array
                                    items:
                                        type: string
                                        enum:
                                          - delivered_at
                                          - cancel_reason
                                          - feedback
                                          - cart
                                          - delivery_address
+                                         - include_refund
                            required:
                              - filters
            responses:
                "200":
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/GetOrdersResponse'
```

```
GetOrdersResponse:
    type: object
    additionalProperties: false
    description: обёртка для коллекции заказов
    required:
    - orders
    properties:
    orders:
    type: array
    items:
        Order:
        type: object
        additionalProperties: false
        description: объект заказа 
        required:
          - order_id
          - place_id
          - status
          - source
          - delivery_location
          - total_amount
          - is_asap
          - created_at
        properties:
            order_id:
                description: идентификатор заказа
                type: string
            place_id:
                description: идентификатор ресторана
                type: integer
                format: int32
            status:
                description: статус заказа
                type: string
                enum:
                  - created 
                  - cancelled
                  - delivered
+                 - payed
+                 - confirmed
+                 - taken
+                 - promise_changed
+                 - ready_to_send
            source:
                description: источник заказа
                type: string
                enum:
                  - eda
                  - lavka
                  - pharmacy
            delivery_location:
                type: object
                additionalProperties: false
                description: объект для хранения гео-координат места получения заказа
                properties:
                    lat:
                        description: latitude
                        type: number
                        minimum: -90
                        maximum: 90
                    lon:
                        description: longtitude
                        type: number
                        minimum: -180
                        maximum: 180
                required:
                  - lon
                  - lat
                x-taxi-cpp-type: geometry::PositionAsObject
            total_amount:
                description: суммарная стоимость
                type: string
            is_asap:
                description: признак того, что заказ нужно привести к конкретному
                    времени
                type: boolean
            created_at:
                description: время создания заказа
                type: string
                format: date-time
                example: "2020-04-28T12:00:00+03:00"
            delivered_at:
                description: время вручения заказа клиенту
                type: string
                format: date-time
                example: "2020-04-28T12:00:00+03:00"
            cancel_reason:
                description: код причины отмены заказа
                type: string
            feedback:
                type: object
                additionalProperties: false
                description: объект для хранения отзыва покупателя о заказе (оба поля
                    могут быть необязательными?)
                properties:
                    rating:
                        description: пользовательская оценка заказ (от 1 до 5)
                        type: integer
                        format: int32
                    comment:
                        description: комментарий к заказу
                        type: string
            cart:
                description: коллекция заказанных пользователем товаров
                type: array
                items:
                    type: object
                    additionalProperties: false
                    description: товарная позиция в корзине пользователя
                    properties:
-                       place_menu_item_id:
-                           description: идентификатор товара в меню ресторана
-                           type: integer
-                           format: int32
-                       product_id:
-                           description: идентификатор товара
-                           type: string
                        name:
                            description: название товара, например «картошка»
                            type: string
                        quantity:
                            description: количество товаров в рамках этой позиции
                            type: integer
                            format: int32
                        catalog_type:
                            description: тип каталога, к которому относится позиция
                            type: string
                            enum:
                              - core_catalog
                              - lavka_catalog
                              - eats_nomenclature
                              - eats_restaurant_nomenclature
                        origin_id:
                            description: идентификатор внутри каталога
                            type: string
+                       parent_origin_id:
+                           description: Идентификатор родительского продукта
+                           type: string
+                       measure_unit:
+                           description: Единицы измерения веса, например GRM
+                           type: string
+                       weight:
+                           description: Вес
+                           type: number
+                       original_quantity:
+                           description: Количество/вес в изначальном заказе
+                           type: int32                                                                
+                       cost_for_customer:
+                           description: Итоговая цена c копейками
+                           type: string
+                           x-taxi-cpp-type: decimal64::Dec
+                           pattern: '^[0-9]+(\.[0-9]{1,2})
+                           example: '"123456.78"'
+                           description: Цена c копейками
+                       refunded_amount:
+                           description: Возврат, цена c копейками
+                           type: string
+                           x-taxi-cpp-type: decimal64::Decimal<2>
+                           pattern: '^[0-9]+(\.[0-9]{1,2})?$'
+                           example: '"123456.78"'
+                           description: Цена c копейками
+                       stand_alone_parent_origin_id:
+                           type: string
+                           description: origin_id родительского продукта для меню с подменой комбо-блюд (из ревизий)
                    required:
                      - name
                      - quantity
            delivery_address:
                type: object
                additionalProperties: false
                description: объект для хранения адреса места получения заказа
                properties:
                    full_address:
                        description: адрес
                        type: string
                        example: "Россия, Москва, Садовническая ул, 81к1"
                    entrance:
                        description: номер подъезда
                        type: string
                    floor:
                        description: этаж
                        type: string
                    office:
                        description: квартира
                        type: string
                    doorcode:
                        description: код домофона
                        type: string
                    comment:
                        description: комментарий
                        type: string
-           flow_type:
-               description: флоу заказа
-               type: string
-               enum:
-                 - native
-                 - burger_king
-                 - pickup
-                 - pharmacy
-                 - shop
-                 - retail
-                 - fuelfood
+           shipping_type:
+               description: тип доставки (курьерская/самовывоз)
+               type: string
+               enum:
+                 - pickup
+                 - delivery
+           delivery_type:
+               description: чья доставка (наша/маркетплейс)
+               type: string
+               enum: 
+                 - native
+                 - marketplace
+           order_type:
+               enum:
+                 - native
+                 - retail
+                 - shop
+                 - lavka
+                 - pharmacy
+                 - fast_food
+                 - fuel_food
+           currency:
+               description: Валюта
+               type: string
+           original_total_amount:
+               description: изначальная суммарная стоимость
+               type: string
```

#### Изменения в базе:
```
orders:
    order_id                text,
-   order_source            enum [eda, lavka, pharmacy],
+   order_type              enum [native, retail, shop, lavka, pharmacy, fast_food, fuel_food],
    eats_user_id            int,
    taxi_user_id            text,
    yandex_uid              text,
    place_id                int,
-   status                  text,
+   status                  enum [created, payed, confirmed, taken, finished, cancelled, promise_changed, ready_to_send],
    delivery_location       point,
    total_amount            text,
+   original_total_amount   text,
+   currency                text,
    is_asap                 bool,
    cancel_reason           text,
    created_at              timestamptz,
    delivered_at            timestamptz,
-   flow_type               enum [native, burger_king, pickup, pharmacy, shop, retail, fuelfood],
+   shipping_type           enum [pickup, delivery],
+   delivery_type           enum [native, marketplace],
+   last_revision_id        text
```
`currency`, `total_amount` (конечная стоимость) и `original_total_amount` (начальная стоимость) будем получать из eats-orders-revision, остальное из procaas через logbroker

```
cart_items:
    order_id                        text,
-   place_menu_item_id              int,
-   product_id                      text,
    name                            text,
+   original_quantity               int,
    quantity                        int,
+   measure_unit                    text,
+   weight                          double precision,
    origin_id                       text,
+   parent_origin_id                text,
    catalog_type                    enum [core_catalog, lavka_catalog, eats_nomenclature, eats_restaurant_nomenclature],
+   cost_for_customer               decimal (13, 2),
+   refunded_amount                 decimal (13, 2)
+   stand_alone_parent_origin_id    text,
```
Все необходимы данные для корзины будем получать из eats-orders-revision, `place_menu_item_id` там отсутствует
