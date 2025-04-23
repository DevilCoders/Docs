### Описание

Необходимо возвращать подробную информацию по всем офферам в routestats.
Чтобы клиенты не ходили за ней в layers, сразу отображали все плашки. Так не будет заметна перерисовка одной плашки и замена ее на несколько плашек.
Достаточно возвращать SummarySelectorItem (из layers)
https://github.yandex-team.ru/taxi/uservices/blob/937bd31a9425d9516c5d7eeb09b398332358d8b9/schemas/services/layers/definitions.yaml#L1095

#### Важно: 
Делаем через конфиг 3.0, для клиентов старых версий возвращаем старый ответ, для клиентов новых версий возвращаем ответ, описанный ниже

### Пример информации по офферам в drive_extra
```json5

"drive_extra": {
  "layers_context": {...},
  "offers": [
    {
      "offer_id": "8f5764c2-8b1e3954-ad3ed28b-24e4541b",
      "base_service_level_class": "drive",
      "layers_extra": {
        "car_number": "т577нх799",
        "layers_object_id": "drive__т577нх799",
      },
      "service_level_override": {
        "brandings": [
          {
            "title": "Кэшбээк",
            "tooltip": {
              "text": "кэшбээк"
            },
            "type": "cashback",
            "value": "9"
          }
        ],
        "class": "drive__т577нх799",
        "description": "За 74 $SIGN$$CURRENCY$, ~8 мин",
        "description_parts": {
          "prefix": "",
          "suffix": "",
          "value": "74 $SIGN$$CURRENCY$"
        },
        "estimated_waiting": {
          "message": "идти 9 мин",
          "seconds": 540
        },
        "name": "Kaptur",
        "selector": {
          "icon": {
            "tag": "class_drive_icon_7"
          },
          "image": {
            "url": "https://carsharing.s3.yandex.net/drive/car-models/renault_kaptur/renault-kaptur-side-2-kaz_large.png"
          }
        },
        "subtitle": "Ждать 16 мин бесплатно",
        "title": "Далее"
      },
      "type": "summary"
    }
  ]
}
```

### Схема оффера
```yaml

Offer:
  type: object
  additionalProperties: false
  properties:
      offer_id:
          type: string
      type:
          type: string
          enum:
            - summary
      layers_extra:
                  type: object
                  additionalProperties: false
                  properties:
                      car_number:
                          type: string
                      layers_object_id:
                          description: |
                              Айди объекта для того, чтобы привязать тариф
                              к объекту
                          type: string
                  required:
                    - car_number
                    - layers_object_id
      base_service_level_class:
          description: базовый стиль, от которого нужно множить тарифы
          type: string
      service_level_override:
          type: object
          additionalProperties: false
          properties:
              class:
                  type: string
              name:
                  type: string
                  example: "X-Line"
              brandings:
                  type: array
                  items:
                      type: object
                      additionalProperties: false
                      properties:
                          type:
                              type: string
                              enum:
                                - cashback
                          value:
                              type: string
                          title:
                              type: string
                          tooltip:
                              type: object
                              additionalProperties: false
                              properties:
                                  text:
                                      type: string
                              required:
                                - text
                      required:
                        - type
                        - value
                        - title
                        - tooltip
              selector:
                  type: object
                  description: переопределяет иконку в селекторе тарифов
                  additionalProperties: false
                  properties:
                      icon:
                          type: object
                          additionalProperties: false
                          properties:
                              tag:
                                  type: string
                          required:
                            - tag
                      image:
                          type: object
                          description: |
                              Переопределяет большую картинку машины на
                              развернутой карточке
                          additionalProperties: false
                          properties:
                              url:
                                  type: string
                          required:
                            - url
                  required:
                    - icon
                    - image
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
                      Пеший маршрут до машины - отображается в карточке
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
                      Переопределяет description при уточнении точки B на
                      карте
                  example: "Поездка 194 $SIGN$$CURRENCY$, ~20 мин"
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
            - selector
            - description_parts
            - estimated_waiting
            - description
            - title

  required:
    - offer_id
    - type
    - base_service_level_class
    - service_level_override
    - layers_extra
```
