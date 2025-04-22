#### Описание

attributed_text уже используется в шорткатах и в промке на саммари.
Для удобства в этом файлике продублирована схема для AttributedText.

#### Схема attributed_text

```yaml
    AttributedText:
        type: object
        additionalProperties: false
        properties:
            items:
                type: array
                items:
                    oneOf:
                      - $ref: "#/definitions/ATText"
                      - $ref: "#/definitions/ATImage"
        required:
          - items

    MetaColor:
        type: string
        description: | 
              мета цвет
              plus - цвет "кнопка плюса"
              plus_text - цвет "текст плюса"
        enum:
            - plus
            - plus_text 

    ATText:
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
                pattern: "^#[0-9A-Z]{6}"
            meta_color:
                $ref: '#/definitions/MetaColor'
        required:
          - type
          - text

    ATImage:
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
                pattern: "^#[0-9A-Z]{6}"
            meta_color:
                $ref: '#/definitions/MetaColor'
        required:
          - type
          - image_tag

```


#### Пример attributed_text
```
{
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
      },
      {
        "type": "text",
        "text": "сюда",
        "font_size": 16,
        "font_weight": "medium",
        "meta_color": "plus_text"
      }
    ]
}
```




