# Surge pins MVP

## Обзор:
Предложения на перемещение в режиме SuperSurge доставляется на клиент в таком такой схеме:

```yaml
    v2.GenericMode:
        type: object
        additionalProperties: true
        x-taxi-additional-properties-true-reason: for allOf
        properties:
            restrictions:
                type: array
                items:
                    $ref: '#/definitions/v2.Restriction'
            submodes_info:
                $ref: '#/definitions/v2.SubmodesInfo'
            client_attributes:
                $ref: '#/definitions/v2.ClientAttributesMap'
            ready_panel:
                $ref: '#/definitions/v2.Section'
                description: Reposition title and description
            permitted_work_modes:
                type: array
                items:
                    type: string
        required:
          - restrictions
          - client_attributes
          - ready_panel
          - permitted_work_modes

    v2.OfferInfoMetadata:
        type: object
        additionalProperties: false
        properties:
            airport_queue_id:
                type: string
                description: Id of airport queue if offer to the airport

    v2.OfferInfo:
        type: object
        additionalProperties: true
        x-taxi-additional-properties-true-reason: for allOf
        properties:
            offered_at:
                type: string
                format: date-time
                description: Offer timestamp
            expires_at:
                type: string
                format: date-time
                description: Offer deadline
            image_id:
                type: string
                description: Offer icon id
            description:
                type: string
                description: Offer description
            destination_radius:
                type: number
                format: double
            restrictions:
                type: array
                items:
                    $ref: '#/definitions/v2.Restriction'
            metadata:
                $ref: '#/definitions/v2.OfferInfoMetadata'
        required:
          - offered_at
          - expires_at
          - image_id
          - description
          - destination_radius
          - restrictions

        V2RepositionOfferedModesResponse:
            type: object
            description: Offered modes
            additionalProperties:
                $ref: '#/components/schemas/V2RepositionOfferedModesMode'

        V2RepositionOfferedModesMode:
            allOf:
              - $ref: '../definitions.yaml#/definitions/v2.GenericMode'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: for allOf
                properties:
                    locations:
                        $ref: '#/components/schemas/V2RepositionOfferedModesOffers'
                required:
                  - locations

        V2RepositionOfferedModesOffers:
            type: object
            description: Offers map
            additionalProperties:
                $ref: '#/components/schemas/V2RepositionOfferedModesOffer'

        V2RepositionOfferedModesOffer:
            allOf:
              - $ref: '../definitions.yaml#/definitions/v2.OfferInfo'
              - type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: for allOf
                properties:
                    location:
                        $ref: '../definitions.yaml#/definitions/v2.PointLocation'
                required:
                  - location

```

В таком виде:
```js
{
    "SuperSurge": {
        "client_attributes": {
            "active_anchor_on_map": false,
            "active_cursor_model": "ARROW_ONLINE",
            ...
        },
        "locations": {
            "5xYRdG69MV0LbDzO": {
                "description": "Перемещайтесь к зоне спроса с заказами по пути",
                "destination_radius": 1200,
                "expires_at": "2022-02-24T01:25:16+00:00",
                "image_id": "star",
                "location": {
                    "address": {
                        "subtitle": "",
                        "title": ""
                    },
                    "id": "OjoQeZ4vgMV5bpZV",
                    "point": [
                        39.69660568237305,
                        47.24484634399414
                    ],
                    "type": "point"
                },
                "offered_at": "2022-02-24T01:22:17.187792+00:00",
                "restrictions": []
            }
        },
        "permitted_work_modes": [
            "orders"
        ],
        "ready_panel": {
            "subtitle": "В зону спроса",
            "title": "Проводник"
        },
        "restrictions": [
            {
                "image_id": "arrow_up",
                "short_text": "Получите приоритет",
                "text": "Получайте больше заказов в зоне высокого спроса",
                "title": "Приоритет"
            },
            {
                "image_id": "gift",
                "short_text": "Вам будет доступна точка Б",
                "text": "Вам будет видна конечная точка маршрута во всех заказах от Проводника",
                "title": "Открыта точка Б"
            }
        ]
    }
}
```

## Реализация пинов

### Вариант 1
Быстрый вариант для реализации MVP, срок ~1-2 недели на бэкенде + 2 недели на клиенте.
Предлагается обновить структуру OfferInfo, дополнив его:
* типом предложения (Regular, Pin);
* коэффициентом суржа в offer_metadata.

Сохраняется обратная совместимость с текущими версиями, на клиенте надо будет переписывать логику, когда в будущем переедем на пины, чтобы использовать конструктор.

