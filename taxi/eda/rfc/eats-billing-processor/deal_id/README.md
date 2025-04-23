# Токенизация сделки (проверка корректности данных партнера)
## Проблемы:
1. Есть контрагенты, у которых невалдиные биллинговые данные. Это приводит к тому, что мы не можем им сделать выплату.
2. Есть много данных, которые нужно пробрасывать через разные события. Если добавлять что-нибудь ещё, то нужно изменять несколько сервисов по цепочке.

## Решение:

1. Получение deal_id (токена сделки) как можно раньше в жизненном цикле заказа. 
Невозможность его получения говорит о том, что заказ нельзя выполнить (так как с невалидными контрагентами не можем расплатиться).

2. Прокидывание deal_id через события в новом формате (ручка v2/create сервиса eats-billing-processor).

## Что нужно для перехода

1. Проверить что события в новом формате имеют все необходимые данные (клиент, eats-billing-processor);
2. Перейти на новый флоу работы, закрыв экспериментом (клиент);
3. Корректно обрабатывать ситуацию отсутствия deal_id для контрагента (отмена заказа или другой сценарий);
4. Сделать конвертацию необходимого списка событий в новый формат (eats-billing-processor);
5. Включить конвертацию (eats-billing-processor). Не влияет на клиента, нужно для проверки корректности обработки событий в новом формате и выявление недочетов;
6. Переход на новый флоу (посредством эксперимента).

Рестораны/магазины:
1. Проверка партнера на этапе создания заказа (не даем создать заказ);
2. Проверка партнера при изменении ресторана, обновление deal_id (отмена в случае не успеха).

Курьеры/сборщики:
На этапе формирования событиий в биллинг, проверять валидность контрагента, если невалидный, отменяем заказ.


## Затрагиваемые сервисы:

### Чек заказы (qr-pay, inplace, b2b)
(eats-integration-offline-orders, eats-corp-orders)

### lavka
(grocery-payments-billing)

### Помощь рядом
(persey-payments)

### Все заказы еды
(eda-core, eats-payments-billing, eats-order-revision, eats-orders-billing, eats-place-subscriptions)

## Изменение в API:

В текущей реализации сервисы потребители ходят в ручку /v1/create (eats-billing-processor)

В новой схеме должно быть так: 
Сервис потребитель ходит в /v1/deal_id (eats-billing-processor), получает токен (deal_id), 
обогощает событие полученным токеном (токенами) и формирует события в новом формате /v2/create (eats-billing-processor)

![Client_scheme](./deal_id_sequence_diagram.png)

### /v1/deal_id

