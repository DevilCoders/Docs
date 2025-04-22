## Апи для админки стилей карты

### Бизнес-описание

Клиентская ручка стилей карт переезжает из экспериментов 3.0 в сервис inapp_communications.
Данные стилей будут храниться в promotions и отдаваться клиентам из кэша в inapp_communications.
В этой связи появляется потребность расширить апи promotions для управления этими данными.

### Видение

В админке добавляется режим для работы со стилями карт.
Этот режим позволяет просматривать и редактировать определения стилей,
а также назначать их на разные конфигурации пользовательских приложений.
Админка работает со стилями, обращаясь к апи сервиса inapp_communications.
Для этого предлагается добавить методы:

```
    /admin/map-styles/definition
    /admin/map-styles/all-ids
    /admin/map-styles/update
    /admin/map-styles/remove
```

### Примерный план использования апи

На экране имеется редактор стиля, меню выбора функционального идентификатора и кнопки "сохранить", "переиспользовать", "добавить" и "удалить", описание работы которых приведено ниже.

#### инициализация

- пользователь открыл админку стилей
- запрос на `/admin/map-styles/all-ids` - получить все функциональные идентификаторов, заполнить менюшку доступних функциональные идентификаторов

#### редактироване стиля

подготовить содержимое стиля для редактирования

- пользователь выбирает один из функциональных идентификаторов в меню
- запрос на `/admin/map-styles/definition` - получить определение выбранного стиля и его etag
- отрисовать стиль в редакторе

#### сохранение изменения содержимого стиля

сохранить текущий стиль из редактора в текущий функциональный идентификатор

- при открытом для редактировании стиле нажать "сохранить"
- запрос на `/admin/map-styles/update` с выбранным функциональным идентификатором и новым содержимым стиля

#### переиспользование стиля в другом функциональном идентификаторе

сохранить текущий стиль из редактора в другой функциональный идентификатор

- при открытом для редактировании стиле нажать "назначить этот стиль для другого идентификатора", выбрать целевой идентификатор
- запрос на `/admin/map-styles/update` с новым функциональным идентификатором и etag'ом открытого стиля

#### добавление функционального идентификатора

создать новый функциональный идентификатор и сохранить в него текущий стиль из редактора

- при открытом для редактировании стиле нажать "добавть идентификатор", заполнить его поля
- запрос на `/admin/map-styles/update` с новым функциональным идентификатором и etag'ом открытого стиля
- в меню функциональных идентификаторов добавить и выбрать только что созданный идентификатор

#### удаление функционального идентификатора

удалить текущий функциональный идентификатор

- при открытом для редактировании стиле нажать "удалить идентификатор", переспросить
- запрос на `/admin/map-styles/remove` с выбранным функциональным идентификатором
- в меню функциональных идентификаторов удалить выбранный идентификатор

### Спецификация Апи