```diff
diff --git a/taxi/uservices/services/reposition-api/docs/yaml/definitions.yaml b/taxi/uservices/services/reposition-api/docs/yaml/definitions.yaml
--- a/taxi/uservices/services/reposition-api/docs/yaml/definitions.yaml
+++ b/taxi/uservices/services/reposition-api/docs/yaml/definitions.yaml
@@ -703,23 +715,35 @@ definitions:
           - start_screen_usages
           - usage_limit_dialog
 ### v2/types/usages
 
  ### v2/types/offer
+    v2.OfferType:
+        type: string
+        enum:
+          - Regular
+          - Pin
+
     v2.OfferInfoMetadata:
         type: object
         additionalProperties: false
         properties:
+            surge_coefficient:
+                type: number
+                format: double
+                description: Destination surge
             airport_queue_id:
                 type: string
                 description: Id of airport queue if offer to the airport

     v2.OfferInfo:
         type: object
         additionalProperties: true
         x-taxi-additional-properties-true-reason: for allOf
         properties:
+            offer_type:
+                $ref: '#/definitions/v2.OfferType'
             offered_at:
                 type: string
                 format: date-time
                 description: Offer timestamp
             expires_at:
@@ -730,10 +754,12 @@ definitions:
                 type: string
                 description: Offer icon id
             description:
                 type: string
                 description: Offer description
             destination_radius:
                 type: number
                 format: double
             restrictions:
                 type: array
```

В таком виде:
```js
{
    "SuperSurge": {
        "client_attributes": {
            ...
        },
        "locations": {
            "5xYRdG69MV0LbDzO": {
                "description": "Перемещайтесь к зоне спроса с заказами по пути",
                "destination_radius": 1200,
                "expires_at": "2022-02-24T01:25:16+00:00",
                "image_id": "star",
                "location": {
                    "address": {
                        "subtitle": "",
                        "title": ""
                    },
                    "id": "OjoQeZ4vgMV5bpZV",
                    "point": [
                        39.69660568237305,
                        47.24484634399414
                    ],
                    "type": "point"
                },
                "metadata": {
                    "surge_coefficient": 1.5
                },
                "offered_at": "2022-02-24T01:22:17.187792+00:00",
                "restrictions": [],
                "start_button": {
                    "subtitle": "12 км * 9 мин",
                    "title": "Поехать с заказами по пути"
                }
            }
        },
        "permitted_work_modes": [
            "orders"
        ],
        "ready_panel": {
            "subtitle": "В зону спроса",
            "title": "Проводник"
        },
        "restrictions": [
            ...
        ]
    }
}
```

### Вариант 2
Нечто промежуточное между быстрым вариантом для MVP и хорошим вариантом с использованием конструктора, срок ~3-4 недели на бэкенде + 2 недели на клиенте.

В текущий ответ offered_modes к locations добавляется словарь pins, каждый value которого содержит location и constructor, который представляет собой UI, открываемый при нажатии на пин.

Сохраняется обратная совместимость с текущими версиями, на клиенте можно будет переиспользовать логику с конструктором, когда переедем на схему с пинами.

Схема:
```diff
diff --git a/taxi/uservices/services/reposition-api/docs/yaml/api/v2_reposition_offered_modes.yaml b/taxi/uservices/services/reposition-api/docs/yaml/api/v2_reposition_offered_modes.yaml
--- a/taxi/uservices/services/reposition-api/docs/yaml/api/v2_reposition_offered_modes.yaml
+++ b/taxi/uservices/services/reposition-api/docs/yaml/api/v2_reposition_offered_modes.yaml
@@ -81,19 +81,27 @@ components:
                 additionalProperties: true
                 x-taxi-additional-properties-true-reason: for allOf
                 properties:
                     locations:
                         $ref: '#/components/schemas/V2RepositionOfferedModesOffers'
+                    pins:
+                        $ref: '#/components/schemas/V2RepositionOfferedModesPins'
                 required:
                   - locations

         V2RepositionOfferedModesOffers:
             type: object
             description: Offers map
             additionalProperties:
                 $ref: '#/components/schemas/V2RepositionOfferedModesOffer'

+        V2RepositionOfferedModesPins:
+            type: object
+            description: Pins map
+            additionalProperties:
+                $ref: '#/components/schemas/V2RepositionOfferedModesPin'
+
         V2RepositionOfferedModesOffer:
             allOf:
               - $ref: '../definitions.yaml#/definitions/v2.OfferInfo'
               - type: object
                 additionalProperties: true
@@ -101,5 +109,24 @@ components:
                 properties:
                     location:
                         $ref: '../definitions.yaml#/definitions/v2.PointLocation'
                 required:
                   - location
+
+        V2RepositionOfferedModesPin:
+            type: object
+            description: Pins map
+            additionalProperties: false
+            properties:
+                location:
+                    $ref: '../definitions.yaml#/definitions/v2.PointLocation'
+                constructor:
+                    $ref: '#/components/schemas/V2RepositionOfferedModesPinConstructor'
+            required:
+              - location
+              - constructor
+
+        V2RepositionOfferedModesPinConstructor:
+            type: object
+            description: taximeter constructor object
+            additionalProperties: true
+            x-taxi-additional-properties-true-reason: taximeter-constructor
```

### Вариант 3
Реализовать вариант с конструктором отдельной от offered_modes ручкой, данные которой надо будет прокинуть в polling/order, новые версии клиента сразу могут использовать её (возможно, некоторое время параллельно, пока не откажемся от предложений в пользу пинов). Срок ~4-5 недель (~5-6 недель в случае перевода всех предложений – GeobookingOffers, Airport, ..., – на пины) на бэкенде + 2 недели на клиенте.

Схема ожидается похожей на схему offered_modes, лишь предложения будут заменены на пины-конструкторы, поэтому схема опущена. Текущие клиенты никак не будут затронуты.
