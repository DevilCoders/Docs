# Копирование меню

Будет 2 ручки:
1) Копируем меню из исходного заведения в конченое с конкретной ревизии
2) Узнаем возможность скопировать из исходного в переданные

## Предпологаемая схема

paths:
    /4.0/restapp-front/eats-restapp-menu/v1/menu/copy:
        post:
            description: Копирование меню
            parameters:
                - $ref: "#/components/parameters/PartnerId"
                - $ref: "#/components/parameters/SourcePlaceId"
                - $ref: "#/components/parameters/SourceRevision"
                - $ref: "#/components/parameters/TargetPlaceId"
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
            responses:
                200:
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/RevisionResult"
                403:
                    description: Нет прав на меню у данного заведения
                    content:
                        application/json:
                            schema:
                                $ref: "../definitions.yaml#/components/schemas/ApiError"
                404:
                    description: Нет меню с такой ревизией у данного заведения
                    content:
                        application/json:
                            schema:
                                $ref: "../definitions.yaml#/components/schemas/ApiError"

    /4.0/restapp-front/eats-restapp-menu/v1/menu/copy/suggest:
        post:
            description: Копирование меню
            parameters:
                - $ref: "#/components/parameters/PartnerId"
                - $ref: "#/components/parameters/TargetPlaceId"
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
            responses:
                200:
                    description: OK
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/CopySuggestResponse"
                403:
                    description: Нет прав на меню у данного заведения
                    content:
                        application/json:
                            schema:
                                $ref: "../definitions.yaml#/components/schemas/ApiError"
                404:
                    description: Нет исходного заведения
                    content:
                        application/json:
                            schema:
                                $ref: "../definitions.yaml#/components/schemas/ApiError"

components:
    parameters:
        PartnerId:
            name: X-YaEda-PartnerId
            in: header
            required: true
            description: ID партнера
            schema:
                type: integer
                format: int64
        SourcePlaceId:
            name: source_place_id
            in: query
            required: true
            description: ID заведения из которого копируется
            schema:
                type: integer
                format: int64
        SourceRevision:
            name: source_revision
            in: query
            required: true
            description: Уникальная ревизия меню
            schema:
                type: string
        TargetPlaceId:
            name: target_place_id
            in: query
            required: true
            description: ID заведения куда копируется
            schema:
                type: integer
                format: int64

        RevisionResult:
            type: object
            additionalProperties: false
            required:
                - revision
                - status_type
                - status
            properties:
                status_type:
                    $ref: "../definitions/revision.yaml#/components/schemas/RevisionStatusType"
                status:
                    $ref: "../definitions/revision.yaml#/components/schemas/RevisionStatus"
                revision:
                    description: Уникальная ревизия меню
                    type: string
                activate_at:
                    description:
                        Запланированное время применения меню (для отложенного
                        меню)
                    type: string
                    format: date-time
                applied_at:
                    description: Время успешного применения меню в коре (при успехе)
                    type: string
                    format: date-time
                created_at:
                    description:
                        Время создания меню, для "внешнего" меню этой даты
                        не будет
                    type: string
                    format: date-time
                errors:
                    description:
                        Описание ошибок, возникших при парсинге/обновлении
                        меню
                    $ref: "../definitions/errors.yaml#/components/schemas/MenuError"

        CopySuggestPlace:
            type: object
            additionalProperties: false
            required:
                - target_place_id
                - id
                - name
                - type
                - can_copy
            properties:
                target_place_id:
                    type: integer
                    format: int64
                    description: ID заведения куда планируется копировать
                id:
                    type: integer
                    format: int64
                    description: ID заведения откуда копируется
                name:
                    type: string
                    description: Наименование места
                address:
                    type: string
                    description: Адрес места, формат (Улица, Дом, Город, Страна)
                type:
                    type: string
                    description: Тип доставки места
                    enum:
                      - native
                      - marketplace
                can_copy:
                    type: boolean
                    description: Возможно ли копирование в это заведение
                reason:
                    type: string
                    description: Причина недоступности копирования

        CopySuggestResponse:
            type: object
            additionalProperties: false
            required:
              - payload
            properties:
                payload:
                    type: array
                    items:
                        $ref: '#/components/schemas/CopySuggestPlace'
