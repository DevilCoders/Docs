### Новая ручка букинга с принятием оффера

Зачем: добавляется offer_id, и почти все принимаемые параметры в текущей ручке повторяют содержимое оффера.
В новой ручке не будет дублирования, не надо будет проверять, какие поля приходят на вход и по какому алгоритму
создавать букинг.

API новой ручки:

```

/4.0/shuttle-control/v2/booking/create:
    post:
        x-taxi-middlewares:
            api-4.0: true
        description: Create shuttle booking using offer
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        $ref: '#/components/schemas/V2BookingCreateRequest'
        responses:
            200:
                description: OK
                content:
                    application/json:
                        schema:
                            $ref: 'shuttle-control/definitions.yaml#/components/schemas/V1BookingInformation'
                headers:
                    X-YaTaxi-Polling-Interval-Ms:
                        schema:
                            type: integer
                        description: Задержка до следующего запроса от клиента
            400:
                description: Bad Request
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
                            properties:
                                code:
                                    type: string
                                message:
                                    type: string
                                    description: Человекочитаемая ошибка
                                    example: Закончились места в Шаттле
                            required:
                              - code
                              - message

components:
    schemas:
        RoutePoint:
            type: object
            additionalProperties: false
            properties:
                position:
                    $ref: 'shuttle-control/definitions.yaml#/components/schemas/PositionAsArray'
                short_text:
                    type: string
                full_text:
                    type: string
                uri:
                    type: string
            required:
                - position
                - short_text
                - full_text

        V2BookingCreateRequest:
            type: object
            additionalProperties: false
            properties:
                offer_id:
                    description: Идентификатор оффера
                    type: string
                route:
                    description: Точки А и Б заказа
                    type: array
                    minItems: 2
                    maxItems: 2
                    items:
                        $ref: '#/components/schemas/RoutePoint'
                payment:
                    $ref: 'shuttle-control/definitions.yaml#/components/schemas/Payment'        
            required:
              - route
              - payment

```