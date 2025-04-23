# Валидирование меню

Ручка валидирование меню по блюдам или категориям, может быть несколько или одно

## Предпологаемая схема

paths:
    /4.0/restapp-front/eats-restapp-menu/v1/menu/validate:
        post:
            description: Валидирование меню
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
                            required:
                                - categories
                                - items
                            properties:
                                categories:
                                    type: array
                                    description: Категории меню
                                    items:
                                        $ref: "#/components/schemas/MenuCategory"
                                items:
                                    type: array
                                    description: Список блюд доступных для заказа в ресторане
                                    items:
                                        $ref: "#/components/schemas/MenuItem"

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
                                $ref: "#/components/schemas/ValidateResult"
                400:
                    description: Общая ошибка
                    content:
                        application/json:
                            schema:
                                $ref: "#/components/schemas/ApiError"

components:
    parameters:
        ValidateResult:
            type: object
            additionalProperties: false
            required:
              - categories
              - items
            properties:
                categories:
                    type: array
                    description: Категории меню
                    items:
                        $ref: "#/components/schemas/ValidationCategory"
                items:
                    type: array
                    description: Список блюд доступных для заказа в ресторане
                    items:
                        $ref: "#/components/schemas/ValidationItem"

        ValidationCategory:
            type: object
            additionalProperties: false
            required:
              - id
              - name
              - status
            properties:
                id:
                    type: string
                    description: >-
                        Внутренний идентификатор категории в системе партнера.
                        Может быть любым значением, приводимым к строке.
                        Рекомендация - UUID4
                name:
                    type: string
                    description: Наименование категории (например "Супы")
                status:
                    $ref: "#/components/schemas/ValidationStatus"
                errors:
                    type: array
                    description: Ошибки валидации
                    items:
                        $ref: "#/components/schemas/ValidationError"

        ValidationItem:
            type: object
            additionalProperties: false
            required:
              - id
              - name
              - status
            properties:
                id:
                    type: string
                    description: >-
                        Внутренний идентификатор блюда в ресторане в системе
                        партнера. Может быть любым значением, приводимым к
                        строке. Рекомендация - UUID4
                name:
                    type: string
                    description: Наименование блюда в ресторане (например "Пирожки
                        с вишней")
                status:
                    $ref: "#/components/schemas/ValidationStatus"
                errors:
                    type: array
                    description: Ошибки валидации
                    items:
                        $ref: "#/components/schemas/ValidationError"

        ValidationError:
            type: object
            additionalProperties: false
            required:
              - code
            properties:
                code:
                    type: string
                    description: уникальный id ошибки
                    example: cant_add_an_ice_cream_dish
                message:
                    type: string
                    description: Человекочитаемое сообщение об ошибке
                    example: "Не подходит для доставки: не можем добавить блюдо с\
                        \ мороженым"

        ValidationStatus:
            type: string
            enum:
              - approved
              - rejected

        ApiError:
            type: object
            additionalProperties: false
            required:
              - code
              - message
            properties:
                code:
                    type: string
                message:
                    type: string

