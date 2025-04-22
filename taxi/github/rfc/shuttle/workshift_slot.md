# Слоты работы водителя шаттла

## Концепция

Водители начинают работать согласно сменам - слотам работы, которые они выбирают заранее в Pro, и которые
представляют собой непрерывный интервал времени, в течение которого водителю будут доступны заказы через приложение
и через "от борта".

Принцип подписки: в приложении отображается плашка с расписанием, по нажатию на которую водителю показываются
все возможные слоты работы, ему доступные, на N дней вперед. Водитель может отказаться от выбранного слота работы
(максимум за M часов/минут до ее наступления). Чтобы выйти на линию и получать деньги за линию, смену нужно явно
начать. В идеале при выборе сначала должен открываться экран маршрута, и по нажатию на какой-то доступный маршрут 
открывается выбор слота, привязанного к нему, разнесенный по дням недели. 

У слотов работы должны быть явные ограничения по доступности водителям (например, запрет по тегам). 
К тому же должно быть ограничено сверху число водителей, которым этот слот доступен. В первой итерации 
в слоты не включаем обед и паузы, а также ставка среди всех слотов на одно и то же время фиксирована.

Дизайн по примеру курьеров: https://www.figma.com/file/xPrcG0RGzgrgQMb11UBZ3a/Untitled?node-id=0%3A1

## Новая ручка поллинга

Отходим от старой ручки, привязанной семантически к маршрутам, на новую. В ней дополнительно 
отдаем объект, описывающий текущий статус расписания смен водителя.

```
/driver/v1/shuttle-control/v2/shuttle/status:
    x-generator-tags:
      - android-client
    post:
        description: Poll v2 shuttle status
        operationId: status_v2
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
        responses:
            200:
                description: OK
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/ShuttleStatusResponseV2'
                headers:
                    X-Polling-Power-Policy:
                        schema:
                            type: string
                        description: |
                            Задержка до следующего запроса от консьюмера в разрезе режимов энергопотребления

components:
    schemas:
        ShuttleWorkModeInformation:
            type: object
            additionalProperties: false
            properties:
                title:
                    type: string
                text:
                    type: string
                icon:
                    type: string
                action_status:
                    type: string
                    enum:
                      - route_selection
                      - en_route
                      - warning
            required:
              - title
              - text
              - icon
              - action_status
              
        ShuttleStatusEnumV2:
            type: string
            enum:
              - scheduling
              - en_route
              
        ShiftScheduleUi:
            type: object
            additionalProperties: false
            properties:
                items:
                    type: array
                    items:
                        type: object
                        additionalProperties: true
                        x-taxi-additional-properties-true-reason: конструктор для
                            таксометра
                        x-custom-type: ru.yandex.taximeter.data.api.uiconstructor.ComponentListItemResponse
                        description: constructor ui elements
                    minItems: 1
            required:
              - items

        ShuttleStatusScheduling:
            type: object
            additionalProperties: false
            properties:
                state:
                    $ref: '#/components/schemas/ShuttleStatusEnumV2'
                panels:
                    type: object
                    additionalProperties: false
                    properties:
                        work_mode_info:
                            $ref: '#/components/schemas/ShuttleWorkModeInformation'
                        shift_schedule_ui:
                            $ref: '#/components/schemas/ShiftScheduleUi'
                    required:
                      - shift_schedule_ui
            required:
              - state
              - panels
              
        TicketsSettings:
            type: object
            additionalProperties: false
            description: |
                Настройки параметров билетов, проверяемых на маршруте
            properties:
                length:
                    description: Длина билетов на текущем маршруте
                    type: integer
                    minimum: 1
            required:
              - length

        ShuttleStatusEnRouteV2:
            type: object
            additionalProperties: false
            properties:
                state:
                    $ref: '#/components/schemas/ShuttleStatusEnumV2'
                shuttle_id:
                    type: string
                shift_id:
                    type: string
                route:
                    $ref: '#/components/schemas/ShuttleRoute'
                settings:
                    description: |
                      Настройки отображения различных объектов поллинга
                    type: object
                    additionalProperties: false
                    properties:
                        tickets:
                            $ref: '#/components/schemas/TicketsSettings'
                    required:
                      - tickets
                panels:
                    type: object
                    additionalProperties: false
                    properties:
                        work_mode_info:
                            $ref: '#/components/schemas/ShuttleWorkModeInformation'
                        shift_schedule_ui:
                            $ref: '#/components/schemas/ShiftScheduleUi'
                    required:
                      - work_mode_info
            required:
              - state
              - shuttle_id
              - shift_id
              - route
              - settings
              - panels
              
        ShuttleStatusResponseV2:
            oneOf:
              - $ref: '#/components/schemas/ShuttleStatusScheduling'
              - $ref: '#/components/schemas/ShuttleStatusEnRouteV2'
            discriminator:
                propertyName: state
                mapping:
                    scheduling: ShuttleStatusScheduling
                    en_route: ShuttleStatusEnRouteV2

```

