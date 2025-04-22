### Что хотим

Хотим возможность анимированого бэкграунда шортката (для беспилотника — волны, исходящие из лидара).

![animated_shortcut.png](animated_shortcut.png)

### Что предлагаем
Сейчас поле ```background``` в корне шортката выглядит так:
```yaml
BackgroundObject:
  type: object
  additionalProperties: false
  properties:
    color:
        type: string
    image_url:
        type: string
    image_tag:
        type: string
    alt_text:
        type: string
  required:
    - color
```

Предлагается расширить поле ```background``` в корне шортката, чтобы поддерживать параметры анимации.

### Пример

```yaml
ShortcutBackgroundPulseAnimation:
  type: object
  additionalProperties: false
  properties:
      id:
        type: string
      type:
        type: string
        enum:
          - pulse_circles
      count:
        description: сколько раз отображается анимация (за жизнь приложения)
        type: integer
      delay:
        description: задержка перед анимацией (мс)
        type: number
      source:
        type: object
        additionalProperties: false
        properties:
          color:
            type: string
          duration:
            type: number
          delay_per_circle:
            type: number
          circle_count:
            type: integer
          anchor:
            type: object
            additionalProperties: false
            properties:
              shape:
                type: string
                enum:
                  - car
                  - poi
                  - sticker
                  - bubble
              point:
                type: object
                description: |
                  Точка, за которую цепляется якорь
                additionalProperties: false
                properties:
                  x:
                    type: number
                    minimum: 0
                    maximum: 1
                  y:
                    type: number
                    minimum: 0
                    maximum: 1
                required:
                  - x
                  - y
            required:
              - shape
              - point
        required:
          - color
          - duration
          - delay_per_circle
          - circle_count
          - anchor
  required:
    - id
    - type
    - count
    - delay
    - source


BackgroundObject:
  type: object
  additionalProperties: false
  properties:
    color:
      type: string
    image_url:
      type: string
    image_tag:
      type: string
    alt_text:
      type: string
    animation:
      oneOf:
        - $ref: '#/ShortcutBackgroundPulseAnimation'
      discriminator:
        propertyName: type
        mapping:
          pulse_circles: '#/ShortcutBackgroundPulseAnimation'
  required:
    - color
```

```json
{
  "background": {
    "color": "#F2E7E7",
    "animation": {
      "id": "sdc_onboarding_animation",
      "type": "pulse_circles",
      "source": {
        "color": "#FFFFFF",
        "anchor": {
          "shape": "car|poi|sticker|bubble",
          "point": {
            "x": 0.5, // range (0.0 to 1.0)
            "y": 0.0 // range (0.0 to 1.0)
          }
        },
        "delay_per_circle": 500,
        "circle_count": 3,
        "duration": 3000 //ms
      },
      "count": 3,
      "delay": 2.0
    }
  }
}
```

Весь шорткат:
```json
{
  "shortcut_id": "df9eb7e0b3094933a956427f96de2a33",
  "title": "Домthfrr",
  "type": "taxi:expected-destination",
  "width": 2,
  "height": 2,
  "background": {
    "color": "#F2E7E7",
    "animation": {
      "id": "sdc_onboarding_animation",
      "type": "pulse_circles",
      "source": {
        "color": "#FFFFFF",
        "anchor": {
          "shape": "car|poi|sticker|bubble",
          "point": {
            "x": 0.5, // range (0.0 to 1.0)
            "y": 0.0 // range (0.0 to 1.0)
          }
        },
        "duration": 3000 //ms
      },
      "count": 3,
      "delay": 2.0
    }
  },
  "action": {
    "position": [
      37.534405,
      55.750027
    ],
    "log": "{\"type\":\"userplace\",\"userplace_id\":\"home\",\"tags\":[\"userplace\",\"userplace_home\"]}",
    "uri": "ymapsbm1://geo?ll=37.534%2C55.750&spn=0.001%2C0.001&text=%D0%A0%D0%BE%D1%81%D1%81%D0%B8%D1%8F%2C%20%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D0%B0%2C%201-%D0%B9%20%D0%9A%D1%80%D0%B0%D1%81%D0%BD%D0%BE%D0%B3%D0%B2%D0%B0%D1%80%D0%B4%D0%B5%D0%B9%D1%81%D0%BA%D0%B8%D0%B9%20%D0%BF%D1%80%D0%BE%D0%B5%D0%B7%D0%B4%2C%2021%D1%811"
  },
  "overlays": [
    {
      "shape": "poi",
      "background": {
        "color": "#C4BFA7"
      },
      "image_tag": "custom_shortcut_home_userplace_tag"
    }
  ]
}
```