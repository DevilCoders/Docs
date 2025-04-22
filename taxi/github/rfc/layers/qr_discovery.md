## Дизайн

![qr-discovery](https://jing.yandex-team.ru/files/pavelnekrasov/qr_design_final.png "Дискавери QR")

### Клиентский эксперимент
Режим дискавери для QR включается через клиентский эксперимент `qr_discovery`.
(Консюмер `client-superapp-misc/availability`). Эксперимент:
```json
{
  "enabled": true,
  "l10n": {
    "qr_layers_unavailability_message": "Попробуйте повторить" //описание ниже
  }
}
```

### Хождения в layers
Экран discovery для QR очень похож на экран discovery для Драйва/Транспорта.

Клиент должен ходить в layers с `"screen": "discovery", "mode": "qr"`.

На экране disсovery должен быть поддержан `optimal_view` и отображение ошибки 
`no_objects_message`. Также при отстутствии объектов присылается 
`no_object_subtitle`.

Пример выдачи ответа без объектов:
```json5
{
  "bbox": [...],
  "clean_sec": 86400,
  "features": [],
  "optimal_view": {
    "no_objects_message": "Нет ресторанов поблизости",
    "no_objects_subtitle": "Можно подвигать карту, вдруг повезет"
  },
  "throttle_ms": 100,
  "type": "FeatureCollection",
  "validity_sec": 86400,
  "zooms": [
    15.0,
    21.0
  ]
}
```
 
Если layers не отвечает, либо 500-тит, то нужно отобразить ошибку с текстом 
из qr_discovery.l10n.qr_layers_unavailability_message
с кнопкой `Повторить`.

### Доработки объекта из layers

#### Overlay
Для объекта в layers добавляется новое свойство `Overlay`. См. подробное описание 
в файлике overlay.md. `Overlay` нужен для того, чтобы отображать
кэшбэк для ресторана. 

#### Новый экшн OrganizationCardAction

Добавляется новый экшн OrganizationCardAction. По этому экшну нужно сходить 
в ручку `/4.0/layers/v1/organization` с содержимым экшна и открыть карточку 
организации. Подробное описание в файлике `organization_card.md`.

```yaml
OrganizationCardAction:
    type: object
    additionalProperties: false
    description: |
        По  данному экшну нужно открыть карточку QR-объекта
    properties:
        type:
            type: string
            enum:
              - organization_card
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
    required:
      - type
      - id
```

Пример:
```json5
{
   "type": "organization_card",
   "id": {
     "type": "qr",
     "value": "1234567"
   },
   "mode": "suggest"
}
```

#### Новый тип лэйбла

Добавляется новый лэйбл - `poi` - подпись для организации (без фона). 
Цвет текста задается в поле `color`. Лэйбл скрывается, если объект выбран.
```json
    "label": {
      "type": "poi",
      "text": "Кофемания",
      "color": "AFAFAF",
      "zooms": [15, 21]
    }
```

#### Префикс для аппметрики

Вместе с объектом передается `appmetrica_prefix` (https://st.yandex-team.ru/ITAXI-10079).
Для ресторанов QR это будет `QrRestaraunt` (???)


#### Пример QR-ресторана для кэшбэка
```json5
{
  "type": "Feature",
  "id": "qr_123456",
  "geometry": {
    "type": "Point",
    "coordinates": [
      37.5893,
      55.7342
    ]
  },
  "properties": {
    "appmetrica_prefix": "QrRestaraunt",
    "display_settings": {
      "z_index": 210,
      "zooms": [10, 21],
      "simplified_zoom": 15
    },
    "options": [
      {
        "actions": [
          {
            "type": "organization_card",
            "id": {
              "type": "qr",
              "value": "123456" 
            },
            "mode": "suggest"
          }
        ],
        "on": "tap"
      }
    ],
    "style": {
      "image": {
        "type": "tag",
        "name": "qr_restaraunt",
        "anchor": [
            0.5, 0.5
        ]
      },
      "selected_image": {
        "type": "tag",
        "name": "selected_qr_restaraunt",
        "anchor": [
            0.5, 0.7
        ]     
      }
    },
    "simplified_style": {
      "image": {
        "type": "tag",
        "name": "qr_restaraunt_simplified"
      },
      "selected_image": {
        "type": "tag",
        "name": "selected_qr_restaraunt",
        "anchor": [
            0.5, 0.7
        ]     
      }
    },
    "overlays": [
      {
          "shape": "rounded_rectangle",
          "zooms": [15, 21],
          "anchor": [0.5, 0.8],
          "attributed_text": {
            "items": [
              {
                "type": "text",
                "text": "10%", 
                "font_size": 12,
                "meta_color": "plus_text"
              }
            ]
          },
          "show_states": ["unselected"],
          "background": {
            "color": "FFFFFF"
          }
      }
    ],
    "label": {
      "type": "poi",
      "text": "Кофемания",
      "color": "AFAFAF",
      "zooms": [15, 21]
    }
  }
}

```