## Главный экран с расписанием

На объекте расписания `ShuttleStatusScheduling` есть краткая информация про текущий выбранный слот (если он есть),
возможность посмотреть все расписание водителя, добавить новую смену или начать следующую (если смена наступает скоро).

### Экран информации про смену

Если нажать на слот на главном экране, раскрывается более подробная информация про него, в котором есть время работы, 
гарантия заработка, etc., а также есть кнопки с действиями начать слот, изменить (если можно, 
по сути бросает на экран с выбором нового слота, см. ниже), 
отменить (если можно), остановить поездку, поставить на паузу/обед (в теории, пока не будет сделано).

```
/driver/v1/shuttle-control/v1/shifts/info:
    x-generator-tags:
      - android-client
    get:
        description: Get shift info
        operationId: shifts_info
        tags:
          - shuttle_pro_api
        parameters:
          - name: Accept-Language
            description: Предпочитаемый язык ответа
            in: header
            schema:
              type: string
            required: true
          - name: shift_id
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
                            $ref: '#/components/schemas/ShiftsInfoResponse'
            404:
                description: Shift is not found
                content:
                    application/json:
                        schema:
                            $ref: '../definitions.yaml#/components/schemas/TaximeterError'

components:
    schemas:
        ShiftsInfoResponse:
            type: object
            additionalProperties: false
            properties:
                title:
                    type: string
                subtitle:
                    description: finished in time | 20 min to go | 10 min late | smth else
                    type: string
                info_items_ui:
                    type: array
                    items:
                        type: object
                        additionalProperties: true
                        x-taxi-additional-properties-true-reason: конструктор для
                            таксометра
                        x-custom-type: ru.yandex.taximeter.data.api.uiconstructor.ComponentListItemResponse
                        description: constructor ui elements
                    minItems: 1
                allowed_actions:
                    type: array
                    items:
                        type: string
                        enum:
                          - start
                          - stop
                          - cancel
            required:
                - title
                - info_items_ui
                - allowed_actions
         
```

Ручка для начала выбранной смены, которая заменяет текущую ручку `shuttle/start_trip`:

```
/driver/v1/shuttle-control/v1/personal-schedule/start-shift: 
    x-generator-tags:
        - android-client
    post:
        description: Start the shift
        operationId: schedule_start_shift
        tags:
            - shuttle_pro_api
        parameters:
            - name: Accept-Language
              description: Предпочитаемый язык ответа
              in: header
              schema:
                  type: string
              required: true
            - name: shift_id
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
                            $ref: '#/components/schemas/ShuttleStatusEnRouteV2'
            400:
                description: Shift cannot be started by the driver
                content:
                    application/json:
                        schema:
                            $ref: '../definitions.yaml#/components/schemas/TaximeterError'
            403:
                description: Shift is forbidden to start by the driver now
                content:
                    application/json:
                        schema:
                            $ref: '../definitions.yaml#/components/schemas/TaximeterError'
            404:
                description: Shift is not found in driver's schedule
                content:
                    application/json:
                        schema:
                            $ref: '../definitions.yaml#/components/schemas/TaximeterError'

```

