# Внутреняя ручка получения айтемов из меню

Необходимо реализовать внутреннюю ручку, которая будет ходить за айтемами в `eats-rest-menu-storage`, добавлять наченки и скидки и возвращять эти айтемы с учетом расписания. Данная ручка будет запрашивать информацию об айтемах из одного плэйса.

### Проработка существующих запросов 

Так как данная ручка будет ходить в `eats-rest-menu-storage`, то для запроса в этот сервис необходимы следующие поля:
```
GetItemsRequest:
    required:
        - shipping_types
    properties:
        shipping_types:
            description: массив из способов доставки (delivery/pickup)
        places:
            description: массив из place_id и item_ids, в настоящем запросе будет использоваться один плэйс, в котором будут id всех айтемов в запросе
        legacy_ids:
            description: Идентификаторы товаров в коре, будут копироваться item_ids из предыдущего поля
        delivery_time:
            format: 'date-time'
```

В сервисе `eats-restaurant-menu` уже реализован поход за новыми скидками в классе `DiscountsHelper`. 
Для конструктора данного класса необходимы следующие данные:
```
const handlers::Dependencies& deps,
const experiments3::models::KwargsBuilderWithConsumer& kwargs,
        - для конструирования необходим авторизационный контекст пользователя
const std::string& slug,
        - place_slug для получения из кеша полной информации по place
const ::eats_authproxy_backend::AuthContext& eats_auth_context,
const std::vector<ItemsInfo>& items_info
```

В сервисе `eats-restaurant-menu` уже реализован поход за умными ценами в классе `SmartPricesHelper`. 
Для конструктора данного класса необходимы следующие данные:
```
const handlers::Dependencies& deps, 
const std::string& slug,
        - place_slug для получения из кеша полной информации по place
const ::eats_authproxy_backend::AuthContext& eats_auth_context
```

### Api новой ручки:
```
openapi: 3.0.0
info:
    description: Yandex Taxi eats-restaurant-menu Service
    title: Yandex Taxi eats-restaurant-menu Service
    version: '1.0'

# Not used in codegen
servers:
  - url: eats-restaurant-menu.eda.yandex.net
    description: production

x-taxi-middlewares:
    tvm: true


x-taxi-client-qos:
    taxi-config: EATS_RESTAURANT_MENU_CLIENT_QOS

paths:
    /api/v1/menu/get-items:
        post:
            x-taxi-middlewares:
                eats: v1
            description: |
                Получение информации о блюдах ресторана по их id.
            parameters:
              - name: x-request-id
                in: header
                description: Идентификатор запроса
                schema:
                    type: string
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/GetItemsRequest'
            responses:
                '200':
                    description: Данные по товарам
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/GetItemsResponse'
                '400':
                    description: Ошибка обработки запроса
                    content:
                        application/json:
                            schema:
                                $ref: '#/components/schemas/GetItemsErrorResponse'

components:
    schemas:
        GetItemsRequest:
            type: object
            additionalProperties: false
            required:
              - shipping_type
              - place_slug
            properties:
                shipping_type:
                    $ref: "../definitions.yaml#/components/schemas/ShippingType"
                place_slug:
                    type: string
                    description: Слаг ресторана
                places:
                    type: array
                    description: Сейчас для запросов использоваться не будет, так как в корзине числовые идентификаторы айтемов
                    items:
                        $ref: "#/components/schemas/GetItemsPlaceRequest"
                legacy_ids:
                    type: array
                    description: будет использоваться как основное поле для передачи id айтемов
                    items:
                        type: integer
                        format: int64
                        description: Идентификаторы товаров в коре
                delivery_time:
                    type: string
                    format: 'date-time'
        
        GetItemsPlaceRequest:
            type: object
            additionalProperties: false
            required:
              - place_id
              - items
            properties:
                place_id:
                    type: string
                    description: Идентификатор заведения
                items:
                    type: array
                    minItems: 1
                    items:
                        $ref: "../definitions.yaml#/components/schemas/ItemId"

        GetItemsResponse:
            type: object
            additionalProperties: false
            required:
              - place_id
              - items
            properties:
                place_id:
                    type: string
                    description: Идентификатор заведения
                items:
                    type: array
                    description: Данные идентификаторы являются строковыми и выдаются сервисом eats-rest-menu-storage 
                    items:
                        $ref: "../definitions.yaml#/components/schemas/Item"

        GetItemsErrorResponse:
            type: object
            additionalProperties: false
            required:
              - error
              - message
            properties:
                error:
                    description: |
                        Машинночитаемый код ошибки
                          - validation_error - ошибка валидации
                          - place_menu_items_not_found - какие-то из переданных id айтемов не были найдены
                          - different_places_forbidden - нельзя получить данные по айтемам из разных плейсов
                          - not_found_place - плейс не найден
                          - not_found_brand - бренд не найден
                    type: string
                    enum:
                      - validation_error
                      - place_menu_items_not_found
                      - different_places_forbidden
                      - not_found_place
                      - not_found_brand
                message:
                    description: Человекочитаемое сообщение об ошибке
                    type: string

        Item:
            type: object
            additionalProperties: false
            required:
              - id
              - origin_id
              - name
              - adult
              - shipping_types
              - price
              - available
            properties:
                id:
                    type: string
                origin_id:
                    type: string
                name:
                    type: string
                adult:
                    type: boolean
                shipping_types:
                    $ref: "../definitions.yaml#/components/schemas/ShippingType"
                legacy_id:
                    type: integer
                    format: int64
                    description: Идентификатор блюда в коре
                description:
                    type: string
                weight_unit:
                    type: string
                    description: Тип измерения веса
                weight_value:
                    $ref: "../definitions.yaml#/components/schemas/WeightValue"
                pictures:
                    $ref: "../definitions.yaml#/components/schemas/Pictures"
                vat:
                    $ref: "../definitions.yaml#/components/schemas/Vat"
                options_groups:
                    type: array
                    items:
                        $ref: "../definitions.yaml#/components/schemas/OptionsGroup"
                price:
                    $ref: "../definitions.yaml#/components/schemas/Price"
                available:
                    type: boolean
                    description: Доступность товара
                promo_price:
                    $ref: "../definitions.yaml#/components/schemas/Price"
                ordinary:
                    type: boolean
                choosable:
                    type: boolean
                stock:
                    type: integer
                    description: Остатки блюда
                short_name:
                    type: string
                    description: Сокращенное имя блюда
                categories_ids:
                    type: array
                    items:
                        $ref: "../definitions.yaml#/components/schemas/CategoryIds"
                    description: Айди из коры и из сервиса категорий айтема
```