```
openapi: 3.0.0
info:
    description: Yandex Taxi eats-billing-processor Service
    title: Yandex Taxi eats-billing-processor Service
    version: '1.0'

# Not used in codegen
servers:
  - url: eats-billing-processor.eda.yandex.net
    description: production

x-taxi-middlewares:
    tvm: true


x-taxi-client-qos:
    taxi-config: EATS_BILLING_PROCESSOR_CLIENT_QOS

paths:
    /v1/deal_id:
        post:
            description: Получение токена биллинга заказа
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/DealIdRequest'
            responses:
                '200':
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/DealIdResponse'
                '400':
                    $ref: '../definitions/error_responses.yaml#/components/responses/BadRequest'
                '404':
                    $ref: '../definitions/error_responses.yaml#/components/responses/NotFound'
                '500':
                    $ref: '../definitions/error_responses.yaml#/components/responses/InternalError'

components:
    schemas:
        DealIdRequest:
            oneOf:
              - $ref: '#/components/schemas/Place'
              - $ref: '#/components/schemas/Picker'
              - $ref: '#/components/schemas/Courier'
              - $ref: '#/components/schemas/Donation'
              - $ref: '#/components/schemas/ServiceFee'
            discriminator:
                propertyName: counterparty_type
                mapping:
                    'place': '#/components/schemas/Place'
                    'picker': '#/components/schemas/Picker'
                    'courier': '#/components/schemas/Courier'
                    'donation': '#/components/schemas/Donation'
                    'service_fee': '#/components/schemas/ServiceFee'

        DealIdCommon:
            type: object
            additionalProperties: true
            x-taxi-additional-properties-true-reason: Требование валидатора для allOf
            required:
              - counterparty_id
              - order_nr
              - place_type
              - delivery_type
              - timestamp
            properties:
                counterparty_id:
                    description: Идентификатор клиента
                    type: string
                order_nr:
                    description: Номер заказа
                    type: string
                place_type:
                    description: Тип места
                    type: string
                    enum:
                      - restaurant
                      - shop
                      - grocery
                delivery_type:
                    description: Тип доставки
                    type: string
                    enum:
                      - native
                      - place
                      - pickup
                      - inplace
                assembly_type:
                    description: Тип сборки
                    type: string
                    enum:
                      - native
                      - place
                timestamp:
                    description: Время
                    $ref: '../definitions/common_types.yaml#/components/schemas/DateTime'

        Picker:
            allOf:
              - $ref: '#/components/schemas/DealIdCommon'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - counterparty_type
                properties:
                    counterparty_type:
                        description: Тип
                        type: string
                        enum:
                          - picker

        Courier:
            allOf:
              - $ref: '#/components/schemas/DealIdCommon'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - counterparty_type
                properties:
                    counterparty_type:
                        description: Тип
                        type: string
                        enum:
                          - courier

        Place:
            allOf:
              - $ref: '#/components/schemas/DealIdCommon'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - counterparty_type
                properties:
                    counterparty_type:
                        description: Тип
                        type: string
                        enum:
                          - place

        Donation:
            allOf:
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - counterparty_type
                  - order_nr
                  - currency
                  - timestamp
                properties:
                    counterparty_type:
                        description: Тип
                        type: string
                        enum:
                          - donation
                    order_nr:
                        description: Номер заказа
                        type: string
                    currency:
                        description: Валюта
                        type: string
                    timestamp:
                        description: Время
                        $ref: '../definitions/common_types.yaml#/components/schemas/DateTime'

        ServiceFee:
            allOf:
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - counterparty_type
                  - order_nr
                  - currency
                  - timestamp
                  - place_type
                  - delivery_type
                properties:
                    counterparty_type:
                        description: Тип
                        type: string
                        enum:
                          - service_fee
                    order_nr:
                        description: Номер заказа
                        type: string
                    currency:
                        description: Валюта
                        type: string
                    timestamp:
                        description: Время
                        $ref: '../definitions/common_types.yaml#/components/schemas/DateTime'
                    place_type:
                        description: Тип места
                        type: string
                        enum:
                          - restaurant
                          - shop
                          - grocery
                    delivery_type:
                        description: Тип доставки
                        type: string
                        enum:
                          - native
                          - place
                          - pickup
                          - inplace
                    assembly_type:
                        description: Тип сборки
                        type: string
                        enum:
                          - native
                          - place

        DealIdResponse:
            type: object
            additionalProperties: false
            required:
              - deal_id
            properties:
                deal_id:
                    description: Токен
                    type: string

```

### /v2/create

**В текущей реализации не учтена часть событий и поля к имеющимся (в разработке)**

```
openapi: 3.0.0
info:
    description: Yandex Taxi eats-billing-processor Service
    title: Yandex Taxi eats-billing-processor Service
    version: '1.0'

# Not used in codegen
servers:
  - url: eats-billing-processor.eda.yandex.net
    description: production

x-taxi-middlewares:
    tvm: true


x-taxi-client-qos:
    taxi-config: EATS_BILLING_PROCESSOR_CLIENT_QOS

paths:
    /v1/create:
        post:
            description: Создать входное событие
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/CreateRequest'
            responses:
                '200':
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/CreateResponse'
                '400':
                    $ref: '../definitions/error_responses.yaml#/components/responses/BadRequest'
                '500':
                    $ref: '../definitions/error_responses.yaml#/components/responses/InternalError'

    /v2/create:
        post:
            description: Создать входное событие
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/CreateRequestV2'
            responses:
                '200':
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/CreateResponse'
                '400':
                    $ref: '../definitions/error_responses.yaml#/components/responses/BadRequest'
                '500':
                    $ref: '../definitions/error_responses.yaml#/components/responses/InternalError'

components:
    schemas:
        CreateRequestData:
            $ref: '../definitions/input_events.yaml#/components/schemas/AllEvents'

        CreateRequest:
            type: object
            additionalProperties: false
            required:
              - order_nr
              - external_id
              - event_at
              - kind
              - data
            properties:
                order_nr:
                    description: Номер заказа
                    type: string
                external_id:
                    description: Внешний уникальный идентификатор события
                    type: string
                event_at:
                    description: Время создания события
                    $ref: '../definitions/common_types.yaml#/components/schemas/DateTime'
                kind:
                    description: Тип события
                    $ref: '../definitions/common_types.yaml#/components/schemas/EventKind'
                data:
                    description: Данные события
                    $ref: '#/components/schemas/CreateRequestData'
                rule_name:
                    $ref: '../definitions/rule_name.yaml#/components/schemas/RuleName'

        CreateRequestV2:
            type: object
            additionalProperties: false
            required:
              - order_nr
              - external_id
              - event_at
              - data
            properties:
                order_nr:
                    description: Номер заказа
                    type: string
                external_id:
                    description: Внешний уникальный идентификатор события
                    type: string
                event_at:
                    description: Время создания события
                    $ref: '../definitions/common_types.yaml#/components/schemas/DateTime'
                data:
                    description: Данные события
                    $ref: '../definitions/input_events_v2.yaml#/components/schemas/AllEventsV2'

        CreateResponse:
            type: object
            additionalProperties: false
            required:
              - event_id
            properties:
                event_id:
                    description: Уникальный идентификатор события в базе данных
                    type: string
```

