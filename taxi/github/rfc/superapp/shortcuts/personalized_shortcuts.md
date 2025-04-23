# Персонализированные шорткаты

### Задача
[GODEVPROJECTS-51: Персонализированные шорткаты маркета в нативной шторе и на главной](https://st.yandex-team.ru/GODEVPROJECTS-51 )


### Figma
[Макеты секции и шорткатов](https://www.figma.com/file/DAk0OApRgm9d7bGeccuJcN/%F0%9F%9B%8D-%D0%9C%D0%B0%D1%80%D0%BA%D0%B5%D1%82-Express-%E2%86%92-Go)


### Верхнеуровневое описание

Хотим научиться рисовать секцию с новым типом шорткатов и кнопкой, по которой будет выполняться определенный Action


## Детализация решения 

### Флаг о поддержки новой функциональности

Клиент должен прислать следующие параметры
- В поле `supported_sections` новый тип секции
- В поле `supported_features` новый тип объекта секции

**JSON:**
```JavaScript
"supported_sections": [
    "horizontal_stack_section",
    ...
],
"supported_features": [
    {
        "type": "vertical_stack_item"
        "items": [{
            "type": "info"
        },{
            "type": "rating"
        },{
            "type": "thumb"
        }]
    },
    ...
]
```

### Секция

<img src="./static/personalized_shortcuts_section_mockup.png">

Секция выглядит как `items_horizontal_scrollable_grid`, поэтому можем использовтаь его как основу, но не переиспользовать, так как поведение отличается:
- Скролл не должен появляться если все элементы помещаются на экран
- Элементы должны растягиваться в высоту до размеров самого большого item-a в секции
- И самое главное если мы будем переиспользовать `items_horizontal_scrollable_grid`, то персональные шорткаты должны лежать в массиве items.<br/>
Тогда подразумевается, что новый item может быть в любой секции, но это не так. У него нет фиксированной высоты и он будет ломать всю сетку

Новую секцую назовем `horizontal_stack_section`

**YAML**
```yaml
 HorizontalStackSection:
    type: object
    additionalProperties: false 
    required:
        - type
        - stack_item_ids
```
**JSON:**
```JavaScript
{
    "sections" : [
        {
            "type": "horizontal_stack_section",
            "stack_item_ids": ["id:123", "id:133", "id:323"]
        },
        ...
    ]
}
```

Так же будет новый массив `stack_items` рядом с `headers`, `items`, `buttons`:
```diff
{
    "headers" : [...],
    "items" : [...],
    "buttons" : [...], 
+   "stack_items" : [...],
}
```

### Шоркат

<img src="./static/personalized_shortcut_component_mockup.png" width="200">

Новый персонализированый шорткат является составным, и собирается из различных модулей.<br/>
В теории элементы внутри могут менять местами, какие-то могут не приходить вовсе.<br/>
В дальнейшем может появится требование изменить наполнение на другие компоненты с иным поведением

`width` - по словам дизайнеров, должен быть статичным и не зависеть от сетки. 
На данный момент нет идей по динамичному `width`, без затаскивания знаний на backend

в `action` приходят уже известные `actions`, которые поддержаны в шорткате с типом `action-driven` 

**YAML**
```yaml
 VerticalStack:
    type: object
    additionalProperties: false 
    required:
        - id
        - type
        - alignment_top_items
        - alignment_bottom_items
    properties:
        id:
            type: string
        type:
            type: string
        service:
            type: string
        background_color:
            type: string
        action:
            $ref: '#/components/schemas/Action' # action-driven action
        alignment_top_items:
            $ref: '#/components/schemas/VerticalStackItem'
        alignment_bottom_items:
            $ref: '#/components/schemas/VerticalStackItem'

 VerticalStackItem:
    oneOf:
        - $ref: '#/components/schemas/Info'
        - $ref: '#/components/schemas/Button'
        - $ref: '#/components/schemas/Thumb'
```
**JSON:**
```JavaScript
{
    "id": "id:123"
    "type": "vertical_stack_item",
    "background_color": "#FFFFFF",
    "service": "market",
    "action": {
        "deeplink": "yandextaxi://external?service=shop&href=collections/shops",
        "type": "deeplink"
    },
    "alignment_top_items": [ 
        ... // Тут будут компоненты с alignment к вверхней части 
    ],
    "alignment_bottom_items": [
        ... // Тут будут компоненты с alignment к нижней части 
    ]
}
```

---

#### Info

<img src="./static/personalized_shortcut_title_mockup.png" width="200"> 

Ограничения в 2-3 строки должны соблюдаться со стороны маркетинга, а не техническим ограничениями.

**YAML**
```yaml
 VerticalStackInfoItem:
    type: object
    additionalProperties: false 
    required:
        - type
        - title
    properties:
        type:
            type: string
        title:
            $ref: '#/components/schemas/Title'

 Title:
    type: object
    additionalProperties: false 
    required:
        - text
    properties:
        text:
            type: string
        attributed_text:
            $ref: '#/components/schemas/AttributedText'

```
**JSON:**
```JavaScript
{
    "type": "info",
    "title": {
        "text": "Аккумулятор Xiaomi Redmi Power Bank Fast Charge"
        "attributed_text": {
            "items": [{
                "type": "text",
                "text": "Аккумулятор Xiaomi Redmi Power Bank Fast Charge",
                "color": "#FFFFFF"
            }]
        }
    }
}
```

---

#### Rating

<img src="./static/personalized_shortcut_meta_mockup.png" width="200">

Рейтинг от 0 до 10. При отклонениях рейтинг не будет отображаться вовсе, но тест будет
Фронт умеет отобража только звезду и половину звезды, поэтому выбор пал на значения до 10 

`accessibility_label` - Нужен для доступности. Обычный пользователь не увидит этого, но для слабовидящих пользователей данный текст поможет понять что отображает данный компонент

**YAML**
```yaml
 VerticalStackRatingItem:
    type: object
    additionalProperties: false 
    required:
        - type
        - value
    properties:
        type:
            type: string
        meta_info:
            $ref: '#/components/schemas/Title'
        details:
            type: object
            additionalProperties: false 
            required:
                - content
            properties:
                content:
                    $ref: '#/components/schemas/Title'
                accessibility_label:
                    type: string
```
**JSON:**
```JavaScript
{
    "type": "rating",
    "meta_info": {
        "text": "20 000 мА·ч  - c кабелем",
        "attributed_text": nil
    }, 
    "details": {
        "accessibility_label": "Рейтинг 4.8: на основе 411 пользователей",
        "content": {
            "text": nil,
            "attributed_text": {
                 "items": [{
                    "type": "text",
                    "text": "4,8 ",
                    "color": "#21201F",
                    "font_size": "11"
                },
                {
                    "type": "text",
                    "text": "/ 411",
                    "color": "#9E9B98",
                    "font_size": "11"
                }
            }
        }
    },
    "value": 9
}
```

---

#### Price

<img src="./static/personalized_shortcut_price_mockup.png" width="200">
 
Компонент `price` реализуется при помощи`attributed_text`.

Поле `text_decoration` в `AttributedText` - становится deprecated, тк является массивом `String`, а текстовые декораторы могут иметь параметры.
Для этого добавляем поле `detailed_text_decoration` с объектами

После обновления на `text_decoration`

Некторые шрифты и языки не поддерживаю различные знаки валют, на саммари проблема была решена с помощью `currency_rules`.

**YAML**
```yaml
Price:
    type: object
    additionalProperties: false 
    required:
        - type
        - title
    properties:
        type:
            type: string
        title:
            $ref: '#/components/schemas/Title'
```
**JSON**
```JavaScript
{
    "type": "price",
    "title": {
        "text": "fallback text",
        "attributed_text": {
            "items": [{
                "type": "text",
                "text": "1 490",
                "color": "#FC5230",
                "font_size": "16"
            },
            {
                "type": "text",
                "text": "₽ ",
                "color": "#FC5230",
                "font_size": "13"
            },
            {
                "type": "text",
                "text": "1 690 ₽",
                "color": "#8A8784",
                "font_size": "13",
                "text_decoration": [...], // Deprecated
                "detailed_text_decoration": [
                    {
                        "type": "line_through",
                        "style": "diagonally" // default | diagonally
                        "color": "#FC5230"
                    },{
                    "type": "underline"
                    }
                ]
            }]
        }
    }   
}
```

Изменения в `AttributedText`

**YAML**
```yaml
AttributedText:
    type: object
    additionalProperties: false 
    properties:
        ...
        detailed_text_decoration:
            oneOf:
                - $ref: '#/components/schemas/LineThrough'
                - $ref: '#/components/schemas/Underline'
        ...

LineThrough:
    type: object
    additionalProperties: false
    required:
        - type
        - style
    properties:
        type: string
        style:
            type: string
            enum:
                - diagonally
                - default
        color: string
Underline:
    type: object
    additionalProperties: false
    required:
        - type
    properties:
        type: string
        color: string
```

---

#### Button

<img src="./static/personalized_shortcut_button_mockup.png" width="200">

Компонент кнопки, в `action` приходят уже известные `actions`, которые поддержаны в шорткате с типом `action-driven` 


Уже сейчас обдумывают концепт нескольких кнопок в ряд.<br/>
Данный кейс будет в возможно реализовать с помощью нового `type`.

**YAML**
```yaml
VerticalStackButtonItem:
    type: object
    additionalProperties: false 
    required:
        - type
        - title
        - action
    properties:
        type:
            type: string
        background_color:
            type: string
        title:
            $ref: '#/components/schemas/Title'
        action:
            $ref: '#/components/schemas/Action' # action-driven action

```
**JSON:**
```JavaScript
{
    "type": "button",
    "background_color": "FFFFFF",
    "title": {
        "text": "В корзину",
        "attributed_text": null
    },
    "action": {
        "deeplink": "yandextaxi://external?service=shop&href=collections/shops",
        "type": "deeplink"
    }
}
```

---

#### Thumb

<img src="./static/personalized_shortcut_thumb_mockup.png" width="200">

`Thumb` - это полноценный компонент с изображением и массивом компонентов `overlays`<br/>

`overlays` - стикеры будут различных типов, так же как и в других шорткатах. Но в данной реализации хочеться разделить внешний вид от его расположения, так как на макетах видно, что расположение стикеров очень хаотичное.

`multiply_color` - Используется для наложения цвета на картинку, чтобы заменить белый цвет фона. Так же используется для фона если всего элемента `thumb`

Вводится новый параметр `position`. Где указаны координаты на `Thumb` и координаты на `overlay`.<br/>
В данном случае `0, 0` левый верхний угол и `0.5, 0.5` центр у `overlay`

**YAML**
```yaml
 VerticalStackThumbItem:
    type: object
    additionalProperties: false 
    required:
        - type
        - image_url
        - image_tag
    properties:
        type:
            type: string
        image_url:
            type: string
        image_tag:
            type: string
        multiply_color:
            type: string
        overlays:
            $ref: '#/components/schemas/Overlay'

 Overlay:
    oneOf:
        - $ref: '#/components/schemas/RoundLabelOverlay'
        - $ref: '#/components/schemas/SquircleLabelOverlay'
        - $ref: '#/components/schemas/HexagonLabelOverlay'
        - $ref: '#/components/schemas/ParallelogramLabelOverlay'
        - $ref: '#/components/schemas/PlusLabelOverlay'

 RoundLabelOverlay:
    type: object
    additionalProperties: false 
    required:
        - type
        - background_color
        - tilt_angle
        - title
        - position
    properties:
        type:
            type: string
            enum:
              - round_label
        background_color:
            type: string
        tilt_angle:
            type: float
        title:
            $ref: '#/components/schemas/Title'
        position:
            $ref: '#/components/schemas/Position'
            
 SquircleLabelOverlay:
    type: object
    additionalProperties: false 
    required:
        - type
        - background_color
        - tilt_angle
        - title
        - position
    properties:
        type:
            type: string
            enum:
              - squircle_label
        background_color:
            type: string
        tilt_angle:
            type: float
        title:
            $ref: '#/components/schemas/Title'
        position:
            $ref: '#/components/schemas/Position'
            
 HexagonLabelOverlay:
    type: object
    additionalProperties: false 
    required:
        - type
        - background_color
        - tilt_angle
        - title
        - position
    properties:
        type:
            type: string
            enum:
              - hexagon_label
        background_color:
            type: string
        tilt_angle:
            type: float
        title:
            $ref: '#/components/schemas/Title'
        position:
            $ref: '#/components/schemas/Position'
            
 ParallelogramLabelOverlay:
    type: object
    additionalProperties: false 
    required:
        - type
        - background_color
        - tilt_angle
        - title
        - position
    properties:
        type:
            type: string
            enum:
              - parallelogram_label
        background_color:
            type: string
        tilt_angle:
            type: float
        title:
            $ref: '#/components/schemas/Title'
        position:
            $ref: '#/components/schemas/Position'

 PlusLabelOverlay:
    type: object
    additionalProperties: false 
    required:
        - type
        - tilt_angle
        - title
        - position
    properties:
        type:
            type: string
            enum:
              - plus_label
        tilt_angle:
            type: float
        title:
            type: string
        position:
            $ref: '#/components/schemas/Position'

Position:
    oneOf:
        - $ref: '#/components/schemas/AnchoredPosition'

AnchoredPosition:
    type: object
    additionalProperties: false 
    required:
        - type
        - point_on_parent
        - anchor
    properties:
        type:
            type: string
        point_on_parent:
            type: object
            additionalProperties: false
            required:
                - vertical
                - horizontal
            properties:
                vertical: 
                    type: float
                horizontal: 
                    type: float
        anchor:
            type: object
            additionalProperties: false
            required:
                - vertical
                - horizontal
            properties:
                vertical: 
                    type: float
                horizontal: 
                    type: float
```
**JSON:**
```JavaScript
{
    "type": "thumb",
    "image_url": "https://...", // takes precedence over image_tag
    "image_tag": "headphones",
    "multiply_color": "#F5F4F2",
    "overlays": [
        {
            "type": "round_label",
            "background_color": "#21201F",
            "title": {
                "text": "Скидка",
                "attributed_text": null
            },
            "tilt_angle": 180,
            "position": {
                "type": "anchored",
                "point_on_parent": {
                    "vertical": 0,
                    "horizontal": 0,
                },
                "anchor": {
                    "vertical": 0.5,
                    "horizontal": 0.5,
                }
            } 
        }
    ]
}
```
