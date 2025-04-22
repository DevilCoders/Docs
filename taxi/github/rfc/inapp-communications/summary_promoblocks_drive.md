### Виджет для промо-блока Драйва

#### Дизайн
![drive_promo](https://jing.yandex-team.ru/files/pavelnekrasov/drive_widget_v2.jpg "drive_promo")

![drive_cashback](https://jing.yandex-team.ru/files/pavelnekrasov/drive_cashback.jpg "drive_cashback")

#### Виджет drive_arrow_button
Добавляет новый тип виджета `drive_arrow_button`
```json5
{
  "drive_arrow_button": {
    "layers_context": {
      "type": "drive_fixpoint_offers",
      "src": [
        33.33,
        55.55
      ],
      "dst": [
        33.307668,
        53.246202
      ],
      "offer_count_limit": 5,
      "preferred_car_number": "м668от799",
      "previous_offer_ids": [
        "offer_1",
        "offer_2"
      ],
      "items": [
        {
          "type": "image",
          "image_tag": "drive_car",
          "width": 15,
          "vertical_alignment": "center",
          "color": "#000000"
        }
      ]
    },
    "color": "afafaf"
  }
}
```

Если клиент поддерживает этот виджет, то в запросе должно быть указано:
```json5
{
  "client_info": {
    "supported_features": [
      {
        "type": "promoblock",
        "widgets": [
          "drive_arrow_button",
          ...
        ]
      }
    ],
    ...
  }
}
```

Важный момент, что виджет должен активироваться при нажатии на любую часть плашки
Драйва (не только на саму стрелочку)

Действия, по нажатию на виджет аналогичны шорткату Драйва 
(https://github.yandex-team.ru/taxi/rfc/blob/master/drive-shortcut/shortcut.md)
При нажатии на виджет идем в `/4.0/layers/v2/objects` с контекстом 
`layers_context` из шортката и `"mode": "drive"`, `"screen": "summary"`. Контекст должен быть передан 
в корне запроса в поле `"context"` **as-is** (т.е. при изменении формата 
контекста не нужно изменять клиентов)

Пример запроса:
 ```json
 {
  "context": {
    "type": "drive_fixpoint_offers",
    "src": [
      37.880318157794707,
      55.754543995739407
    ],
    "dst": [
      37.6425634912552,
      55.73475967775757
    ],
    "offer_count_limit": 5,
    "preferred_car_number": "м668от799",
    "previous_offer_ids": [
       "offer_1",
       "offer_2"
    ]
  },
  "state": {
    "bbox": [
      37.868574701220695,
      55.73813247694166,
      37.892082162849164,
      55.762261637963604
    ],
    "location": [
      37.88048333333333,
      55.755160000000004
    ],
    "mode": "drive",
    "screen": "summary",
    "zoom": 14.60303
  }
}
 ```
 
layers вернет все машинки на карте с прогруженными офферами. 
Клиент делает объект `selected_object_id` выбранным (как будто на него нажал 
пользователь) и центрирует карту на выбранном объекте с увеличением зума до 17.0. 
 При выборе объекта открывается карточка драйва из SDK с 
прогруженным оффером. При нахождении на экране с машинками фикса
все хождения в layers должны быть с контекстом.  


Если layers не вернул офферы, либо ручка objects не отвечает, нужно показать 
сообщение об ошибке и вернуться на саммари.


#### Пример промо-блока драйва
```json5
{
  "id": "5cc0e8eb0c69ff1a8a364b37",
  "title": {
    "items": [
      {
        "type": "text",
        "text": "На Драйве от 119 Р",
        "font_size": 14,
        "color": "#000000"
      }
    ]
  },
  "text": {
    "items": [
      {
        "type": "text",
        "text": "5 машин рядом",
        "font_size": 10,
        "color": "#000000"
      }
    ]
  },
  "cashback": {
    "amount": "10"
  },
  "widgets": {
    "drive_arrow_button": {
      "layers_context": {
        "type": "drive_fixpoint_offers",
        "src": [
          33.33,
          55.55
        ],
        "dst": [
          33.307668,
          53.246202
        ],
        "offer_count_limit": 5,
        "previous_offer_ids": [
          "offer_1",
          "offer_2"
        ]
      },
      "color": "afafaf",
      "items": [
        {
          "type": "image",
          "image_tag": "drive_car",
          "width": 15,
          "vertical_alignment": "center",
          "color": "#000000"
        }
      ]
    }
  }
}

```