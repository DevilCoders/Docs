# Попутчики в тарифе комбо

## Где отправляем инфу о попутчиках?

В корень ответа ручки /3.0/taxiontheway добавляем массив `companions` (TBD):
```yaml
TaxiOnTheWayResponse:
    type: object
    additionalProperties: false
    properties:
        companions:
            type: array
            items:
                $ref: "#/definitions/Companion"
```

На экране мультизаказа клиент добавляет карточки попутчиков над карточкой заказа комбо снизу вверх. То есть последний элемент в массиве `companions`
должен быть самым верхним на экране пользователя.
Каждый объект массива содержит `header` (то, что выше разделительной черты) и `body` (то, что ниже разделительной черты).
Если `body` отсутствует, то разделительная черта не отображается.

Если в хедере попутчика присутствует `"car": {"show": true}`, то берем форматирвоанный номер и иконку машины, которые уже были получены из totw.

Полное описание схемы попутчика:
```yaml
definitions:
    ShowFullScreenAction:
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - show_fullscreen
            fullscreen:
                type: object
                additionalProperties: false
                properties:
                    id:
                        type: string
                required:
                  - id
        required:
          - type
          - fullscreen_id
    
    Action:
        oneOf:
          - $ref: "#/definitions/ShowFullScreenAction"
    
    Actions:
        type: array
        items:
            $ref: "#/definitions/Action"
    
    Shevron:
        type: object
        additionalProperties: false
        properties:
            actions:
                $ref: "#/definitions/Actions"
        required:
          - actions
    
    Car:
        type: object
        additionalProperties: false
        properties:
            show:
                type: boolean
        required:
          - show

    HeaderDetails:
        description: |
            All `required` elements from companion's header go to details card.
            Here we describe additional companion's elements in details card
        type: object
        additionalProperties: false
        properties:
            image:
                type: object
                additionalProperties: false
                properties:
                    image_tag:
                        type: string
                required:
                  - image_tag

    CompanionHeader:
        type: object
        additionalProperties: false
        properties:
            title:
                type: object
                additionalProperties: false
                properties:
                    text:
                        type: string
                    shimmering:
                        type: boolean
                required:
                  - text
                  - shimmering
            subtitle:
                type: object
                additionalProperties: false
                properties:
                    text:
                        type: string
                required:
                  - text
            car:
                $ref: "#/definitions/Car"
            shevron:
                $ref: "#/definitions/Shevron"
            details_card:
                $ref: "#/definitions/HeaderDetails"
        required:
          - title
          - subtitle
    
    AttributedTextItem:
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - text
            text:
                type: string
            font_size:
                type: integer
            font_weight:
                type: string
                enum:
                  - regular
                  - light
                  - medium
                  - bold
                  - display-heavy
            font_style:
                type: string
                enum:
                  - normal
                  - italic
            color:
                type: string
                pattern: "^#?[0-9a-zA-Z]{6}"
        required:
          - type
          - text
    
    AttributedImageItem:
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - image
            image_tag:
                type: string
            width:
                type: integer
            vertical_alignment:
                type: string
                enum:
                  - baseline
                  - center
            color:
                type: string
                pattern: "^#?[0-9a-zA-Z]{6}"
        required:
          - type
          - image_tag
    
    AttributedItem:
        oneOf:
          - $ref: "#/definitions/AttributedTextItem"
          - $ref: "#/definitions/AttributedImageItem"
    
    AttributedContent:
        type: object
        additionalProperties: false
        properties:
            items:
                type: array
                items:
                    $ref: "#/definitions/AttributedItem"
        required:
          - items
    
    ArrowButton:
        type: object
        additionalProperties: false
        properties:
            text:
                $ref: "#/definitions/AttributedContent"
            actions:
                $ref: "#/definitions/Actions"
        required:
          - text
          - actions
    
    Feedback:
        type: object
        additionalProperties: false
        properties:
            enabled:
                type: boolean
            rating_value:
                type: integer
                minimum: 1
                maximum: 5
        required:
          - enabled
    
    CompanionBody:
        type: object
        additionalProperties: false
        properties:
            text:
                $ref: "#/definitions/AttributedContent"
            arrow_button:
                $ref: "#/definitions/ArrowButton"
        required:
          - text
    
    Companion:
        type: object
        additionalProperties: false
        properties:
            header:
                $ref: "#/definitions/CompanionHeader"
            body:
                $ref: "#/definitions/CompanionBody"
            feedback:
                $ref: "#/definitions/Feedback"
        required:
          - header
```