**Событие PaymentUpdateV2 разобьем на два события (payment_received, payment_refund)**


### ../definitions/input_events_v2.yaml#/components/schemas/AllEventsV2

```
components:
    schemas:
        InputEventV2:
            description: Общая часть входного события
            type: object
            additionalProperties: true
            x-taxi-additional-properties-true-reason: Требование валидатора для allOf
            required:
              - order_nr
              - event_at
            properties:
                order_nr:
                    description: Номер заказа
                    type: string
                event_at:
                    description: Время создания события
                    $ref: 'common_types.yaml#/components/schemas/DateTime'
                payload:
                    description: Дополнительная информация
                    type: object
                    additionalProperties: true
                    x-taxi-additional-properties-true-reason: Произвольные данные

        InputEventProducts:
            description: Список продуктов/услуг и скидок
            type: array
            items:
                type: object
                additionalProperties: false
                required:
                  - token
                  - amount
                  - product_type
                  - payment_type
                  - discounts
                properties:
                    token:
                        description: Токен партнера
                        type: string
                    transaction_date:
                        description: Дата проведения транзакции
                        $ref: 'common_types.yaml#/components/schemas/DateTime'
                    amount:
                        description: Стоимость продукта/услуги
                        $ref: 'amount_type.yaml#/definitions/AmountType'
                    product_type:
                        description: Тип продукта/услуги
                        $ref: 'product_type.yaml#/definitions/ProductType'
                    payment_type:
                        description: Способ оплаты
                        $ref: 'payment_type.yaml#/definitions/PaymentType'
                    discounts:
                        description: Список примененных скидок
                        type: array
                        items:
                            type: object
                            additionalProperties: false
                            required:
                              - amount
                              - discount_type
                            properties:
                                amount:
                                    description: Сумма скидки
                                    $ref: 'amount_type.yaml#/definitions/AmountType'
                                discount_type:
                                    description: Тип промокода
                                    $ref: 'discount_type.yaml#/components/schemas/DiscountType'

        InputEventFees:
            description: Сборы в пользу Еды
            type: array
            items:
                type: object
                additionalProperties: false
                required:
                  - token
                  - amount
                  - fee_type
                properties:
                    token:
                        description: Токен партнера
                        type: string
                    transaction_date:
                        description: Дата проведения транзакции
                        $ref: 'common_types.yaml#/components/schemas/DateTime'
                    amount:
                        description: Стоимость продукта/услуги
                        $ref: 'amount_type.yaml#/definitions/AmountType'
                    fee_type:
                        description: Тип сбора
                        $ref: 'fee_type.yaml#/components/schemas/FeeType'

        PaymentUpdateV2:
            description: Обновление данных по платежу
            allOf:
              - $ref: '#/components/schemas/InputEventV2'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - kind
                  - version
                  - transaction_date
                  - token
                  - currency
                  - amount
                  - product_type
                  - payment_type
                properties:
                    kind:
                        description: Тип события
                        type: string
                        enum:
                          - payment_update
                    version:
                        description: Версия события
                        type: string
                        enum:
                          - v2.0
                    transaction_date:
                        description: Дата проведения транзакции
                        $ref: 'common_types.yaml#/components/schemas/DateTime'
                    token:
                        description: Токен партнера
                        type: string
                    currency:
                        description: Валюта транзакции
                        type: string
                    amount:
                        description: Сумма транзакции
                        $ref: 'amount_type.yaml#/definitions/AmountType'
                    product_type:
                        description: Тип продукта/услуги
                        $ref: 'product_type.yaml#/definitions/ProductType'
                    payment_type:
                        description: Способ оплаты
                        $ref: 'payment_type.yaml#/definitions/PaymentType'
                    payment_terminal_id:
                        description: Платежный терминал
                        type: string
                    external_payment_id:
                        description: Уникальный идентификатор платежа
                        type: string
                    payment_service:
                        description: Тип платежного сервиса
                        type: string

        PaymentNotReceivedV2:
            description: Не удалось списать деньги
            allOf:
              - $ref: '#/components/schemas/InputEventV2'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - kind
                  - version
                  - transaction_date
                  - token
                  - currency
                  - amount
                  - product_type
                  - payment_type
                properties:
                    kind:
                        description: Тип события
                        type: string
                        enum:
                          - payment_not_received
                    version:
                        description: Версия события
                        type: string
                        enum:
                          - v2.0
                    transaction_date:
                        description: Дата проведения транзакции
                        $ref: 'common_types.yaml#/components/schemas/DateTime'
                    token:
                        description: Токен партнера
                        type: string
                    currency:
                        description: Валюта транзакции
                        type: string
                    amount:
                        description: Сумма транзакции
                        $ref: 'amount_type.yaml#/definitions/AmountType'
                    product_type:
                        description: Тип продукта/услуги
                        $ref: 'product_type.yaml#/definitions/ProductType'
                    payment_type:
                        description: Способ оплаты
                        $ref: 'payment_type.yaml#/definitions/PaymentType'
                    payment_terminal_id:
                        description: Платежный терминал
                        type: string
                    external_payment_id:
                        description: Уникальный идентификатор платежа
                        type: string

        PlusCashbackEmissionV2:
            description: Начисление пользователю баллов Я.Плюс
            allOf:
              - $ref: '#/components/schemas/InputEventV2'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - kind
                  - version
                  - transaction_date
                  - currency
                  - amount
                  - amounts_per_counterparty
                properties:
                    kind:
                        description: Тип события
                        type: string
                        enum:
                          - plus_cashback_emission
                    version:
                        description: Версия события
                        type: string
                        enum:
                          - v2.0
                    transaction_date:
                        description: Дата проведения транзакции
                        $ref: 'common_types.yaml#/components/schemas/DateTime'
                    currency:
                        description: Валюта начисления
                        type: string
                    amount:
                        description: Сумма начисления
                        $ref: 'amount_type.yaml#/definitions/AmountType'
                    amounts_per_counterparty:
                        description: Сумма за счет партнера
                        type: array
                        items:
                            type: object
                            additionalProperties: false
                            required:
                              - token
                              - amount
                            properties:
                                token:
                                    description: Токен партнера
                                    type: string
                                amount:
                                    description: Сумма компенсации
                                    $ref: 'amount_type.yaml#/definitions/AmountType'

        OrderCancelledV2:
            description: Заказ отменен
            allOf:
              - $ref: '#/components/schemas/InputEventV2'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - kind
                  - version
                  - transaction_date
                  - is_payment_expected
                  - is_reimbursement_required
                  - is_place_fault
                  - reason_id
                  - currency
                  - products
                  - fees
                properties:
                    kind:
                        description: Тип события
                        type: string
                        enum:
                          - order_cancelled
                    version:
                        description: Версия события
                        type: string
                        enum:
                          - v2.0
                    transaction_date:
                        description: Дата проведения транзакции
                        $ref: 'common_types.yaml#/components/schemas/DateTime'
                    is_payment_expected:
                        description: Признак ожидания платежей по заказу
                        type: boolean
                    is_reimbursement_required:
                        description: Признак необходимости компенсировать затраты
                        type: boolean
                    is_place_fault:
                        description: Признак отмены по вине ресторана
                        type: boolean
                    reason_id:
                        description: Идентификатор причины отмены
                        type: string
                    currency:
                        description: Валюта
                        type: string
                    products:
                        $ref: '#/components/schemas/InputEventProducts'
                    fees:
                        $ref: '#/components/schemas/InputEventFees'
                    gmv_amount:
                        description: Сумма GMV
                        $ref: 'amount_type.yaml#/definitions/AmountType'
                    dynamic_price:
                        description: Динамическая наценка
                        $ref: 'amount_type.yaml#/definitions/AmountType'

        OrderDeliveredV2:
            description: Заказ доставлен
            allOf:
              - $ref: '#/components/schemas/InputEventV2'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - kind
                  - version
                  - transaction_date
                  - currency
                  - products
                  - fees
                properties:
                    kind:
                        description: Тип события
                        type: string
                        enum:
                          - order_delivered
                    version:
                        description: Версия события
                        type: string
                        enum:
                          - v2.0
                    transaction_date:
                        description: Дата проведения транзакции
                        $ref: 'common_types.yaml#/components/schemas/DateTime'
                    currency:
                        description: Валюта
                        type: string
                    products:
                        $ref: '#/components/schemas/InputEventProducts'
                    fees:
                        $ref: '#/components/schemas/InputEventFees'

        OrderGmvV2:
            description: Совокупный оборот по заказу
            allOf:
              - $ref: '#/components/schemas/InputEventV2'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - kind
                  - version
                  - transaction_date
                  - token
                  - currency
                  - amount
                properties:
                    kind:
                        description: Тип события
                        type: string
                        enum:
                          - order_gmv
                    version:
                        description: Версия события
                        type: string
                        enum:
                          - v2.0
                    transaction_date:
                        description: Дата проведения транзакции
                        $ref: 'common_types.yaml#/components/schemas/DateTime'
                    token:
                        description: Токен партнера
                        type: string
                    currency:
                        description: Валюта
                        type: string
                    amount:
                        description: Сумма GMV
                        $ref: 'amount_type.yaml#/definitions/AmountType'
                    special_commission_type:
                        description: Дополнительная специальная комиссия
                        $ref: 'special_commission_type.yaml#/definitions/SpecialCommissionType'
                    dynamic_price:
                        description: Динамическая наценка
                        $ref: 'amount_type.yaml#/definitions/AmountType'

        ReceiptV2:
            description: Данные чека
            allOf:
              - $ref: '#/components/schemas/InputEventV2'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - kind
                  - version
                  - transaction_date
                  - token
                  - currency
                  - amount
                  - operation_type
                  - fiscal_drive_number
                  - fiscal_document_number
                  - fiscal_sign
                properties:
                    kind:
                        description: Тип события
                        type: string
                        enum:
                          - receipt
                    version:
                        description: Версия события
                        type: string
                        enum:
                          - v2.0
                    transaction_date:
                        description: Дата проведения транзакции
                        $ref: 'common_types.yaml#/components/schemas/DateTime'
                    token:
                        description: Токен партнера
                        type: string
                    currency:
                        description: Валюта
                        type: string
                    amount:
                        description: Сумма GMV
                        $ref: 'amount_type.yaml#/definitions/AmountType'
                    operation_type:
                        description: Тип операции
                        type: string
                        enum:
                          - income
                          - expense
                          - income_refund
                          - expense_refund
                    fiscal_drive_number:
                        description: Фискальный номер
                        type: string
                    fiscal_document_number:
                        description: Фискальный номер документа
                        type: integer
                    fiscal_sign:
                        description: Подпись
                        type: string

        CompensationV2:
            description: Выплата компенсаций
            allOf:
              - $ref: '#/components/schemas/InputEventV2'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: Требование валидатора для
                    allOf
                required:
                  - kind
                  - version
                  - transaction_date
                  - reason_id
                  - currency
                  - products
                  - fees
                properties:
                    kind:
                        description: Тип события
                        type: string
                        enum:
                          - compensation
                    version:
                        description: Версия события
                        type: string
                        enum:
                          - v2.0
                    transaction_date:
                        description: Дата проведения транзакции
                        $ref: 'common_types.yaml#/components/schemas/DateTime'
                    reason_id:
                        description: Идентификатор причины компенсации
                        type: string
                    is_place_fault:
                        description: Признак компенсации по вине ресторана
                        type: boolean
                    currency:
                        description: Валюта
                        type: string
                    products:
                        $ref: '#/components/schemas/InputEventProducts'
                    fees:
                        $ref: '#/components/schemas/InputEventFees'

        AllEventsV2:
            oneOf:
              - $ref: '#/components/schemas/PaymentUpdateV2'
              - $ref: '#/components/schemas/PaymentNotReceivedV2'
              - $ref: '#/components/schemas/PlusCashbackEmissionV2'
              - $ref: '#/components/schemas/OrderCancelledV2'
              - $ref: '#/components/schemas/OrderDeliveredV2'
              - $ref: '#/components/schemas/OrderGmvV2'
              - $ref: '#/components/schemas/ReceiptV2'
              - $ref: '#/components/schemas/CompensationV2'
            discriminator:
                propertyName: kind
                mapping:
                    payment_update: '#/components/schemas/PaymentUpdateV2'
                    payment_not_received: '#/components/schemas/PaymentNotReceivedV2'
                    plus_cashback_emission: '#/components/schemas/PlusCashbackEmissionV2'
                    order_cancelled: '#/components/schemas/OrderCancelledV2'
                    order_delivered: '#/components/schemas/OrderDeliveredV2'
                    order_gmv: '#/components/schemas/OrderGmvV2'
                    receipt: '#/components/schemas/ReceiptV2'
                    compensation: '#/components/schemas/CompensationV2'
```