```yaml
    /admin/map-styles/definition/:
        post:
            summary: Получение стиля карты по его ID
            operationId: AdminGetMapStyleDefinition
            parameters:
              - in: body
                name: body
                required: true
                schema:
                    $ref: "#/definitions/MapStyleRequest"
            responses:
                200:
                    description: OK
                    schema:
                        $ref: "#/definitions/MapStyleResponse"
                404:
                    description: Not found
                    schema:
                        $ref: 'promotions/definitions.yaml#/definitions/ErrorResponse'


    /admin/map-styles/all-ids/:
        get:
            summary: Получение всех ID стилей карты
            operationId: AdminGetAllMapStyleIds
            parameters: []
            responses:
                200:
                    description: OK
                    schema:
                        $ref: "#/definitions/AllMapStyleIdsResponse"


    /admin/map-styles/update/:
        post:
            summary: Обновление и удаление стиля карты
            operationId: AdminUpdateMapStyle
            parameters:
              - in: body
                name: body
                required: true
                schema:
                    $ref: "#/definitions/MapStyleUpdateRequest"
            responses:
                200:
                    description: OK
                    schema:
                        $ref: "#/definitions/MapStyleUpdateResponse"
                400:
                    description: Bad Request
                    schema:
                        $ref: 'promotions/definitions.yaml#/definitions/ErrorResponse'
                404:
                    description: Not found
                    schema:
                        $ref: 'promotions/definitions.yaml#/definitions/ErrorResponse'
                500:
                    description: Внутренняя ошибка сервиса
                    schema:
                        $ref: 'promotions/definitions.yaml#/definitions/ErrorResponse'

    /admin/map-styles/remove/:
        post:
            summary: Удаление и удаление стиля карты
            operationId: AdminRemoveMapStyle
            parameters:
              - in: body
                name: body
                required: true
                schema:
                    $ref: "#/definitions/MapStyleRemoveRequest"
            responses:
                200:
                    description: OK
                    schema:
                        $ref: "#/definitions/MapStyleUpdateResponse"
                400:
                    description: Bad Request
                    schema:
                        $ref: 'promotions/definitions.yaml#/definitions/ErrorResponse'
                404:
                    description: Not found
                    schema:
                        $ref: 'promotions/definitions.yaml#/definitions/ErrorResponse'
                500:
                    description: Внутренняя ошибка сервиса
                    schema:
                        $ref: 'promotions/definitions.yaml#/definitions/ErrorResponse'


definitions:
    MapStyleRequest:
        type: object
        additionalProperties: false
        properties:
            requested_style_id:
                $ref: "promotions/definitions.yaml#/definitions/MapStyleId"
        required:
          - requested_style_id

    MapStyleResponse:
        type: object
        description: запрошенный стиль
        additionalProperties: false
        properties:
            id:
                $ref: "promotions/definitions.yaml#/definitions/MapStyleId"
            etag:
                type: integer
            style:
                $ref: "promotions/definitions.yaml#/definitions/MapStyle"
        required:
          - id
          - etag
          - style

    AllMapStyleIdsResponse:
        type: object
        additionalProperties: false
        properties:
            ids:
                type: array
                items:
                    $ref: "promotions/definitions.yaml#/definitions/MapStyleId"
        required:
          - ids

    MapStyleUpdateRequest:
        type: object
        additionalProperties: false
        properties:
            id:
                $ref: "promotions/definitions.yaml#/definitions/MapStyleId"
            style:
                description: установить для данного ID новое определение стиля
                $ref: "promotions/definitions.yaml#/definitions/MapStyle"
            etag:
                description: установить для данного ID определение уже имеющегося
                    стиля по etag
                type: integer
        required:
          - id

    MapStyleUpdateResponse:
        type: object
        additionalProperties: false
        properties:
            etag:
                description: etag только что изменённого стиля
                type: integer

    MapStyleRemoveRequest:
        type: object
        additionalProperties: false
        properties:
            removed_style_id:
                $ref: "promotions/definitions.yaml#/definitions/MapStyleId"
        required:
          - removed_style_id

    MapStyleId:
        type: object
        additionalProperties: false
        properties:
            app:
                type: string
            mode:
                type: string
            theme:
                type: string
                enum:
                  - light
                  - dark

    MapStyle:
        type: object
        additionalProperties: false
        properties:
            map_style:
                type: array
                items:
                    type: object
                    additionalProperties: false
                    properties:
                        elements:
                            type: string
                        stylers:
                            oneOf:
                              - type: object
                                additionalProperties: false
                                properties:
                                    color:
                                        type: string
                                    hue:
                                        type: string
                                    lightness:
                                        type: number
                                    saturation:
                                        type: number
                                    scale:
                                        type: number
                                    visibility:
                                        type: string
                                    zoom:
                                        type: array
                                        items:
                                            type: integer
                              - type: array
                                items:
                                    type: object
                                    additionalProperties: false
                                    properties:
                                        color:
                                            type: string
                                        hue:
                                            type: string
                                        lightness:
                                            type: number
                                        saturation:
                                            type: number
                                        scale:
                                            type: number
                                        visibility:
                                            type: string
                                        zoom:
                                            items:
                                                type: integer
                                            type: array
                        tags:
                            type: object
                            additionalProperties: false
                            properties:
                                all:
                                    oneOf:
                                      - type: string
                                      - type: array
                                        items:
                                            type: string
                                any:
                                    items:
                                        type: string
                                    type: array
                                none:
                                    items:
                                        type: string
                                    type: array
                        types:
                            oneOf:
                              - type: string
                              - type: array
                                items:
                                    type: string
                    required:
                      - stylers
                      - types
            route_traffic_style:
                type: object
                additionalProperties: false
                properties:
                    gradient_length:
                        type: integer
                    inner_outline_enabled:
                        type: boolean
                    jam_style_colors:
                        type: object
                        additionalProperties: false
                        properties:
                            blocked:
                                type: string
                            free:
                                type: string
                            hard:
                                type: string
                            light:
                                type: string
                            unknown:
                                type: string
                            very_hard:
                                type: string
                        required:
                          - blocked
                          - free
                          - hard
                          - light
                          - unknown
                          - very_hard
                    outline_color:
                        type: string
                    outline_width:
                        type: integer
                    stroke_width:
                        type: integer
                required:
                  - gradient_length
                  - inner_outline_enabled
                  - jam_style_colors
                  - outline_color
                  - outline_width
                  - stroke_width
        required:
          - map_style
          - route_traffic_style
```