Примеры:

* Поиск попутчика

![поиск попутчика](./search.png) 

```json
{
  "companions": [
    {
      "header": {
        "title": {
          "text": "Поиск попутчика",
          "shimmering": true
        },
        "subtitle": {
          "text": "По дороге к вам присоединится попутчик"
        },
        "details_card": {
          "image": {
            "image_tag": "companion_image_for_details_card"
          }
        }
      },
      "body": {
        "text": {
          "items": [
            {
              "type": "text",
              "text": "Тариф `С попутчиком`"
            }
          ]
        },
        "arrow_button": {
          "text": {
            "items": [
              {
                "type": "text",
                "text": "Подробнее",
                "color": "#9E9B98",
                "font_size": 13
              }
            ],
            "actions": [
              {
                "type": "show_fullscreen",
                "fullscreen": {
                  "id": "combo_fullscreen_id"
                }
              }
            ]
          }
        }
      }
    }
  ]
}
```

* Ждём, когда присоединится попутчик

![ждем попутчика ](./waiting.png)

```json
{
  "companions": [
    {
      "header": {
        "title": {
          "text": "Попутчик",
          "shimmering": false
        },
        "subtitle": {
          "text": "Присоединится через 5 минут"
        },
        "car": {
          "show": true
        },
        "shevron": {
          "actions": [
            {
              "type": "show_fullscreen",
              "fullscreen": {
                "id": "combo_fullscreen_id"
              }
            }
          ]
        },
        "details_card": {
          "image": {
            "image_tag": "companion_image_for_details_card"
          }
        }
      }
    }
  ]
}
```

* Едем с попутчиком

![в пути](./driving.png)

```json
{
  "companions": [
    {
      "header": {
        "title": {
          "text": "Попутчик",
          "shimmering": false
        },
        "subtitle": {
          "text": "Выйдет через 2 минуты"
        },
        "car": {
          "show": true
        },
        "shevron": {
          "actions": [
            {
              "type": "show_fullscreen",
              "fullscreen": {
                "id": "combo_fullscreen_id"
              }
            }
          ]
        },
        "details_card": {
          "image": {
            "image_tag": "companion_image_for_details_card"
          }
        }
      },
      "feedback": {
        "enabled": true
      }
    }
  ]
}
```

* Несколько попутчиков в списке

![несколько](./many_companions.png)

```json
{
  "companions": [
    {
      "header": {
        "title": {
          "text": "Первый попутчик",
          "shimmering": false
        },
        "subtitle": {
          "text": "Уже вышел"
        },
        "shevron": {
          "actions": [
            {
              "type": "show_fullscreen",
              "fullscreen": {
                "id": "combo_fullscreen_id"
              }
            }
          ]
        },
        "details_card": {
          "image": {
            "image_tag": "companion_image_for_details_card"
          }
        }
      },
      "feedback": {
        "enabled": true
      }
    },
    {
      "header": {
        "title": {
          "text": "Второй опутчик",
          "shimmering": false
        },
        "subtitle": {
          "text": "Присоединится через 1 минуту"
        },
        "car": {
          "show": true
        },
        "shevron": {
          "actions": [
            {
              "type": "show_fullscreen",
              "fullscreen": {
                "id": "combo_fullscreen_id"
              }
            }
          ]
        },
        "details_card": {
          "image": {
            "image_tag": "companion_image_for_details_card"
          }
        }
      }
    }
  ]
}
```
