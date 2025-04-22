## Описание
Для отображения карточки ресторанов (в т.ч. QR), а также для режима поиска на 
карте из саджеста добавляем сущность - карточка организации.

Примеры карточек:

![](https://jing.yandex-team.ru/files/pavelnekrasov/organization_card_short.png "Карточка организации 1")
![](https://jing.yandex-team.ru/files/pavelnekrasov/organization_card_full.png "Карточка организации 2")


## Карточка организации
Карточка состоит из модулей:
```json5
{
  "organization": {
    "title": <attributed_text>,
    "subtitle": <attributed_text>,
    "images": [...],
    "list_items": [...],
    "buttons": [...]
  }
}
```

Подробное описание каждого из модулей приведено дальше.

#### title/subtitle
Оба поля представляют собой attributed_text.  См. файлик `attributed_text.md`.

#### images
Список картинок `images`. Если картинок несколько и клиент не поддерживает 
отображение нескольких картинок, то отображается первая картинка. 
Если картинку не удалось подгрузить, то она не отображается. Соответственно, 
если ни одну картинку не удалось подгрузить, то в карточке не отображается секция 
с картинками (т.е. сразу title/subtitle).


Схема элемента `images`:

```yaml
Image:
  type: object
  additionalProperties: false
  properties:
    image_url:
      type: string
    image_tag:
      type: string
```

Пример images:
```
  "images": [
    {
      "image_url": "1234566"
    },
    {
      "image_url": "789"
    }
  ]
```

#### list_items
Список `list_items` состоит из кликабельных элементов. Пример: элемент 
`Сканировать счет` в дизайне.
Элемент состоит из `lead` части  - все, что слева: иконка, тайтл, сабтайтл и
`trail` части: индикатор (шеврон), размер кэшбэка. 

Элемент имеет следующую схему:

```yaml
ListItem:
    type: object
    additionalProperties: false
    properties:
      lead:
        type: object
        additionalProperties: false,
        properties:
            icon:
                type: object
                properties:
                    image_tag:
                        type: string
                    image_url:
                        type: string
                additionalProperties: false
            title:
                $ref: "#/definitions/AttributedText"
            subtitle:
                $ref: "#/definitions/AttributedText"
        required:
          - title
      trail:
        type: object
        additionalProperties: false
        properties:
          indicator:
            type: object
            additionalProperties: false
            properties:
              type:
                type: string
                enum:
                  - chevron
            required:
              - type
          cashback:
            type: object
            additionalProperties: false
            properties:
              style:
                type: string
                enum:
                  - light
                  - dark
              value:
                type: string
            required:
              - style
              - value
      action:
        $ref: '#/definitions/Action' // <- смотри ниже варианты экшнов
    required:
      - lead
      - action
```

Пример элемента:
```json5
{
   "lead": {
       "icon": {
         "image_tag": "qr_scan_tag"
       },
       "title": {
         "items": [
            {
              "type": "text",
              "text": "Сканировать счет",
              "font_size": 16,
              "color": "21201F"
            }
         ]
       }
   },
   "action": {
     "type": "qr_scan"
   },
   "trail": {
      "indicator": {
        "type": "chevron"
      },
      "cashback": {
        "style": "light",
        "value": "15%"
      }
   }
}
```

Если `action` не поддержан на клиенте, то элемент не нужно отображать
Если `trail.indicator.type` не поддержан на клиенте, то элемент не нужно отображать.

#### buttons
Список кнопок. Кнопка задается стилем (фон, текст) и действием (`action`) по 
нажатию на кнопку. Также для кнопки задается размер `size`: `auto` или `square`.
Размер `auto` подразумевает, что размер кнопки подстраивается под все доступное 
место. Размер `square` подразумевает, что кнопка должна быть квадратной.

Последовательность отображения кнопок:
1. Валидируются экшны в кнопках. Если экшн в кнопке не поддерживается, 
то кнопка игнорируется.
2. Рассчитывается максимальное количество `N` квадратных кнопок, которое 
можно отобразить. Если число кнопок превышает `N`, то список кнопок обрезается 
до `N`.
3. Если в списке нет `auto` кнопок, то первая кнопка в списке становится `auto`.
4. Рассчитывается размер `auto` кнопки - из общей ширины вычитаются 
все квадратные кнопки и оставшееся место делится между на количество `auto` 
кнопок 
5. Кнопки отображаются.

Схема кнопки:
```yaml
Button:
    type: object
    additionalProperties: false
    properties:
        background:
            type: object
            additionalProperties: false
            properties:
                color:
                    type: string
                meta_color:
                    $ref: '#/definitions/MetaColor'
                image_tag:
                    type: string
        title:
            $ref: "#/definitions/AttributedText"
        subtitle:
            $ref: "#/definitions/AttributedText"
        action:
            $ref: '#/definitions/Action' // <- смотри ниже варианты экшнов
    required:
      - background
      - title
      - action
```

Пример кнопки:
```json5
{
  "size": "auto",
  "title": {
    "items": [
      {
        "type": "image",
        "image_tag": "car_image_tag"
      },
      {
        "type": "text",
        "text": "Поехать",
        "font_size": 16,
        "color": "21201F"
      }
    ]
  },
  "background": {
    "color": "FCE000"
  },
  "action": {
    "type": "taxi_route",
    "dst": {
      "position": [37.5, 55.5],
      "finalsuggest_log": "xxxx"
    }
  }
}
```


### Экшны в карточке организации
Экшн в карточке организации имеет следующую схему:
```yaml
Action:
    oneOf:
      - $ref: "#/definitions/QrScanAction"
      - $ref: "#/definitions/TaxiRouteAction"
      - $ref: "#/definitions/WalkRouteAction"
      - $ref: "#/definitions/PhoneCallAction"
      - $ref: "#/definitions/DeeplinkAction"
```


#### QrScanAction
По данному экшну необходимо открыть экран сканирования QR-кода для оплаты в 
ресторане

Схема:
```yaml
QrScanAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - qr_scan
```
Пример:
```json5
{
  "type": "qr_scan"
}
```

#### TaxiRouteAction
По данному экшну необходимо выполнить финализацию точки `dst` из экшна и открыть 
саммари (аналог диплинка `taxi_route`). По финализацией понимается запрос в 
ручку `/4.0/persuggest/v1/finalsuggest` с `action: finalize` (`position` и 
`prev_log` берутся из экшна).

Схема:
```yaml
TaxiRouteAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - taxi_route
        dst:
            type: object
            additionalProperties: false
            properties:
                position:
                    $ref: "#/definitions/Position" // [37.5, 55.5]
                prev_log:
                    type: string
                    description: поле prev_log для финализации адреса dst    
            required:
              - position
    required:
      - type
      - dst
```

Пример:
```json5
{
    "type": "taxi_route",
    "dst": {
      "position": [37.5, 55.5],
      "prev_log": "xxxx"
    }
}
```

#### WalkRouteAction
По данному экшну необходимо построить маршрут от локации пользователя до точки 
`dst` из экшна. Данный экшн валиден только при доступной локации пользователя в 
сценарии работы с картой (т.е. карточка организации открыта на карте). 

Схема:
```yaml
WalkRouteAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - walk_route
        dst:
            type: object
            additionalProperties: false
            properties:
                position:
                    $ref: "#/definitions/Position" // [37.5, 55.5]
            required:
              - position
    required:
      - type
      - dst
```
Пример:
```json5
{
    "type": "walk_route",
    "dst": {
      "position": [37.5, 55.5]
    }
}
```

#### PhoneCallAction
По данному экшну необходимо позвоните по номеру телефона из экшна. 
Данный экшн валиден только если приложение может звонить.

Схема:
```yaml
PhoneCallAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - phone_call
        number:
            type: string
            example: +74951234567
    required:
      - type
      - number
```
Пример:
```json5
{
  "type": "phone_call",
  "number": "+74951234567"
}
```

#### DeeplinkAction
По данному экшну необходимо открыть диплинк из экшна

Схема:
```yaml
DeeplinkAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - deeplink
        deeplink:
            type: string
    required:
      - type
      - deeplink
```
Пример:
```json5
{
  "type": "deeplink",
  "number": "yandextaxi://xxxx"
}
```


## Ручка /4.0/layers/v1/organization
Для получения карточки организации нужно дернуть ручку 
`/4.0/layers/v1/organization`.

Ручка принимает на вход айди организации запрашиваемой карточки, режим `mode`, 
а также `state` с текущим состоянием приложения. На текущий момент в `state` 
передается только опциональное поле `location` (нужно для того, чтобы 
посчитать расстояние до организации, которое отображается в карточке):
```
POST /4.0/layers/v1/organization
{
  "id": {
    "type": "geosearch/qr",
    "value": "12312341"
  },
  "mode": "suggest", //<- опциональное поле
  "state": {
    "location": [37.5, 55.5]
  }
}
```

Для айди организации добавляется тип айдишника - `geosearch` или `qr`. 
Тип нужен для того, чтобы можно было запросить информацию об организации по 
разным типам айдишников. Поле `mode` нужно для того, чтобы фильтровать поля 
карточки в зависимости от текущего режима. Если `mode` не задан, то возвращается 
полная карточка.

Ручка отвечает в формате:
```json5
{
   "organization": {
       //карточка организации 
   }
}
```

Схема запроса:
```yaml
OrganizationCardRequest:
  type: object
  additionalProperties: false
  properties:
    id:
      type: object
      additionalProperties: false
      properties:
        type:
          type: string
          enum:
            - qr
            - geosearch
          value:
            type: string
      required:
        - type
        - value
    mode:
      type: string
    state:
      type: object
      additionalProperties: false
      properties:
        location:
          $ref: "#/definitions/Position" // [37.5, 55.5]
  required:
    - id
    - state  
```


#### Пример ответа ручки 

```json
{
  "organization": {
      "images": [
        {
          "image_url": "xxxxxx"
        }
      ],
      "title": {
        "items": [
          {
            "type": "text",
            "text": "Tilda",
            "font_size": 24,
            "color": "21201F"
          }
        ]
      },
      "subtitle": {
        "items": [
          {
            "type": "text",
            "text": "до 22:30 · 1,5 км · Садовническая 82с2",
            "font_size": 13,
            "color": "9E9B98"
          }
        ]
      },
      "list_items": [
        {
           "lead": {
               "icon": {
                 "image_tag": "qr_scan_tag"
               },
               "title": {
                 "items": [
                    {
                      "type": "text",
                      "text": "Сканировать счет",
                      "font_size": 16,
                      "color": "21201F"
                    }
                 ]
               }
           },
           "action": {
             "type": "qr_scan"
           },
           "trail": {
              "indicator": {
                "type": "chevron"
              },
              "cashback": {
                "style": "light",
                "value": "15%"
              }
           }
        }
      ],
      "buttons": [
        {
          "size": "auto",
          "title": {
            "items": [
              {
                "type": "image",
                "image_tag": "car_image_tag"
              },
              {
                "type": "text",
                "text": "Поехать",
                "font_size": 16,
                "color": "21201F"
              }
            ]
          },
          "background": {
            "color": "FCE000"
          },
          "action": {
            "type": "taxi_route",
            "dst": {
              "position": [37.5, 55.5],
              "prev_log": "xxxx"
            }
          }
        },
        {
          "size": "square",
          "title": {
            "items": [
              {
                "type": "image",
                "image_tag": "walk_route_tag"
              }
            ]
          },
          "background": {
            "color": "F1F0ED"
          },
          "action": {
            "type": "walk_route",
            "dst": {
              "position": [37.5, 55.5]
            }
          }
        },
        {
          "size": "square",
          "title": {
            "items": [
              {
                "type": "image",
                "image_tag": "call_tag"
              }
            ]
          },
          "background": {
            "color": "F1F0ED"
          },
          "action": {
            "type": "phone_call",
            "number": "+74951234567"
          }
        }
      ]
    }
 }
```

#### Обработка ошибок
Если организацию не удалось найти, то ручка вовзвращает ошибку 404:

```json5
{
  "code": "organization_not_found",
  "message": "Organization not found",
  "details": {
    "subtitle": "Try later" <- Опциональное поле
  }
}
```

Вместо карточки нужно отобразить:
- message - тайтл
- subtitle - опциональный сабтайтл
- кпопку `Попробовать еще раз`


![](https://jing.yandex-team.ru/files/pavelnekrasov/error_screen.png "Не найдено")


Если ручка таймаутит или 500-тит, то нужно отобразить кнопку `Попробовать еще раз` и 
дефолтный тайтл "Не смогли загрузить".