Для отписки водителя от какой-то уже выбранной смены вызывается ручка:

```
/driver/v1/shuttle-control/v1/personal-schedule/remove-shift: 
    x-generator-tags:
        - android-client
    post:
        description: Remove the shift from the schedule
        operationId: schedule_remove_shift
        tags:
            - shuttle_pro_api
        parameters:
            - name: Accept-Language
              description: Предпочитаемый язык ответа
              in: header
              schema:
                  type: string
              required: true
            - name: shift_id
              in: query
              required: true
              schema:
                  type: string
        responses:
            200:
                description: OK
            400:
                description: Shift cannot be cancelled now
                content:
                    application/json:
                        schema:
                            $ref: '../definitions.yaml#/components/schemas/TaximeterError'
            404:
                description: Shift is not found in the driver schedule
                content:
                    application/json:
                        schema:
                            $ref: '../definitions.yaml#/components/schemas/TaximeterError'

```

### Экран текущего расписания водителя

По нажатию на кнопку с расписанием, появляется окошко со списком уже выбранных водителем смен 

```

/driver/v1/shuttle-control/v1/shifts/schedule:
    x-generator-tags:
        - android-client
    get:
        description: Get driver schedule
        operationId: shifts_schedule
        tags:
            - shuttle_pro_api
        parameters:
            - name: Accept-Language
              description: Предпочитаемый язык ответа
              in: header
              schema:
                  type: string
              required: true
        responses:
            200:
                description: OK
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/ShiftsScheduleResponse'

components:
    schemas:
        ScheduleShift:
            type: object
            additionalProperties: false
            properties:
                id:
                    type: string
                title:
                    type: string
                subtitle:
                    type: string
                status:
                    - missed
                    - finished
                    - planned
                    - ongoing
            required:
                - id
                - title
                - subtitle
                - status

        ScheduleItem:
            type: object
            additionalProperties: false
            properties:
                date:
                    type: string
                    format: date
                shifts:
                    type: array
                    items:
                        $ref: '#/components/schemas/ScheduleShift'
            required:
                - date
                - shifts

        ShiftsScheduleResponse:
            type: object
            additionalProperties: false
            properties:
                schedule:
                    type: array
                    items:
                        $ref: '#/components/schemas/ScheduleItem'
            required:
                - schedule

```

С этого экрана можно посмотреть подробную информацию про слот через ручку `/info`, 
либо добавить новую смену.

### Выбор и добавление слота

По нажатию на кнопку добавления слота появляется экран с доступными маршрутам, для этого вызывается ручка 

```
/driver/v1/shuttle-control/v1/shifts/available-routes: 
    x-generator-tags:
        - android-client
    get:
        description: List of available driver routes
        operationId: shifts_available_routes
        tags:
            - shuttle_pro_api
        parameters:
            - name: Accept-Language
              description: Предпочитаемый язык ответа
              in: header
              schema:
                  type: string
              required: true
        responses:
            200:
                description: OK
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/AvailableRoutesResponse'
   
components:
    schemas:
        AvailableRoutesResponse:
            type: object
            additionalProperties: false
            properties:
                routes:
                    type: array
                    items:
                        type: object
                        additionalProperties: false
                        properties:
                            id:
                                type: string
                            name:
                                type: string
                        required:
                            - id
                            - name
            required:
                - routes   
   
```

По нажатию на маршрут происходит запрос в ручку, в которой отдаются все существующие и доступные водителю слоты
за какой-то определенный промежуток дат

