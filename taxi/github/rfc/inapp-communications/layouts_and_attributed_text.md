## Attributed Text

В связи с багом при построении html на платформе iOS возникла необходимость в использовании т.н. Attributed Text (или AT). Данный механизм позволяет кастомизировать строку на клиентах. А именно, отображать последовательность из текста, неразделимых пробелов, переносов строк, ссылок и изображений как одну строку. Каждый элемент данной последовательности может иметь свои собственные параметры, независимые от других элементов последовательности.

## Использование AT в ручках сервиса `inapp-communications`.

Отметим, что все текстовые поля со временем должны стать AT (сейчас по сути это просто текст с цветом и типом `small`/`large`).

### Пайплайн построения AT из `TypedContentWidget`

На данный момент все коммуникации, приходящие из `promotions` в ручке `/internal/promotions/list`, хранятся в кеше в том виде, в каком пришли. `inapp-communications` во многих клиентских ручках производит персонализацию строк (сейчас это поход в танкер и yql-подстановка). К этому списку добавляется построение AT с помощью библиотеки `extended-template`. В существующее api сервиса `promotions` для историй, фуллскринов, карточек и нотификаций добавляется булево поле `is_attributed_text`. 
Описание возможных случаев для конкретного поля типа `TypedWidgetContent`:
| коммуникация is_attributed_text           | поле is_tanker_key  | смысл content |
|-------------|-----| -----|
| нет | нет | контент с потенциальной html-разметкой, логика прежняя |
| да | нет | AT-разметка |
| нет | да | танкерный ключ, по которому потенциально лежит html-разметка, логика прежняя |
| да |  да | танкерный ключ, по которому лежит AT-разметка |

### Истории в ответе ручки `/4.0/promotions/v1/promotion/retrieve`

Текущий формат stories, отдаваемый в ручке `/4.0/promotions/v1/promotion/retrieve`:
```json5
{
  "id": "8ae4ef0ac1a94270bd36eeb3f1eb8337:a25ae2",
  "options": {
    "activate_condition": {
      "screen": [
        "pickup_location"
      ]
    },
    "communication_type": "story",
    "end_date": "2021-10-23T08:11:00.000000Z",
    "meta_type": "media_stories",
    "priority": 4000,
    "start_date": "2020-10-23T08:11:00.000000Z",
    "zones": [
    ]
  },
  "payload": {
    "is_tapable": true,
    "pages": [
      {
        "autonext": true,
        "layout": { // optional - без этого поля, стандартный шаблон истории
          "id": "main|main_with_top_inset|bottom", // идентификатор лейаута, известный клиенту
                        // если бэк отдал неизвестный лейаут, использовать стандартный
                        // предлагается держать знание о доступности лейаута на той или иной версии клиента на бэке (а не supported_layouts в запросе) 
        },
        "backgrounds": [
          {
            "content": "https://taxi-promotions.s3.yandex.net/8c6b1597cdf44bc9b92cfadbe0b087e9.jpg",
            "type": "image"
          }
        ],
        "duration": 15,
        "widgets": {
          "action_buttons": [
          ],
          "close_button": {
            "color": "21201f"
          }
        }
      },
      {
        "autonext": true,
        "backgrounds": [
          {
            "content": "https://taxi-promotions.s3.yandex.net/997ae75d2e064df589cd494724c820b2.jpg",
            "type": "image"
          }
        ],
        "duration": 15,
        "widgets": {
          "action_buttons": [
          ],
          "close_button": {
            "color": "21201f"
          }
        }
      },
      {
        "autonext": true,
        "backgrounds": [
          {
            "content": "https://taxi-promotions.s3.yandex.net/180d50fe39854ad7bc9a9fa648d64e1c.jpg",
            "type": "image"
          }
        ],
        "duration": 15,
        "widgets": {
          "action_buttons": [
          ],
          "close_button": {
            "color": "21201f"
          }
        }
      },
      {
        "autonext": true,
        "backgrounds": [
          {
            "content": "https://taxi-promotions.s3.yandex.net/28cae3eb1dcc4b63b3d239c06b33d2a4.jpg",
            "type": "image"
          }
        ],
        "duration": 15,
        "widgets": {
          "action_buttons": [
          ],
          "close_button": {
            "color": "21201f"
          }
        }
      },
      {
        "autonext": true,
        "backgrounds": [
          {
            "content": "https://taxi-promotions.s3.yandex.net/9851fd362ce54af88b23728e31e960a3.jpg",
            "type": "image"
          }
        ],
        "duration": 15,
        "widgets": {
          "action_buttons": [
          ],
          "close_button": {
            "color": "21201f"
          }
        }
      }
    ],
    "preview": {
      "backgrounds": [
        {
          "content": "https://taxi-promotions.s3.yandex.net/fb652dcb5d804528980f997915eeaa35.jpg",
          "type": "image"
        },
        {
          "content": "DCA070",
          "type": "color"
        },
        {
          "content": "https://taxi-promotions.s3.yandex.net/fb652dcb5d804528980f997915eeaa35.jpg",
          "type": "image_url"
        }
      ],
      "text": {
        "color": "FFFFFF",
        "content": "<b>Я нашёл человека</b>"
      },
      "title": {
        "color": "FFFFFF",
        "content": "Водитель"
      }
    }
  },
  "type": "story"
}
```

