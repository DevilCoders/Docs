# Интеграция shuttle в routestats

Проект "Шаттл" хочется интегрировать в Summary по аналогии с Драйвом, поскольку изначально "цикл заказа" будет другим:
- Пользователь указывает точки А и Б
- routestats идет в сервис shuttle-control и, в случае нахождения "удачного" попутного маршрута получает данные по остановкам, и шаттлу
- клиентское приложение отображает остановки А и Б, пеший маршрут до А, и кнопку "забронировать место"

Кажется, что order_flow всегда будет другим (даже после того, как Шаттл станет "платным", появится необходимость оплаты, и так далее), поскольку логически пользователю нужно показывать другой UI - пеший маршрут до А, причем А - не точка, которую он указал (а ближайшая остановка). С точкой Б тоже самое.

## Этапы реализации

1. Заводится фиктивный тариф shuttle
2. Для него устанавливается отдельный order_flow (shuttle)
3. Разрабатывается плагин shuttle_order_flow для routestats, который ходит в shuttle-control с примерным API:
```
GET internal/v1/shuttle-control/v1/routestats:
{
  "route": [ // Точки А и Б, при наличии промежуточных точек в первой ревизии запрос не выполняется
    [33.0, 55.0],
    [34.0, 55.0]
  ],
  // Параметры, берущиеся из эксперимента в плагине shuttle_order_flow
  "pickup_parameters": {
    "max_walk_time_s": 180,
    "max_walk_distance_m": 480,
    "max_wait_time": 180
  },
  "dropoff_parameters": {
    "max_walk_time_s": 180,
    "max_walk_distance_m": 480,
    "max_wait_time": 180
  }
}

Response:
[
{
  "offer_id": "4323213213", // В shuttle stage 3 (с оплатой)
  "shuttle_id": "niceshuttle",
  "route_id": "avrora_city",
  "pickup_stop_id": "10",
  "dropoff_stop_id": "10",
  "eta_s": 180,
  "route_info": {
    "time_s": 1200,
    "distance_m": 3000
  }
}
]
```

4. Изменение протокола routestats:

services/routestats/docs/yaml/definitions.yaml:
```
definitions:
    ServiceLevel:
        type: object
        additionalProperties: true
        x-taxi-additional-properties-true-reason: plugins
        description: положение селектора
        properties:
            class:
                $ref: "#/definitions/TariffClass"
                description: категория тарифа
            is_fixed_price:
                type: boolean
                description: признак фикс-прайса
            description_parts:
                $ref: "#/definitions/DescriptionParts"
            tariff_unavailable:
                $ref: "#/definitions/TariffUnavailable"
            title:
                type: string
            subtitle:
                type: string
            brandings:
                type: array
                items:
                    $ref: "#/definitions/ServiceLevelBranding"
            estimated_waiting:
                $ref: "#/definitions/EstimatedWaiting"
            selector:
                $ref: "definitions/drive_order_flow.yaml#/definitions/ServiceLevelSelector"
            drive_extra:
                description: |
                    Дополнительные поля, необходимые для категорий с
                    order_flow=drive.
                $ref: "definitions/drive_order_flow.yaml#/definitions/DriveExtra"
            delivery_extra:
                description: |
                    Дополнительные поля, необходимые для категорий с
                    order_flow=delivery.
                $ref: "definitions/delivery_order_flow.yaml#/definitions/DeliveryExtra"
            shuttle_extra:
                description: |
                    Дополнительные поля, необходимые для категорий с order_flow=shuttle.
                $ref: "definitions/shuttle_order_flow.yaml#/definitions/ShuttleExtra

```

services/routestats/docs/yaml/definitions/shuttle_order_flow.yaml:
```
definitions:
    ShuttleOffer:
        type: object
        additionalProperties: false
        properties:
            shuttle_id:
                type: string
                description: Идентификатор шаттла для вызова ручки /book
                    Идеологически эти три идентфикатора будут заменены на offer_id в следующей итерации
                    при добавлении оплаты.
            route_id:
                type: string
                description: Идентификатор маршрута для вызова ручки /book
            stop_id:
                type: string
                description: Идентификатор остановки для вызова ручки /book
            type:
                type: string
                enum:
                  - summary
            base_service_level_class:
                description: базовый стиль, от которого нужно множить тарифы (shuttle)
                type: string
            layers_extra:
                type: object
                additionalProperties: false
                properties:
                    line_id:
                        description: |
                            Айди маршрута для того, чтобы подсветить маршрут шаттла
                            (line_id)
                        type: string
                    pickup_stop_id:
                        description: |
                            Айди объекта для того, чтобы привязать тариф
                            к объекту (id остановки посадки)
                        type: string
                    dropoff_stop_id:
                        description: |
                            Айди объекта для того, чтобы привязать тариф
                            к объекту (id остановки высадки)
                        type: string
                required:
                  - line_id
                  - pickup_stop_id
                  - dropoff_stop_id
            service_level_override:
                type: object
                additionalProperties: false
                properties:
                    class:
                        type: string
                    name:
                        type: string
                        example: "Аврора - Сити"
                    description_parts:
                        type: object
                        description: |
                            Переопределяет цену в селекторе тарифов и на
                            развернутой карточке
                        additionalProperties: false
                        properties:
                            prefix:
                                type: string
                            suffix:
                                type: string
                            value:
                                type: string
                                example: "194 $SIGN$$CURRENCY$"
                        required:
                          - prefix
                          - suffix
                          - value
                    estimated_waiting:
                        type: object
                        description: |
                            ETA шаттла на остановке посадки
                        additionalProperties: false
                        properties:
                            seconds:
                                type: integer
                            message:
                                type: string
                        required:
                          - seconds
                          - message
                    description:
                        type: string
                        description: |
                            Переопределяет description (?)
                    title:
                        type: string
                    subtitle:
                        type: string
                        description: |
                            Сабтайтл кнопки заказа (title будет в
                            service_level-е routestats)
                required:
                  - class
                  - name
                  - description_parts
                  - estimated_waiting
                  - description
                  - title
        required:
          - shuttle_id
          - route_id
          - stop_id
          - layers_extra
          - type
          - base_service_level_class
          - service_level_override

    ShuttleExtra:
        type: object
        additionalProperties: false
        properties:
            layers_context:
                type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: |
                    формат задается кодегеном сервиса layers
            offers:
                type: array
                description: список всех попутных офферов Шаттла
                items:
                    $ref: "#/definitions/ShuttleOffer"
        required:
          - layers_context
          - offers
```

5. Клиент при нажатии на тарифф с order_flow=shuttle запрашивает сервис layers с указанным layers_context, и получает маршрут шаттла и остановки посадки-высадки.
Из сервиса layers ему приходит selected_object_id=pickup_stop_id, с action=walk_route.

Офферов может быть несколько, поскольку может быть несколько подходящих маршрутов.
6. При нажатии на кнопку "забронировать" клиент идет в shuttle-control с набором {route_id, stop_id, shuttle_id} и бронирует место.
