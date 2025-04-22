## Задача

[SCOOTERDEV-228](https://st.yandex-team.ru/SCOOTERDEV-228)


Зарядные станции.

Нужно поддержать в админке:
1. Cоздание/изменение лавок/шкафов/аккумуляторов.
2. Список лавок/шкафов/аккумуляторов с фильтрацией и пагинацией.


Создание/изменение/отображение лавок.

Отображение списка лавок:
 
Для каждой лавки в админке хотим отображать ее id, координаты и список шкафов. Для каждого шкафа в списке хотим отображать его id, 
количество ячеек в шкафу свободных для бронирования, количество аккумуляторов в шкафу свободных для бронирования и тип шкафа(опционально).
Ручка будет находится в scooters-misc, будет принимать курсор, лимит и фильтры.

Для получения информации о шкафах, внутри вызова этой ручки будет вызываться ручка 
из sccoter-accumulator /scooter-accumulator/v1/depot/cell/available-for-booking.

Пагинация происходит по лавкам.

Предлагаю схему post-ручки в scooters-misc:

```
/admin/v1/depots/list:
    post:
        summary: Возвращает информацию о лавках
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        description: Запрос для выдачи информации по лавкам
                        type: object
                        additionalProperties: false
                        properties:
                            cursor:
                                type: string
                                minLength: 1
                            limit:
                                type: integer
                                minimum: 1
                            depot_id:
                                type: string
                                minLength: 1
                            created_at_min:
                                    type: string
                                    format: date-time
                            created_at_max:
                                    type: string
                                    format: date-time
        responses:
            '200':
                description: Список строк с информацией о лавках
                content:
                    application/json:
                        schema:
                            description: Информация о лавках
                            type: object
                            additionalProperties: false
                            required:
                            - depots
                            properties:
                                cursor:
                                    type: string
                                    minLength: 1
                                depots:
                                    description: Список лавок
                                    type: array
                                    items:
                                        description: Информация о лавке
                                        type: object
                                        additionalProperties: false
                                        required:
                                        - depot_id
                                        - location
                                        - created_at
                                        - updated_at
                                        - cabinets
                                        properties:
                                            depot_id:
                                                type: string
                                                minLength: 1
                                            location:
                                                type: object
                                                additionalProperties: false
                                                required:
                                                - lon
                                                - lat
                                                properties:
                                                    lon:
                                                        type: number
                                                        minimum: -180.0
                                                        maximum: 180.0
                                                    lat:
                                                        type: number
                                                        minimum: -180.0
                                                        maximum: 180.0
                                            created_at:
                                                type: string
                                                format: date-time
                                            updated_at:
                                                type: string
                                                format: date-time
                                            cabinets:
                                                type: array
                                                items:
                                                    description: Информация о шкафе
                                                    type: object
                                                    additionalProperties: false
                                                    required:
                                                    - cabinet_id
                                                    - accumulators_available_for_booking
                                                    - empty_cells_available_for_booking
                                                    properties:
                                                        cabinet_id:
                                                            type: string
                                                            minLength: 1
                                                        cabinet_type:
                                                            type: string
                                                            description: Тип шкафа
                                                            enum:
                                                            - cabinet
                                                            - charge_station
                                                            - charge_station_without_id_receiver
                                                        accumulators_available_for_booking:
                                                            type: integer
                                                            minimum: 0
                                                            description: Количество аккумуляторов доступных для бронирования
                                                        empty_cells_available_for_booking:
                                                            type: integer
                                                            minimum: 0
                                                            description: Количество ячеек доступных для бронирования

```

Добавление новой лавки:

Для добавления лавки достаточно знать depot_id, location.
Ручка будет находится в scooters-misc, будет принимать depot_id, location.
Предлагаю схему post ручки:

```
/admin/v1/depots/create
    description: Добавление лавки
            parameters:
                XIdempotencyToken:
                    in: header
                    name: X-Idempotency-Token
                    required: true
                    schema:
                        type: string
                        minLength: 16
                        maxLength: 64
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
                            required:
                            - depot_id
                            - location
                            properties:
                                depot_id:
                                    type: string
                                    minLength: 1
                                location:
                                    type: object
                                    additionalProperties: false
                                    required:
                                    - lon
                                    - lat
                                    properties:
                                        lon:
                                            type: number
                                            minimum: -180.0
                                            maximum: 180.0
                                        lat:
                                            type: number
                                            minimum: -180.0
                                            maximum: 180.0
            responses:
            '200':
                description: Успех
            '400':
                description: Ошибка добавление шкафа
                content:
                    application/json:
                        schema:
                            type: object
                            required:
                            - message
                            - code
                            properties:
                                message:
                                    type: string
                                    description: Сообщение об ошибке
                                    minLength: 1
                                code:
                                    description: Причина ошибки добавление шкафа
                                    type: string
                                    enum:
                                    - '400'
                            additionalProperties: false
```

Изменение существующей лавки:
Для изменения лавки достаточно знать depot_id. Можно указать location.
Depot_id изменить нельзя.
Ручка будет находится в scooters-misc.
Если указанная лавка не существует - ошибка.
Предлагаю схему post ручки:

```
/admin/v1/depots/update
    description: Изменение лавки
        parameters:
            XIdempotencyToken:
                in: header
                name: X-Idempotency-Token
                required: true
                schema:
                    type: string
                    minLength: 16
                    maxLength: 64
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        type: object
                        additionalProperties: false
                        required:
                        - depot_id
                        properties:
                            depot_id:
                                type: string
                                minLength: 1
                            location:
                                type: object
                                additionalProperties: false
                                required:
                                - lon
                                - lat
                                properties:
                                    lon:
                                        type: number
                                        minimum: -180.0
                                        maximum: 180.0
                                    lat:
                                        type: number
                                        minimum: -180.0
                                        maximum: 180.0
        responses:
            '200':
                description: Успех
            '400':
                description: Ошибка изменения лавки
                content:
                    application/json:
                        schema:
                            type: object
                            required:
                            - message
                            - code
                            properties:
                                message:
                                    type: string
                                    description: Сообщение об ошибке
                                    minLength: 1
                                code:
                                    description: Причина ошибки изменения лавки
                                    type: string
                                    enum:
                                    - '400'
                            additionalProperties: false
```

Отображение списка шкафов:

Для каждого шкафа в админке хотим отображать его id, количество ячеек в шкафу свободных для бронирования, количество аккумуляторов в шкафу свободных для бронирования, id лавки, в которой находится шкаф, тип шкафа. 
Ручка будет находится в scooter-accumulator, будет принимать курсор, лимит и фильтры.

Пагинация происходит по шкафам.

Предлагаю схему post-ручки в scooter-accumulator: 

```
/scooter-accumulator/v1/admin-api/cabinet/list:
    post:
        description: Получение информации о шкафах
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        type: object
                        additionalProperties: false
                        properties:
                            cursor:
                                type: string
                                minLength: 1
                            limit:
                                type: integer
                                minimum: 1
                            cabinet_id:
                                type: string
                                minLength: 1
                            depot_id:
                                type: string
                                minLength: 1
                            cabinet_type:
                                type: string
                                enum:
                                - cabinet
                                - charge_station
                                - charge_station_without_id_receiver
                            created_at_min:
                                    type: string
                                    format: date-time
                            created_at_max:
                                    type: string
                                    format: date-time          
        responses:
            '200':
                description: Список строк с информацией о шкафах
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
                            required:
                            - cabinets
                            properties:
                                cabinets:
                                    type: array
                                    items:
                                        type: object
                                        additionalProperties: false
                                        required:
                                        - cabinet_id
                                        - depot_id
                                        - cabinet_type
                                        - accums_available_for_booking
                                        - cells_available_for_booking
                                        - created_at
                                        - updated_at
                                        properties:
                                            cabinet_id:
                                                type: string
                                                minLength: 1
                                            depot_id:
                                                type: string
                                                minLength: 1
                                            cabinet_type:
                                                type: string
                                                description: Тип шкафа
                                                enum:
                                                - cabinet
                                                - charge_station
                                                - charge_station_without_id_receiver
                                            accumulators_available_for_booking:
                                                type: integer
                                                minimum: 0
                                            cells_available_for_booking:
                                                type: integer
                                                minimum: 0
                                            created_at:
                                                type: string
                                                format: date-time
                                            updated_at:
                                                type: string
                                                format: date-time 
                                cursor:
                                    type: string
                                    minLength: 1
```

Создание/изменение шкафов.

Добавление шкафа:

Для добавления шкафа достаточно знать cabinet_id, cabinet_type, depot_id, количество ячеек в нем.
Предлагаю сделать ручку в scooter-accumulator для добавление шкафа.

Можно указать depot_id, которое не существует в бд в scooters-misc.

При создании шкафа и указании n ячеек, в бд создается нужное количество незабронированных и пустых
ячеек с заданным cabinet_id и cell_id от 1 до n.
Если указанный шкаф уже существует - ошибка.
Предлагаю схему post ручки:

```
/scooter-accumulator/v1/admin-api/cabinet
    post:
        description: Добавление шкафа
        parameters:
            XIdempotencyToken:
                in: header
                name: X-Idempotency-Token
                required: true
                schema:
                    type: string
                    minLength: 16
                    maxLength: 64
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        type: object
                        additionalProperties: false
                        required:
                          - cabinet_id
                          - cabinet_type
                          - depot_id
                          - cells_amount
                        properties:
                            cabinet_id:
                                type: string
                                minLength: 1
                            cabinet_type:
                                type: string
                                enum:
                                - cabinet
                                - charge_station
                                - charge_station_without_id_receiver
                            depot_id:
                                type: string
                                minLength: 1
                            cells_amount:
                                type: integer
                                minimum: 0
        responses:
            '200':
                description: Успех
            '400':
                description: Ошибка добавление шкафа
                content:
                    application/json:
                        schema:
                            type: object
                            required:
                            - message
                            - code
                            properties:
                                message:
                                    type: string
                                    description: Сообщение об ошибке
                                    minLength: 1
                                code:
                                    description: Причина ошибки добавления шкафа
                                    type: string
                                    enum:
                                    - '400'
                            additionalProperties: false
```

Изменение шкафа:

Для изменения шкафа достаточно знать cabinet_id. Можно указать cabinet_type, depot_id, количество ячеек в нем.
Cabinet_id изменить нельзя.
Предлагаю сделать ручку в scooter-accumulator для изменения шкафа.

Если указанное количество ячеек больше, чем текущий размер шкафа, то в бд я ячейками создаются новые пустые и незабронированные ячейки.
Если указанное количество ячеек k меньше, чем текущий размер шкафа n, то, если среди ячеек с id от k+1 до n найдется непустая или забронированная,
то запрещаем менять шкаф, ответ с ошибкой.

Если меняем шкафа типа "cabinet" (шкаф с кладовщиком) на какой то другой тип шкафа, то в бд c ячейками убираем error_code о том что ячейка в
шкафе типа "cabinet" для всех ячеек из указанного шкафа.

Предлагаю схему patch ручки:

```
/scooter-accumulator/v1/admin-api/cabinet
    patch:
        description: Изменение шкафа
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        type: object
                        additionalProperties: false
                        required:
                          - cabinet_id
                        properties:
                            cabinet_id:
                                type: string
                                minLength: 1
                            cabinet_type:
                                type: string
                                enum:
                                - cabinet
                                - charge_station
                                - charge_station_without_id_receiver
                            depot_id:
                                type: string
                                minLength: 1
                            cells_amount:
                                type: integer
                                minimum: 0
        responses:
            '200':
                description: Успех
            '400':
                description: Ошибка изменения шкафа
                content:
                    application/json:
                        schema:
                            type: object
                            required:
                            - message
                            - code
                            properties:
                                message:
                                    type: string
                                    description: Сообщение об ошибке
                                    minLength: 1
                                code:
                                    description: Причина ошибки изменения шкафа
                                    type: string
                                    enum:
                                    - '400'
                            additionalProperties: false
```                        

Создание/изменение аккумуляторов.
   
Добавление аккума:

Для добавления аккумулятора в бд достаточно знать accumulator_id и serial_number.
Если указываем cabinet_id, то есть разветвления, так как шкафы бывают разного вида.
Для шкафа с кладовщиком при отсутствии в запросе cell_id, запрос означает: "положи в любую свободную ячейку".

Для добавление аккумулятора в scooter-accumulator сделаем новую ручку, которая принимает id аккума и его серийный номер как обязательные поля, и уровень заряда, 
cabinet_id, cell_id, scooter_id, contractor_id как необязательные.

Если тип указываемого шкафа - умный шкаф, то если поле cell_id не указано, либо указано и занято другим аккумом в этом шкафу или ячейки не существует или она забронирована, то 
возвращаем ответ с ошибкой, иначе добавляем аккум и тип ответа 200.
Если тип указываемого шкафа - шкаф с кладовщиком, то если поле cell_id не указано, то добавлем аккум в любую свободную ячейку и ответ 200,
если нет свободных, то ошибка. Если шкаф с кладовщиком и ячейка указана, то логика как с умным шкафом.
Если шкаф не указан, но указана ячейка, то ошибка.

Предлагаю схему post ручки:

```
/scooter-accumulator/v1/admin-api/accumulator
    post:
        description: Добавление аккумулятора
        parameters:
            XIdempotencyToken:
                in: header
                name: X-Idempotency-Token
                required: true
                schema:
                    type: string
                    minLength: 16
                    maxLength: 64
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        type: object
                        additionalProperties: false
                        required:
                        - accumulator_id
                        - serial_number
                        properties:
                            accumulator_id:
                                type: string
                                minLength: 1
                            serial_number:
                                type: string
                                minLength: 1
                            cabinet_id:
                                type: string
                                minLength: 1
                            cell_id:
                                type: string
                                minLength: 1
                            scooter_id:
                                type: string
                                minLength: 1
                            contractor_id:
                                type: string
                                minLength: 1
                            charge:
                                type: integer
                                minimum: 0
                                maximum: 100
        responses:
            '200':
                description: Успех
            '400':
                description: Ошибка добавления аккумулятора
                content:
                    application/json:
                        schema:
                            type: object
                            required:
                            - message
                            - code
                            properties:
                                message:
                                    type: string
                                    description: Сообщение об ошибке
                                    minLength: 1
                                code:
                                    description: Причина ошибки добавления аккумулятора
                                    type: string
                                    enum:
                                    - '400'
                            additionalProperties: false

```

Изменение данных об аккумуляторе:

Для изменения данных об аккумуляторе предлагаю сделать в scooter-accumulator новую ручку, которая будет принимать id аккума как обязательный
параметр, а также charge, cabinet_id, cell_id, scooter_id, contractor_id, cabinet_id_is_null, scooter_id_is_null, contractor_id_is_null, как необязательные.
Мы не сможем изменить serial_number и accumulator_id, accumulator_id/serial_number связываются сразу при добавлении аккумулятора.

Изменение cabinet_id, cell_id, scooter_id, contractor_id, может означать, что, либо добавляем аккумулятор в нужное место(до этого там было null) или перекладываем в другое место, либо просто вынимаем из предыдущего места.
Можно не указать id места как и поле is_null. Можно указать сразу несколько мест, например cabinet и scooter.

Если не указали какое нибудь поле из cabinet_id, cell_id, scooter_id, contractor_id, то не перекладываем аккумулятор.
Если указали какое нибудь поле из cabinet_id_is_null, scooter_id_is_null, contractor_id_is_null, то вынимаем аккумулятор из указаного места(если он там находится).
Если для заданного места одновременно is_null = true и id места указано, то ошибка.


Если задана ячейка и не задан шкаф, то ошибка.
Если ячейка задана и занята другим аккумом в этом шкафу или не существует или забронирована, то ошибка.
Если ячейка не задана и тип шкафа - умный шкаф, то ошибка.
Если ячейка не задана и тип шкафа - шкаф с кладовщиком, то, если в заданном шкафе нет свободных и незабронированных ячеек,то ошибка.

Если на аккум, который хотим изменить, есть бронирование, то возвращаем ответ с ошибкой.

Предлагаю схему ручки:

```

scooter-accumulator/v1/admin-api/accumulator
    patch:
        description: Изменение информации об аккумуляторе
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        type: object
                        additionalProperties: false
                        required:
                        - accumulator_id
                        properties:
                            accumulator_id:
                                type: string
                                minLength: 1
                            scooter_id:
                                type: string
                                minLength: 1
                            scooter_id_is_null:
                                type: boolean
                            contractor_id:
                                type: string
                                minLength: 1
                            contractor_id_is_null:
                                type: boolean
                            cabinet_id:
                                type: string
                                minLength: 1
                            cabinet_id_is_null:
                                type: boolean
                            cell_id:
                                type: string
                                minLength: 1
                            charge:
                                type: integer
                                minimum: 0
                                maximum: 100
        responses:
            '200':
                description: Успех
            '400':
                description: Ошибка изменения информации об аккумуляторе
                content:
                    application/json:
                        schema:
                            type: object
                            required:
                            - message
                            - code
                            properties:
                                message:
                                    type: string
                                    description: Сообщение об ошибке
                                    minLength: 1
                                code:
                                    description: Причина ошибки изменения информации об аккумуляторе
                                    type: string
                                    enum:
                                    - '400'
                            additionalProperties: false
        
```

Отображение информации об аккумуляторах:

Для каждого аккума хотим отображать accumulator_id, charge, cabinet_id, serial_number, а также одно из полей cabinet_id,cell_id, scooter_id, contractor_id, зависит от того, где аккум. Также хотим отображать времена добавления и изменения аккумалутора.
Для этого сделаем ручку в scooter-accumulator,
которая будет принимать курсор, лимит и фильтры. 
Пагинация по аккумам.

Предлагаю схему ручки:

```

scooter-accumulator/v1/admin-api/accumulator/list:
    post:
        description: Получение информации об аккумуляторах
        requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
                            properties:
                                cursor:
                                    $ref: '../definitions.yaml#/components/schemas/Cursor'
                                limit:
                                    type: integer
                                    minimum: 1
                                accumulator_id:
                                    type: string
                                    minLength: 1
                                cabinet_id:
                                    type: string
                                    minLength: 1
                                cabinet_id_is_null:
                                    type: boolean
                                created_at_min:
                                    type: string
                                    format: date-time
                                created_at_max:
                                    type: string
                                    format: date-time
        responses:
            '200':
                description: Список строк с информацией об аккумуляторах
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
                            required:
                            - accumulators
                            properties:
                                accumulators:
                                    type: array
                                    items:
                                        type: object
                                        additionalProperties: false
                                        required:
                                        - accumulator_id
                                        - serial_number
                                        - charge
                                        - place_id
                                        - created_at
                                        - updated_at
                                        properties:
                                            accumulator_id:
                                                type: string
                                                minLength: 1
                                            serial_number:
                                                type: string
                                                minLength: 1
                                            charge:
                                                type: integer
                                                minimum: 0
                                                maximum: 100
                                            place_id:
                                                type: object
                                                additionalProperties: false
                                                properties:
                                                    contractor_id:
                                                        type: string
                                                        minLength: 1
                                                    cabinet:
                                                        type: object
                                                        additionalProperties: false
                                                        required:
                                                        - cabinet_id
                                                        - cell_id
                                                        properties:
                                                            cabinet_id:
                                                                type: string
                                                                minLength: 1
                                                            cell_id:
                                                                type: string
                                                                minLength: 1
                                                    scooter_id:
                                                        type: string
                                                        minLength: 1
                                            created_at:
                                                type: string
                                                format: date-time
                                            updated_at:
                                                type: string
                                                format: date-time                                             
```


