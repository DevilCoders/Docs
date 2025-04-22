### Описание

Для объекта layers добавляется новое свойство для отображения - Overlay.
Теперь вместе с объектом в properties может приходить список overlays.

Пример оверлея - закругленный прямоугольник для отображения кэшбэка плюса.

Оверлей использует `attributed_text` - такой же как в шорткатах и промо-плашках (см. схему в файлике `attributed_text`)

Пока поддерживается только оверлей с `"shape": "rounded_rectangle"` (закругленный прямоугольник с тенью).
Размер оверлея выравнивается по содержимому `attributed_text`.

![overlay](https://jing.yandex-team.ru/files/pavelnekrasov/overlay.png "Оверлей")

### Пример оверлея для QR-ресторана

```json5

{
  "type": "Feature",
  "id": "fbb68f7f0391464092812bcef420a829_2",
  "geometry": {
    "type": "Point",
    "coordinates": [
      37.5893,
      55.7342
    ]
  },
  "properties": {
    ...,
    "overlays": [
      {
          "shape": "rounded_rectangle", <- закругленный прямоугольник
          "zooms": [15, 21],
          "anchor": [0.5, 0.8], <- положение центра оверлея относительно объекта
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
          "show_states": ["unselected"], <- список состояний объекта, в которых нужно показывать оверлей
          "background": {
            "color": "FFFFFF"
          }
      }
    ],
    ...
  }
}

```

### Схема оверлея
```yaml

    Overlay:
        type: object
        additionalProperties: false
        properties:
            shape:
                type: string
                enum:
                  - rounded_rectangle
            zooms:
                description: |
                    диапазон зумов, в котором отображается оверлэй.
                    Если объект находится в выбранном состоянии, то поле
                    zooms игнорируется
                $ref: "#/definitions/Zooms"
            anchor:
                description: положение центра оверлэя относительно точки [0, 0]
                $ref: "#/definitions/Anchor"
            attributed_text:
                $ref: "#/definitions/AttributedText" // <-- схема в файлике attributed_text.md
            show_states:
                type: array
                items:
                    type: string
                    enum:
                        - unselected
                        - selected
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
        required:
          - shape
          - zooms
          - anchor
          - show_states

    Anchor:
        type: array
        items:
            type: number
        minItems: 2
        maxItems: 2

    Zooms:
        type: array
        description: интервал зумов
        items:
            type: number
        minItems: 2
        maxItems: 2
        example: "[15, 20]"

```