Текущие действия виджета:
```yaml
WidgetAction:
    type: object
    properties:
        type:
            type: string
            enum:
              - deeplink
              - move
              - share
              - web_view
              - screenshare
        payload:
            oneOf:
              - $ref: '#/definitions/ActionPayload'
              - $ref: '#/definitions/MoveActionPayload'
    required:
      - type
      - payload
    additionalProperties: false
```

Пример действия виджета:
```json5
{
    "type": "web_view",
    "payload": {
        "content": "https://music.yandex.ru/iframe/#album/3880967/?utm_source=go_main&utm_medium=non_music&utm_campaign=go_main_plus&utm_content=white_noise&utm_term=podcast",
        "need_authorization": true
    }
}
```
Для screenshare
```json5
{
    "type": "screenshare",
    "payload": {
        "content": "",
        "need_authorization": false
    }
}
```

Передаваемый текст (было, без AT):
```yaml
TypedContentWidget:
    type: object
    properties:
        content:
            type: string
        color:
            type: string
        type:
            type: string
            enum:
              - small
              - large
    required:
      - content
      - color
    additionalProperties: false
```
Пример старого:
```json5
{
    // ...
    "title": {
        "content": "<b>для детей</b>",
        "color": "FFFFFF"
    }
    // ...
}
```

Передаваемый текст (стало, с AT):
```yaml
TypedContentWidget:
    type: object
    properties:
        attributed_text: '#/definitions/AttributedText'
        content:
            type: string
        color:
            type: string
        type:
            type: string
            enum:
              - small
              - large
    required:
      # required теперь нет, так как либо attributed_text возвращается, либо content + color + type
    additionalProperties: false
```

Пример нового (вариант 1):
```json5
{
    "title": {
      "attributed_text": {
         "items": [
            {
                "type": "image", 
                "image_tag": "ets_badge_icon",
                "width": 15,
                "vertical_alignment": "center",
                "color": "#000000",
            },
            {
                "type": "text", 
                "text": "Еда: доставка за N минут",
                "font_size": 14,
                "font_weight": "bold",
                "font_style": "italic",
                "color": "#000000"
            }
        ]
      }
    } 
}
```

Пример нового (вариант 2):
```json5
{
    // ...
    "title": {
        "attributed_text": {
            "items": [
                {
                    "type": "text",
                    "text": "Подписка за ",
                    "meta_style": "body",
                    "meta_color": "text-main"
                },
                {
                    "type": "text",
                    "text": "баллы",
                    "meta_style": "body",
                    "meta_color": "plus"
                },
            ]
        }
    }
    // ...
}
```

