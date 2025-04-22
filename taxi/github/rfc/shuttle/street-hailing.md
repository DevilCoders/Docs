# Заказы от борта в шаттле

## Идея

Концептуально заказы от борта работают так: за N метров до остановки на маршруте у водителя
показывается кнопка, по нажатию на которую отображается список остановок и цены, сколько будет
стоить доехать до них. Пользователь, который хочется сесть "от борта" просит водителя доехать
до определенной остановки и называет сколько человек поедет. Водитель в это время на своем экране 
делает выбор, берет деньги и называет коды-билетики, присвоенные этим пассажирам. После этого
пользователям гарантируются места в машине.

Дизайн по фигме: https://www.figma.com/file/0MWKdgXKqVcuznXg73I8Um/3-·-Pro-·-Order?node-id=7%3A557

## Экран выбора остановок

За N метров у водителя в Pro появится кнопка открытия окна со всеми остановками впереди, с информацией
сколько будет стоить доехать до них (какая-то приблизительная цена), и также 
сколько мест свободно на них.

```
/driver/v1/shuttle-control/v1/street_hailing/stops_ahead:
        x-generator-tags:
          - android-client
        get:
            description: Get ahead stops info for street hailing
            operationId: get_stops_ahead
            tags:
              - shuttle_pro_api
            parameters:
              - name: Accept-Language
                description: Предпочитаемый язык ответа
                in: header
                schema:
                    type: string
                required: true
              - name: User-Agent
                in: header
                schema:
                    type: string
                required: true
              - name: shuttle_id
                in: query
                required: true
                schema:
                    type: string
            responses:
                200:
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/V1StopsAheadResponse'
                400:
                    description: No such shuttle or shuttle is already ended
                    content:
                        application/json:
                            schema:
                                $ref: 'shuttle-control/definitions.yaml#/components/schemas/Error'

components:
    schemas:
        V1StopsAheadResponse:
            type: object
            additionalProperties: false
            properties:
                route_name:
                    type: string
                stops:
                    type: array
                    items:
                        type: object
                        additionalProperties: false
                        properties:
                            hint:
                                type: object
                                additionalProperties: false
                                properties:
                                    title:
                                        example: 40 рублей | Нет мест
                                        type: string
                                    subtitle:
                                        example: 3 места
                                        type: string
                                required:
                                  - title
                            num_passengers:
                                type: integer
                                minimum: 0
                            stop_name:
                                type: string
                            stop_id:
                                type: string
                        required:
                          - hint
                          - num_passengers
                          - stop_name
                          - stop_id
            required:
              - route_name
              - stops
```

## Выбор числа мест

При нажатии на определенное число мест на экране с остановками происходит запрос на бэк,
в котором происходит валидация возможности доехать до нужной остановки. В случае успеха отдается
оффер заказа и его точная цена. Места при этом не замораживаются за пассажирами.

```
/driver/v1/shuttle-control/v1/street_hailing/create_offer:
        x-generator-tags:
          - android-client
        post:
            description: Create booking offer via street hails
            operationId: create_street_hail_offer
            tags:
              - shuttle_pro_api
            parameters:
              - name: Accept-Language
                description: Предпочитаемый язык ответа
                in: header
                schema:
                    type: string
                required: true
              - name: User-Agent
                in: header
                schema:
                    type: string
                required: true
              - name: shuttle_id
                in: query
                required: true
                schema:
                    type: string
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/V1CreateOfferRequest'
            responses:
                200:
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/V1CreateOfferResponse'
                400:
                    description: Potential booking is not available now
                    content:
                        application/json:
                            schema:
                                $ref: 'shuttle-control/definitions.yaml#/components/schemas/Error'

components:
    schemas:
        V1CreateOfferRequest:
            type: object
            additionalProperties: false
            properties:
                dropoff_stop_id:
                    type: string
                num_passengers:
                    type: integer
                    minimum: 1
                    default: 1
            required:
              - dropoff_stop_id

        V1CreateOfferResponse:
            type: object
            additionalProperties: false
            properties:
                items:
                    type: array
                    items:
                        type: object
                        additionalProperties: true
                        x-taxi-additional-properties-true-reason: конструктор для таксометра
                        x-custom-type: ru.yandex.taximeter.data.api.uiconstructor.ComponentListItemResponse
                        description: constructor ui elements
                offer_id:
                    type: string
            required:
              - items
              - offer_id
```

## Подтверждение бронирования

Если пользователь согласен на цену поездки, водитель нажимает кнопку брони, и если не прошло много 
времени и выданный оффер еще валидный, то бронирование подтверждается на бэкенде (200 ОК),
возвращается итоговая цена и билетики, которые нужно сказать пассажирам 
(по сути их идентификатор внутри шаттла).
Иначе, возвращается 400 с текстом ошибки.

```
/driver/v1/shuttle-control/v1/street_hailing/commit_booking:
        x-generator-tags:
          - android-client
        post:
            description: Confirm driver booking via street hails
            operationId: confirm_street_hail_booking
            tags:
              - shuttle_pro_api
            parameters:
              - name: Accept-Language
                description: Предпочитаемый язык ответа
                in: header
                schema:
                    type: string
                required: true
              - name: User-Agent
                in: header
                schema:
                    type: string
                required: true
              - name: shuttle_id
                in: query
                required: true
                schema:
                    type: string
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/V1CommitBookingRequest'
            responses:
                200:
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/V1CommitBookingResponse'
                400:
                    description: Malformed offer_id or offer became stale
                    content:
                        application/json:
                            schema:
                                $ref: 'shuttle-control/definitions.yaml#/components/schemas/Error'

components:
    schemas:
        V1CommitBookingRequest:
            type: object
            additionalProperties: false
            properties:
                offer_id:
                    type: string
            required:
              - offer_id

        V1CommitBookingResponse:
            type: object
            additionalProperties: false
            properties:
                tickets:
                    type: array
                    items:
                        type: string
                    minItems: 1
                items:
                    type: array
                    items:
                        type: object
                        additionalProperties: true
                        x-taxi-additional-properties-true-reason: конструктор для таксометра
                        x-custom-type: ru.yandex.taximeter.data.api.uiconstructor.ComponentListItemResponse
                        description: constructor ui elements
                    minItems: 0
            required:
              - tickets
              - items
```