```
/driver/v1/shuttle-control/v1/shifts/available-shifts: 
    x-generator-tags:
        - android-client
    get:
        description: List of available driver shifts
        operationId: shifts_available_shifts
        tags:
            - shuttle_pro_api
        parameters:
            - name: Accept-Language
              description: Предпочитаемый язык ответа
              in: header
              schema:
                  type: string
              required: true
            - in: query
              name: route_ids
              description: route ids
              required: true
              explode: false
              style: form
              schema:
                  type: array
                  items:
                      type: string
                  example: 'route1, route2, route3'
        responses:
            200:
                description: OK
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/AvailableShiftsResponse'

components:
    schemas:
        AvailableShift:
            type: object
            additionalProperties: false
            properties:
                id:
                    type: string
                time_range:
                    type: string
                subtitle:
                    type: string
            required:
              - id
              - time_range
              - subtitle
              
        RouteSchedule:
            type: object
            additionalProperties: false
            properties:
                route_name:
                    type: string
                shifts:
                    type: array
                    items:
                        $ref: '#/components/schemas/AvailableShift'
            required:
                - route_name
                - shifts

        ShiftsScheduleItem:
            type: object
            additionalProperties: false
            properties:
                date:
                    type: string
                    format: date
                routes:
                    type: array
                    items:
                        $ref: '#/components/schemas/RouteSchedule'
            required:
                - date
                - routes

        AvailableShiftsResponse:
            type: object
            additionalProperties: false
            properties:
                shifts_schedule:
                    type: array
                    items:
                        $ref: '#/components/schemas/ShiftsScheduleItem'
            required:
                - shifts_schedule
                
```

Нажатие на слот приводит к его выбору (показывается подробная информация с подтверждением?), 
для подписки на слот вызывается `personal-schedule/reserve-shift`:

```
/driver/v1/shuttle-control/v1/personal-schedule/reserve-shift: 
    x-generator-tags:
        - android-client
    post:
        description: Reserve the shift
        operationId: schedule_reserve_shift
        tags:
            - shuttle_pro_api
        parameters:
          - name: Accept-Language
            description: Предпочитаемый язык ответа
            in: header
            schema:
                type: string
            required: true
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        $ref: "#/components/schemas/ReserveShiftsRequest"  
        responses:
            200:
                description: OK, some shifts (maybe 0) are subscribed. Return |
                 an error message about the shifts which cannot be reserved by any means.
                content:
                    application/json:
                        schema:
                            $ref: "#/components/schemas/ReserveShiftsResponse"
            404:
                description: Some shift is not found, the client should update available shifts
                content:
                    application/json:
                        schema:
                            $ref: '../definitions.yaml#/components/schemas/TaximeterError'
            409:
                description: Shifts to reserve conflict with each other or already reserved shifts
                content:
                    application/json:
                        schema:
                            $ref: '../definitions.yaml#/components/schemas/TaximeterError'

components:
    schemas:
        ReserveShiftsRequest:
            type: object
            additionalProperties: false
            properties:
                shifts:
                    type: array
                    items:
                        type: string
            required:
              - shifts
        
        ReserveShiftsResponse:
            type: object
            additionalProperties: false
            properties:
                partial_reservation_reason:
                    type: object
                    additionalProperties: false
                    properties:
                        title:
                            type: string
                        message:
                            type: string
                    required:
                      - title
                      - message

```

Во время поездки для ее завершения (может быть вызвана только один раз для смены) вызывается ручка-аналог `shuttle/stop_trip`:

```
/driver/v1/shuttle-control/v1/personal-schedule/finish-shift:
    x-generator-tags:
        - android-client
    post:
        description: Finish the shift
        operationId: schedule_finish_shift
        tags:
            - shuttle_pro_api
        parameters:
            - name: Accept-Language
              description: Предпочитаемый язык ответа
              in: header
              schema:
                  type: string
              required: true
            - name: shift_id
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
                            $ref: '#/components/schemas/ShuttleStatusScheduling'
            400:
                description: Shift cannot be stopped by the driver
                content:
                    application/json:
                        schema:
                            $ref: '../definitions.yaml#/components/schemas/TaximeterError'
                                
```
