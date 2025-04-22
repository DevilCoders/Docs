### Какую задачу решаем

Хотим возвращать в шорткатах Драйва цену. 
Сейчас данные для шортката забираются из ручки /offers/{offer_type}.

#### Проблема

Информация для шортката запрашивается из метода /offers/{offer_type}, после чего с шортката происходит редирект на саммари,
где в routestats делается запрос ручки /offers/{offer_type} снова. 
В результате можем получить разный список офферов (разные цены, разные машинки).

#### Как решаем

Чтобы гарантировать идентичный набор офферов драйва для шортката и для саммари, достаточно зафиксировать список id офферов 
и передать их в запросе в routestats, где будем делать запрос за офферами с учетом известных offer_ids.
Для этого в ответе /4.0/persuggest/v2/shortcuts в taxi_summary_redirect_params возвращаем summary_context
с информацией о полученных офферах (ранее также передавалась информация для layers, сейчас на новых клиентах не используется).

Клиенты забирают из `shortcuts.scenario_params.taxi_summary_redirect_params(drive_fixpoint_offers_params).summary_context`
объект целиком и добавляют его в массив `summary_context.by_classes` на вход routestats. 
Переданные данные учтутся при запросе в Драйв.

#### Важно

Возможно, контекст для routestats имеет смысл вынести в корень, т.к. хочется также поддержать цену для шорткатов Такси.
Дизайн тут: https://www.figma.com/file/W8oInUTbSrUNsH1g8grbDD/%D0%98%D0%BD%D1%82%D0%B5%D0%B3%D1%80%D0%B0%D1%86%D0%B8%D1%8F-%D0%94%D1%80%D0%B0%D0%B9%D0%B2%D0%B0?node-id=4424%3A43317

### Пример ответа /4.0/persuggest/v2/shortcuts 
```json5
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
              }
            ],
            "subtitle": "идти 9 мин",
            "title": "На работу на Драйве"
          },
          "id": "",
          "scenario": "drive_fixpoint_offers",
          "scenario_params": {
            "taxi_summary_redirect_params": {
              "summary_context": {
                "class" : "drive",
                "payload": {
                  "selected_offer_id": "Selected",
                  "previous_offer_ids": [
                    "selected",
                    "other"
                  ]
                }
              },
              "class": "drive_cargo",
              "destination": {
                "log": "",
                "position": [
                  10.1,
                  20.2
                ],
                "uri": "ymapsbm1://URI_7_7"
              },
              "state": "collapsed",
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

### Пример запроса в /v1/routestats
```json5
{
  "extended_description": true,
  "format_currency": true,
  "id": "eeeeeeeeeeeeeeeeeeeeeeeeeeeeeee0",
  "is_lightweight": false,
  "payment": {
    "payment_method_id": "card-eeeeeeeeeeeeeeeeeeeeeeeee",
    "type": "card"
  },
  "position_accuracy": 0,
  "route": [
    [
      37.587569,
      55.733393
    ],
    [
      37.687569,
      55.633393
    ]
  ],
  "selected_class_only": false,
  "size_hint": 320,
  "skip_estimated_waiting": false,
  "state": {
    "fields": [
      {
        "title": "point_a_title",
        "type": "a"
      },
      {
        "title": "point_b_title",
        "type": "b"
      }
    ],
    "location": [
      37.5,
      55.5
    ]
  },
  "summary_version": 2,
  "supported_markup": "tml-0.1",
  "supports_explicit_antisurge": true,
  "supports_hideable_tariffs": true,
  "supports_multiclass": true,
  "supports_no_cars_available": true,
  "supports_paid_options": true,
  "surge_fake_pin": false,
  "summary_context": {
    // base summary stuff
    
    // summary staff by classes
    "by_classes": [ {
      "class": "drive",
      "payload": {
        // drive shortcuts context   
        "selected_offer_id": "Selected",
        "previous_offer_ids": ["selected", "other"],
        
        // drive summary context (TAXIBACKEND-33780)
        "seen_car_order": [
          "а123вс777",
          "е555ее777"
        ],
      }
    }]
  },
  "tariff_requirements": [
    {
      "class": "drive",
    },
    {
      "class": "econom"
    },
    {
      "class": "business"
    }
  ],
  "with_title": true,
  "zone_name": "ekb"
}


```