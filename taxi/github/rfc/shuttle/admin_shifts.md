# Админка смен и слотов работы водителя шаттла

## Концепция

Смена работы (template-shift) - интервал времени, привязанный к одному или нескольким дням недели на одном маршруте.

Слот работы (shift) - инстанс смены, привязанный уже к конкретной дате. Несколько водителей могут выбрать 
один слот работы (не больше какого-то числа N).

Фигма: https://www.figma.com/file/dMqr3Z4vDcKvdVope4cytU/Untitled?node-id=0%3A1

## Админка смен

Для запроса городов и доступных в нем маршрутов вызывается ручка:

```

/admin/shuttle-control/v1/present-routes:
    get:
        description: Возвращает краткую информацию про существующие маршруты
        responses:
            200:
                description: OK
                content:
                    application/json:
                        schema:
                            type: array
                            items:
                                $ref: '#/components/schemas/AdminRoute'

components:
    schemas:
        AdminRoute:
            type: object
            additionalProperties: false
            properties:
                id:
                    example: bishkek.central
                    type: string
                name:
                    example: Центральный
                    type: string
                city:
                    example: Бишкек
                    type: string
            required:
                - id
                - name
                - city     

```

Для поиска вызывается ручка с выбранными фильтрами (маршрут + диапазон дат недели):

```

/admin/shuttle-control/v1/template-shifts/list:
    get:
        description: Возвращает все смены маршрута, попадающие в диапазон дат
        parameters:
            - name: route_name
              in: query
              required: true
              schema:
                type: string
            - name: date_from
              in: query
              required: true
              schema:
                type: string
                format: date-time
            - name: date_to
              in: query
              required: true
              schema:
                type: string
                format: date-time
        responses:
            200:
                description: OK
                content:
                    application/json:
                        schema:
                            type: array
                            items:
                                $ref: '#/components/schemas/AdminTemplateShift'

components:
    schemas:
        AdminTemplateShift:
            type: object
            additionalProperties: false
            properties:
                id:
                    description: internal workshift_template_id
                    type: string 
                schedule:
                    description: Объект расписаний как в скидках
                    $ref: "#/components/schemas/Schedule"
                in_operation_since:
                    type: string
                    format: date-time
                deprecated_since:
                    type: string
                    format: date-time
                max_simultaneous_subscriptions:
                    type: integer
                    minimum: 0
                personal_goal:
                    type: object
                    additionalProperties: false
                    properties:
                        trips_target:
                            type: integer
                        payout_amount:
                            type: integer
                    required:
                      - trips_target
                      - payout_amount
            required:
                - id
                - schedule
                - in_operation_since
                - max_simultaneous_subscriptions
                
```

Одного цвета отображаются смены с одинаковым id.

Добавление/изменение смены вызывает ручка

```

/admin/shuttle-control/v1/template-shifts/item:
        put:
            description: Добавляет или изменяет смену
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: "#/components/schemas/TemplateShiftsItemRequest"
            responses:
                200:
                    description: OK
                400:
                    description: Невозможно изменить смену с выбранной датой начала
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/Error"
                404:
                    description: Не найдена заменяемая смена
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/Error"

components:
    schemas:
        TemplateShiftsItemRequest:
            type: object
            additionalProperties: false
            properties:
                new_template_shift_id:
                    type: string
                replaced_shift_id:
                    type: string
                route_name:
                    type: string
                schedule:
                    description: Объект расписаний как в скидках
                    $ref: "#/components/schemas/Schedule"
                in_operation_since:
                    type: string
                    format: date-time
                deprecated_since:
                    type: string
                    format: date-time
                max_simultaneous_subscriptions:
                    type: integer
                    minimum: 0
                personal_goal:
                    type: object
                    additionalProperties: false
                    properties:
                        trips_target:
                            type: integer
                        payout_amount:
                            type: integer
                    required:
                      - trips_target
                      - payout_amount
            required:
                - new_template_shift_id
                - route_name
                - schedule
                - in_operation_since
                - max_simultaneous_subscriptions

```

Удаление:

```

/admin/shuttle-control/v1/template-shifts/item:
        delete:
            description: Удаляет смену
            parameters:
              - in: query
                name: template_shift_id
                required: true
                schema:
                    type: string
            responses:
                200:
                    description: OK
                400:
                    description: Смена не может быть удалена прямо сейчас
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/Error"
                404:
                    description: Не найдена удаляемая смена
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/Error"

```

## Админка слотов работы

Для списка маршрутов и городов так же вызывается `admin/shuttle-control/v1/present-routes`.

Показ всех активных слотов по вызову ручки:

```

/admin/shuttle-control/v1/shifts/list:
    get:
        description: Возвращает все слоты работы на маршруте, попадающие в диапазон дат
        parameters:
            - name: route_name
              in: query
              required: true
              schema:
                type: string
            - name: date_from
              in: query
              required: true
              schema:
                type: string
                format: date-time
            - name: date_to
              in: query
              required: true
              schema:
                type: string
                format: date-time
        responses:
            200:
                description: OK
                content:
                    application/json:
                        schema:
                            type: array
                            items: 
                                $ref: '#/components/schemas/AdminTemplateShift'

components:
    schemas:
        AdminShift:
            type: object
            additionalProperties: false
            properties:
                shift_id:
                    type: string 
                starts_at:
                    type: string
                    format: date-time
                ends_at:
                    type: string
                    format: date-time
                subscribed_drivers:
                    type: array
                    items:
                      type: object
                      additionalProperties: false
                      properties:
                        dbid_uuid:
                            type: string
                        name:
                            type: string
                      required:
                        - dbid_uuid
                        - name
                subscriptions_hash:
                    description: hash of dbid_uuid in ascending order
                    type: string
            required:
                - shift_id
                - starts_at
                - ends_at
                - subscribed_drivers
                - subscriptions_hash
                
        AdminTemplateShift:
            type: object
            additionalProperties: false
            properties:
                template_shift_id:
                    type: string
                max_simultaneous_subscriptions:
                    type: integer
                in_operation_since:
                    type: string
                    format: date-time
                deprecated_since:
                    type: string
                    format: date-time
                personal_goal:
                    type: object
                    additionalProperties: false
                    properties:
                        trips_target:
                            type: integer
                        payout_amount:
                            type: integer
                    required:
                      - trips_target
                      - payout_amount
                shifts:
                    type: array
                    items:
                        $ref: '#/components/schemas/AdminShift'
            required:
                - template_shift_id
                - max_simultaneous_subscriptions
                - in_operation_since
                - shifts

```

Добавление/удаление водителей производится в ручке

```

/admin/shuttle-control/v1/shifts/item:
    post:
        description: Изменение подписок водителей на смены
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        type: object
                        additionalProperties: false
                        properties:
                            shifts:
                                type: array
                                items:
                                    $ref: "#/components/schemas/SingleShiftItemRequest"
                        required:
                          - shifts
        responses:
            200:
                description: OK
            400:
                description: Невозможно изменить статус подписки у водителя по какой-то причине
                content:
                    application/json:
                        schema:
                            $ref: "#/components/schemas/Error"
            409:
                description: Подписки водителей изменились с момента запроса
                content:
                    application/json:
                        schema:
                            $ref: "#/components/schemas/Error"

components:
    schemas:
        SingleShiftItemRequest:
            type: object
            additionalProperties: false
            properties:
                shift_id:
                    type: string
                subscribed_drivers:
                    type: array
                    items:
                        description: dbid_uuid
                        type: string
                subscriptions_hash:
                    type: string
            required:
                - shift_id
                - subscribed_drivers
                - subscriptions_hash

```