Пример нового (вариант 3):
```json5
{
    // ...
    "title": {
        "attributed_text": {
            "items": [
                {
                    "type": "text",
                    "text": "Смотри ",
                    "meta_style": "body",
                    "meta_color": "text-main"
                },
                {
                    "type": "link",
                    "link": "https://here.ru",
                    "text": {
                        "type": "text",
                        "text": "здесь",
                        "meta_style": "body",
                        "meta_color": "plus"
                    }
                }
            ]
        }
    }
    // ...
}
```

### Истории в ответе ручки `/4.0/inapp-communications/shortcuts`:

Истории, получаемые напрямую из сервиса `promotions` представляются в виде шортката (используется только превью истории, страницы игнорируются, но в ходе построения сервис проверяет, что история будет полностью построена при запросе через `/4.0/promotions/v1/promotion/retrieve`, т.е. поход в танкер, подстановка AT и yql-подстановка будут произведены успешно) и отдаются в сервис `shortcuts` через ручку `api-proxy`. 

Пример ответа ручки с текущим форматом:
```json5
{
  "scenario_tops": [
    {
      "scenario": "grocery_blocks_other",
      "shortcuts": [
        {
          "content": {
            "color": "#FFFFFF",
            "image_url": "https://taxi-promotions-testing.s3.mdst.yandex.net/f425a4f8e8204a9d8a94c3d271b206b2.jpg",
            "subtitle": "love you",
            "text_color": "#000000",
            "title": "Герой Яндекс Go"
          },
          "id": "d144737936064a51ae9de2acaa17c68c",
          "scenario": "grocery_blocks_other",
          "scenario_params": {
            "media_stories_params": {
              "action_type": "media_stories",
              "promo_id": "42a32c7afc21484881f9b6eab368d7bc:efd2c1"
            }
          }
        }
      ]
    }
  ]
}
```

Пример ответа ручки в новом формате, использующем AT:
```json5
{
  "scenario_tops": [
    {
      "scenario": "grocery_blocks_other",
      "shortcuts": [
        {
          "content": {
            "color": "#FFFFFF",
            "image_url": "https://taxi-promotions-testing.s3.mdst.yandex.net/f425a4f8e8204a9d8a94c3d271b206b2.jpg",
            "attributed_subtitle": {
              "items": [
                {
                  "type": "text",
                  "text": "love you",
                  "font_style": "italic",
                  "font_weight": "bold",
                  "color": "000000" // клиенты должны уметь парсить цвет без решётки
                }
              ]
            },
            "attributed_title": {
              "items": [
                {
                  "type": "text",
                  "text": "Герой Яндекс Go",
                  "font_style": "italic",
                  "font_weight": "bold",
                  "color": "000000" // клиенты должны уметь парсить цвет без решётки
                }
              ]
            }
          },
          "id": "d144737936064a51ae9de2acaa17c68c",
          "scenario": "grocery_blocks_other",
          "scenario_params": {
            "media_stories_params": {
              "action_type": "media_stories",
              "promo_id": "42a32c7afc21484881f9b6eab368d7bc:efd2c1"
            }
          }
        }
      ]
    }
  ]
}
```

Новые должны уметь поддерживать и старый формат (`title`/`subtitle`), и новый (`attributed_title`/`attributed_subtitle`). Это связано с тем, что для промок с `is_attributed_text: false` будут заполняться только старые поля, для промок с `is_attributed_text: true` будут заполняться новые поля. `title`/`subtitle` остаются на беке для обратной совместимости (источники шорткатов, отличные от `inapp-communications`, не умеют работать с AT).

### Другие коммуникации

Фуллскрины, карточки и нотификации, отдаваемые в ручке `/4.0/promotions/v1/promotion/retrieve`, также переводим на AT. В полях типа `TypedContentWidget` также добавляем секцию `attributed_text`.
