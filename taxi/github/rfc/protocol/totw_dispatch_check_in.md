# Продуктовое описание

Хотим реализовать новый флоу в аэропортах с запуском поиска водителя только после того, как пользователь делает чек-ин в 
определенной зоне. При этом заказ можно создать в любой момент.
При этом водители должны искаться на специальной парковке рядом с зоной чек-ина, но возможен фолбэк на поиск водителей из города.

[Миро](https://miro.com/app/board/o9J_l7XG3Mk=/)

## API и логика
1. После создания заказа, если бэкенд решает что заказ создан по флоу с чек-ином, то в ответе ручки `3.0/taxiontheway` возвращается новый статус `check_in` в качестве значения поля `order_status`, а также вся необходимая для чек-ина информация в опциональном объекте `dispatch_check_in` в корне. В частности массив зон для чек-ина, при этом в рамках MVP в ответе будет всегда ровно одна зона.
Также должны передаваться подходящие тексты в поле `status_info`.

```json
status_info:
    type: object
    properties:
        translations:
            type: object
            properties:
                card:
                    type: object
                    properties:
                        title_template:
                            type: string
                            example: "Нажмите, когда будете на остановке"
                        subtitle_template:
                            type: string
                            example: "Назначим машину из тех, что уже на остановке"
dispatch_check_in:
    description: Блок данных для заказов с информацией для чек-ина
    type: object
    additionalProperties: false
    properties:
        check_in_zones:
            type: array
            minItems: 1
            maxItems: 1
            items:
                type: object
                additionalProperties: false
                properties:
                    geopoint:
                        description: Координаты зоны чек-ина [lon, lat]
                        type: array
                        items:
                            type: number
                            minimum: -180.0
                            maximum: 180.0
                        minItems: 2
                        maxItems: 2
                        x-taxi-cpp-type: geometry::Position
                    pickup_line_id:
                        description: Идентификатор соответствующей линии подачи
                        type: string
                required:
                    - geopoint
                    - pickup_line_id
        instruction:
            description: Инструкция по проходу в зону посадки
            type: object
            additionalProperties: false
            properties:
                title:
                    description: Локализованный заголовок для UI
                    type: string
                    example: Машины уже есть на нашей парковке
                subtitle: Локализованный подзаголовок для UI
                    description: Локализованный подзаголовок для UI
                    type: string
                    example: Не торопитесь и следуйте инструкции
                image_tag:
                    description: тег для иконки
                    type: string
                promo_id:
                    description: id сторис с шагами инструкции
                    type: string
                show_steps_button_title:
                    description: Локализованный текст кнопки, которая запустит показ сторис с шагами инструкции
                    type: string
                    example: Покажите, как туда пройти
                skip_steps_button_title:
                    description: Локализованный текст кнопки, которая пропустит показ сторис с шагами инструкции
                    type: string
                    example: Да, я иду к зоне посадки
                show_by_default:
                    description: Показывать ли инструкцию по умолчанию
                    type: boolean
                hint_button_title:
                    description: Текст для кнопки открывающей инструкций
                    type: string
                    example: Как пройти
            required:
                - title
                - subtitle
                - image_tag
                - promo_id
                - show_steps_button_title
                - skip_steps_button_title
                - show_by_default
                - hint_button_title
        ui_config:
            description: Настройки UI
            type: object
            properties:
                card_type:
                    description: Тип отображаемое на клиенте карточки
                    type: string
                    enum:
                    - classic
                    - two_button
                    - three_button
                check_in_action:
                    description: Настройки действия для чек-ина
                    type: object
                    additionalProperties: false
                    properties:
                        title:
                            description: Локализованный заголовок для UI
                            type: string
                            example: Я на месте
                        waiting_title:
                            description: Локализованный заголовок для UI при ожидании ответа
                                бэкенда
                            type: string
                            example: Подтверждаем
                        subtitle:
                            description: Локализованный подзаголовок для UI
                            type: string
                            example: Я на месте
                        waiting_subtitle:
                            description: Локализованный подзаголовок для UI при ожидании ответа
                                бэкенда
                            type: string
                            example: Подтверждаем
                        type:
                            description: Тип действия для чек-ина
                            type: string
                            enum:
                                - qr_code
                                - button
                                - slider
                        required:
                            - title
                            - waiting_title
                            - subtitle
                            - waiting_subtitle
                            - type
                details_action:
                    description: Настройки деталей по заказу
                    type: object
                    additionalProperties: false
                    properties:
                        title:
                            description: Локализованный заголовок для UI
                            type: string
                            example: Детали
                    required:
                        - title
            required:
              - card_type
              - check_in_action
        check_in_action:
            description: Настройки действия для чек-ина
            type: object
            additionalProperties: false
            properties:
                title:
                    description: Локализованный заголовок для UI
                    type: string
                    example: Я на месте
                waiting_title:
                    description: Локализованный заголовок для UI при ожидании ответа
                        бэкенда
                    type: string
                    example: Подтверждаем
                subtitle:
                    description: Локализованный подзаголовок для UI
                    type: string
                    example: Я на месте
                waiting_subtitle:
                    description: Локализованный подзаголовок для UI при ожидании ответа
                        бэкенда
                    type: string
                    example: Подтверждаем
                type:
                    description: Тип действия для чек-ина
                    type: string
                    enum:
                        - qr_code
                        - button
                        - slider
                required:
                    - title
                    - waiting_title
                    - subtitle
                    - waiting_subtitle
                    - type
    required:
        - check_in_zones
        - instruction
        - ui_config
        - check_in_action
```

2. Затем клиент должен произвести чек-ин. Для этого надо вызывать ручку `/4.0/dispatch-check-in/v1/start-dispatch` сервиса dispatch-check-in с указанием зоны чек-ина, куда пришел клиент. Ручка будет за passenger authorizer.

```json
paths:
    /4.0/dispatch-check-in/v1/start-dispatch:
        post:
            description: |
                Устанавливает время check-in-а и запускает поиск исполнителя
            requestBody:
                description: Информация по чек-ину
                required: true
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/StartDispatchRequest'
            responses:
                200:
                    description: OK
                400:
                    description: Error response
                    content:
                        application/json:
                            schema:
                                type: object
                                additionalProperties: false
                                properties:
                                    message:
                                        description: Human-readable error
                                        type: string
                                    code:
                                        description: Error code. Значение в случае невалидного QR кода: INVALID_QR_CODE_VALUE
                                        type: string
                                required:
                                  - message
                                  - code

            x-taxi-middlewares:
                api-4.0: true

components:
    schemas:
        StartDispatchRequest:
            type: object
            additionalProperties: false
            properties:
                order_id:
                    description: Id заказа
                    type: string
                pickup_line_id:
                    description: |
                        Id линии подачи. Если не задано и в терминале заказа
                        более одной линии подачи, то запрос вернет ошибку.
                    type: string
                qr_code_value:
                    description: Значение qr кода
                    type: string

            required:
              - order_id
```

3. После чек-ина ручка `3.0/taxiontheway` вернет новый статус `waiting_in_check_in_zone` в качестве значения поля `order_status` и опциональную информцию `check_in_queue_info` о зоне чек-ина.
Также должны передаваться подходящие тексты в поле `status_info`.

```json
status_info:
    type: object
    properties:
        translations:
            type: object
            properties:
                card:
                    type: object
                    properties:
                        title_template:
                            type: string
                            example: "Пожалуйста ожидайте ~10 мин"
                        subtitle_template:
                            type: string
                            example: "Перед вами в очереди еще 5 человек"
check_in_queue_info:
    description: Блок данных для заказов с информацией для ожидания в зоне чек-ина
    type: object
    additionalProperties: false
    properties:
        check_in_zone:
            type: object
            additionalProperties: false
            properties:
                geopoint:
                    description: Координаты зоны чек-ина [lon, lat]
                    type: array
                    items:
                        type: number
                        minimum: -180.0
                        maximum: 180.0
                    minItems: 2
                    maxItems: 2
                    x-taxi-cpp-type: geometry::Position
                pickup_line_id:
                    description: Идентификатор соответствующей линии подачи
                    type: string
            required:
                - geopoint
                - pickup_line_id
    required:
        - check_in_zone
```

4. Если бэкенд пустил заказ по флоу с чек-ином, то в ответе ручки `3.0/taxiontheway` всегда, независимо от статуса заказа будет присутствовать поле `check_in_flow_status`, имеющее следующие значения:
* `before_check_in` - значит для заказ ещё не был произведён чек-ин
* `after_check_in`- значит для заказа был произведён чек-ин

Список может пополняться в будущем, поэтому нельзя завязываться на то, что могут приходить только эти два статуса. В частности, нельзя полагать, что `check_in_flow_status != 'before_check_in' => 'after_check_in'` и наоборот.
