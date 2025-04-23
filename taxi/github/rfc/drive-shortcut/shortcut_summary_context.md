## Продуктовая задача

### Описание

Научиться показывать цену для шортката Драйва.

#### Проблема

Ручка шортката и ручка драйв на саммари вызываются независимо и каждый раз запрашивают в драйве новые офферы.
При запуске цены на шорткате это приведет к расхождению цены на шорткате Драйва и на саммари для одной и той же машины.

#### Решение

Прокидываем контекст с id офферов Драйва из шорткатов в routestats. Согласовано здесь:
https://github.yandex-team.ru/taxi/rfc/blob/83846c4a8aa2e74465500f9785366ade0e3d9983/persuggest/drive_shortcut_price.md

Конкретнее:

Появляется поле summary_context, схема:

```yaml
SummaryContext:
        type: object
        additionalProperties: false
        properties:
            class:
                type: string
                enum:
                  - drive
            payload:
                type: object
                additionalProperties: false
                properties:
                    selected_offer_id:
                        type: string
                    previous_offer_ids:
                        type: array
                        items:
                            type: string
        required:
          - class
          - payload
```

#### Пример ответа ручки `4.0/persuggest/v2/shortcuts`

```json
{
  "scenario_tops": [
    {
      "scenario": "taxi_expected_destination",
      "shortcuts": []
    },
    {
      "scenario": "drive_fixpoint_offers",
      "shortcuts": [
        {
          "content": {
            "color": "#4d40f9",
            "overlays": [
              {
                "image_tag": "drive_shortcut_car",
                "shape": "car"
              },
              {
                "background": {
                  "color": "#4d40f8"
                },
                "image_tag": "shortcuts_work_userplace_tag",
                "shape": "poi"
              },
              {
                "attributed_text": {
                  "items": [
                    {
                      "color": "#57595C",
                      "font_style": "normal",
                      "font_weight": "regular",
                      "text": "74 ₽",
                      "type": "text"
                    }
                  ]
                },
                "background": {
                  "color": "#FFFFFF"
                },
                "shape": "label",
                "text": ""
              }
            ],
            "subtitle": "идти 9 мин",
            "title": "На работу на Драйве"
          },
          "id": "",
          "scenario": "drive_fixpoint_offers",
          "scenario_params": {
            "taxi_summary_redirect_params": {
              "class": "drive__т577нх799",
              "destination": {
                "log": "",
                "position": [
                  10.1,
                  20.2
                ],
                "uri": "ymapsbm1://URI_7_7"
              },
              "state": "collapsed",
              "summary_context": {
                "class": "drive",
                "payload": {
                  "previous_offer_ids": [
                    "3e29f7f7-8a7d26c2-4359f132-d6e0ee72"
                  ],
                  "selected_offer_id": "3e29f7f7-8a7d26c2-4359f132-d6e0ee72"
                }
              },
              "vertical": "drive",
              "vertical_trap": true
            }
          },
          "tags": [
            "tag1",
            "tag2"
          ]
        }
      ]
    }
  ]
}
```

#### Пример ответа ручки `/4.0/mlutp/v1/products`

```json
{
  "shortcut_id": "7e7233e1679d4b9a90c427258c69d993",
  "title": "Home",
  "subtitle": "16 min walk",
  "type": "action-driven",
  "width": 2,
  "height": 2,
  "background": {
    "color": "#DAE0F8"
  },
  "action": {
    "type": "taxi:summary-redirect",
    "vertical": "drive",
    "class": "drive__б448вг241",
    "state": "collapsed",
    "vertical_trap": false,
    "destination": {
      "position": [37.54346134911116, 55.68156951335919],
      "uri": "ymapsbm1://geo?ll=37.543%2C55.682&spn=0.001%2C0.001&text=%D0%A0%D0%BE%D1%81%D1%81%D0%B8%D1%8F%2C%20%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D0%B0%2C%20%D1%83%D0%BB%D0%B8%D1%86%D0%B0%20%D0%9F%D0%B0%D0%BD%D1%84%D1%91%D1%80%D0%BE%D0%B2%D0%B0%2C%2012%2C%20%D0%BF%D0%BE%D0%B4%D1%8A%D0%B5%D0%B7%D0%B4%204%20%7B3093975820%7D",
      "log": ""
    },
    "summary_context": {
      "class": "drive",
      "payload": {
        "previous_offer_ids": [
          "3e29f7f7-8a7d26c2-4359f132-d6e0ee72"
        ],
        "selected_offer_id": "3e29f7f7-8a7d26c2-4359f132-d6e0ee72"
      }
    }
  },
  "overlays": [{
    "shape": "car",
    "image_tag": "shortcuts_drive_car"
  }, {
    "shape": "poi",
    "background": {
      "color": "#A0B1F4"
    },
    "image_tag": "custom_shortcut_home_userplace_tag"
  }, {
    "text": "",
    "shape": "label",
    "background": {
      "color": "#FFFFFF"
    },
    "attributed_text": {
      "items": [{
        "type": "text",
        "text": "58 ₽",
        "font_weight": "regular",
        "font_style": "normal",
        "color": "#57595C"
      }]
    }
  }]
}
```