Далее описание вспомогательных типов, которые будут лежать в "../definitions.yaml" и объединены с уже существующими структурами
```
        ItemId:
            type: string
            description: Строковый идентификатор блюда из сервиса eats-rest-menu-storage

        WeightValue:
            type: string
            x-taxi-cpp-type: decimal64::Decimal<3>
            pattern: '^-?[0-9]+(\.[0-9]{1,3})?$'
            description: Значение веса

        Vat:
            type: string
            x-taxi-cpp-type: decimal64::Decimal<2>
            pattern: '^-?[0-9]+(\.[0-9]{1,2})?$'

        Pictures:
            type: array
            items:
                type: object
                additionalProperties: false
                required:
                  - url
                properties:
                    url:
                        type: string
                    avatarnica_identity:
                        type: string
                    ratio:
                        type: number
                        format: double
                    sort:
                        type: integer  

        OptionsGroup:
            type: object
            additionalProperties: false
            required:
              - id
              - origin_id
              - name
            properties:
                id:
                    type: string
                origin_id:
                    type: string
                is_required:
                    type: boolean
                    default: false
                name:
                    type: string
                legacy_id:
                    type: integer
                    format: int64
                sort:
                    type: integer
                min_selected_options:
                    type: integer
                max_selected_options:
                    type: integer
                options:
                    type: array
                    items:
                        $ref: "#/components/schemas/Option"
                deactevated_at:
                    type: string
                    format: date-time

        Option:
            type: object
            additionalProperties: false
            required:
              - id
              - name
              - origin_id
              - multiplier
              - available
            properties:
                id:
                    type: string
                name:
                    type: string
                origin_id:
                    type: string
                multiplier:
                    type: integer
                legacy_id:
                    type: integer
                    format: int64
                min_amount:
                    type: integer
                max_amount:
                    type: integer
                price:
                    $ref: "#/components/schemas/Price"
                promo_price:
                    $ref: "#/components/schemas/Price"
                vat:
                    $ref: "#/components/schemas/Vat"
                sort:
                    type: integer
                available:
                    type: boolean
                deactevated_at:
                    type: string
                    format: date-time

        Price:
            type: string
            x-taxi-cpp-type: decimal64::Decimal<2>
            pattern: '^-?[0-9]+(\.[0-9]{1,2})?$'

        CategoryIds:
            type: object
            additionalProperties: false
            required:
              - id
            properties:
                id:
                    type: string
                legacy_id:
                    type: integer
                    format: int64
```
