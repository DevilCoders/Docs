# Шорткат Еды

### Задача
[Самовывоз Еды на карте](https://st.yandex-team.ru/TAXIMOBILEDEV-842 )


### Дизайн
![Screenshot](static/eats_shortcut.png)
[Figma](https://www.figma.com/file/165RFmBXGLkB3uhd7M22YV/%D0%A1%D0%B0%D0%BC%D0%BE%D0%B2%D1%8B%D0%B2%D0%BE%D0%B7?node-id=2256%3A307823)


### Описание

Нужно добавить шорткат для отображения информации о ресторане Еды, при тапе на который открывается webview ресторана.


## Детализация решения 
Дизайн шорката отличается, поэтому предлагается ввести новый тип шортката: `action-driven-thumb`
Для данного типа шортката добавляется поле `thumb_background` - для картинки thumb
Для названия ресторана и подзаголовка: `attributed_title` и `attributed_subtitle` соответственно
Для оверлеев используются существующие `shape`, только в сочетании с типом шорката `action-driven-thumb` они располагаются в другом месте:
 - `shape=bubble` - в левом верхнем углу картинки thumb
 - `shape=corner_text` - в правом нижнем углу картинки thumb
Этот шорткат исполняет `action` любого типа, так же как `action-driven`

```yaml
OfferType:
    type: string
    enum:
        - taxi:expected-destination
        - deeplink
        - media-stories
        - invites
        - taxi:route-input
        - header-deeplink
        - eats-based:superapp
        - drive:fixpoint-offers
        - taxi:header-summary-redirect
        - header-action-driven
        - action-driven
        - action-driven-thumb
```
```yaml
OfferItemObject:
    type: object
    additionalProperties: false
    required:
    - width
    - height
    - title
    - type
    - shortcut_id
    - background
    - thumb_background
    properties:
        shortcut_id:
            type: string
        attributed_title:
            $ref: "extended-template/definitions.yaml#/definitions/AttributedText"
        title:
            type: string
        service:
            type: string
        icon_tag:
            type: string
        attributed_subtitle:
            $ref: "extended-template/definitions.yaml#/definitions/AttributedText"
        subtitle:
            type: string
        type:
            $ref: "#/definitions/OfferType"
        width:
            type: integer
            minimum: 0
        height:
            type: integer
            minimum: 0
        thumb_background:
            $ref: "#/definitions/BackgroundObject"
        background:
            $ref: "#/definitions/BackgroundObject"
        text_style:
            $ref: "#/definitions/TextPropertiesObject"
        action:
            $ref: "#/definitions/ActionObject"
        overlays:
            type: array
            items:
                $ref: "shortcuts/definitions.yaml#/definitions/OverlayObject"
        onboarding:
            $ref: "#/definitions/OnboardingObject"
```

Пример
```
**JSON:**
{
    "shortcut_id": "5b4788ed103b41888451e4addf2171c5",
    "attributed_title": {
        "items": [{
            "type": "text",
            "text": "Ведомости",
            "font_weight": "regular",
            "font_style": "normal",
            "color": "#57595C"
        }]
    },
    "attributed_subtitle": {
        "items": [{
            "type": "text",
            "text": "4.9 Отлично",
            "font_weight": "regular",
            "font_style": "normal",
            "color": "#57595C"
        }]
    },
    "type": "action-driven-thumb",
    "width": 6,
    "height": 3,
    "background": {
        "color": "#F5F2E4"
    },
    "thumb_background": {
        "color": "#F5F2E4",
        "image_url": "..."
    },
    "action": {
        "type": "deeplink",
        "url": "..."
    },
    "overlays": [{
        "shape": "bubble",
        "attributed_text": {
            "items": [{
                "type": "text",
                "text": "Готовят 15-20 мин",
                "font_weight": "regular",
                "font_style": "normal",
                "color": "#57595C"
            }]
        }
    }, {
        "shape": "corner_text",
        "attributed_text": {
            "items": [{
                "type": "text",
                "text": "150 м",
                "font_weight": "regular",
                "font_style": "normal",
                "color": "#57595C"
            }]
        }
    }]
}
```

### Флаг о поддержке новой функциональности

- В поле `supported_features` нужно отправить новый тип шортката

**JSON:**
```JavaScript
"supported_features": [
    {
        "type": "action-driven-thumb",
        "prefetch_strategies": [],
		"services": []
    },
    ...
]
```