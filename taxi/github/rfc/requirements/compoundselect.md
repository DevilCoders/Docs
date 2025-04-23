## Новый вид селектора Детского кресла
https://st.yandex-team.ru/TAXIPROJECTS-1151

![image](https://wiki.yandex-team.ru/users/irbis/dekompozicija-detskojj-vertikali/.files/image-1.png)
![image](https://wiki.yandex-team.ru/users/irbis/dekompozicija-detskojj-vertikali/.files/image-2.png)

## zoneinfo API

По наличию флага `compoundselect` в supported и попаданию в _бекендовый_ эксперимент
`zoneinfo_compoundselect_support` и наличию в нём соответствующих данных отдаем в
zoneinfo.max_tariffs[].supported_requirements требование в новом формате.
*note* Формат compoundselect является расширением над старыми select + multiselect требованиями,
поэтому перечислены только новые поля или те у которых меняется значение

```
"type": "compoundselect",   // вместо select
"unset_order_button": "Выбрать кресла",    // Что писать на кнопке заказа если
                                            // 1) glued: true
                                            // 2) glued_optional: false (или отсутствует)
                                            // 3) пожелание не выбрано (ни одна из его опций)
"select": {
  "caption": "Детские кресла", // 1 вместо Детское кресло
  "type": "number",            // as is
  "options": [
    {
      "name": "infant",               // as-is, используется для матчинга в compoundselect
      "icon": { ... },                // 21
      "icon_disabled": {...},         // (new) 21 если выбор заблокирован
      "title": "Люлька, до 1 года",   // 16
      "label": "100см, до 1 года",    // 13
      // 20 (new) что писать в label если выбор опции недоступен
      // Если отсутствует либо недостаточно полей,
      // может быть заменено на compoundselect.items[].title
      "label_disabled": {             
        "max_weight": "Превышено общее число кресел",
        "max_count": "Больше нельзя выбрать такого типа"
      },
      "item_trail": "Люлька, малыш до 1 года" // (new) items[].trail если выбрали опцию
      // "title_forms" отсутствует
    },
  ]
},
"compoundselect": {
  "items": [
    {
      "title": "Первое кресло", // 10
      "title_popup": "Первое кресло", // 8
      "title_on_label": "Первое кресло", // 20
      "description": "Онбординг текст" // 9,
      "trail_placeholder": "Выбрать",       // 11
      "icon": { ... },           // 12
      "title_selected": "Первое", // title если выбрано
      "cancel_button": "Отменить"
    },
    {
      "title": "Второе кресло", // 10
      "title_popup": "Второе кресло", // 8
      "title_on_label": "Второе кресло", // 20
      "description": "Онбординг текст" // 9,
      "trail_placeholder": "Выбрать",       // 11
      "icon": { ... },           // 12
      "title_selected": "Первое", // title если выбрано
      "cancel_button": "Отменить"
    },
  ]
}
```

## Изменения в схемах
### supported_requirements[] schema
```
(только те поля где есть изменения)
type:
    description: Тип требования
    enum:
      - boolean
      - select
      - compoundselect
    type: string
label:
    description: Локализованное название для UI
    type: string
   
(новые поля)
unset_order_button:
  type: string
  description: Что писать если требование glued, не optional_glued и не выбрано
compoundselect:
  type: object
  additionalProperties: false
  properties:
    items:
      type: array
      items:
        type: object
        additionalProperties: false
        required:
          - title
          - trail_placeholder
          - cancel_button
        properties:
          title:
            type: string
            example: "Первое кресло"
          title_popup:
            type: string
            example: "Первое кресло"
          title_on_label:
            type: string
            example: "Первое кресло"
          description:
            type: string
            example: "Онбординг текст"
          trail_placeholder:
            type: string
            example: "Выбрать"
          icon:
            description: иконка на селекторе "Первое/второе кресло"
            $ref: '#/definitions/image'
          title_selected:
            type: string
            example: "Первое"
          cancel_button:
            type: string
            example: "Отменить
```


### supported_requirements[].select.options[] schema
Новые поля: icon_disabled, item_trail, label_disabled
Поля с изменением значения для compoundselect: icon, label, title
Поля, которых не должно быть в compoundselect: title_forms

```
type: object
additionalProperties: false
required:
  - name
  - label
  - value
properties:
    icon:
        $ref: '#/definitions/image'
        description: иконка опции для саммари / compoundselect попапа
    icon_disabled:
        $ref: '#/definitions/image'
        description: (compoundselect) иконка недоступной опции для попапа
            если отсутствует, используется icon
    item_trail:
        description: (compoundselect) items[].trail если выбрали опцию
        type: string
    image:
        $ref: '#/definitions/image'
        description: изображение опции для карточки тарифа
    independent_tariffication:
        description: тарифицировать ли опцию отдельно
        type: boolean
    label:
        description: Локализованное название для UI
        type: string
    label_disabled:
        description: что писать в label если выбор опции недоступен
        type: object
        additionalProperties: false
        required:
          - max_weight
          - max_count
        properties:
          max_weight:
            type: string
          max_count:
            type: string
    max_count:
        description: максимальное количество
        minimum: 1
        type: integer
    name:
        description: Внутреннее название вложенного
            требования
        type: string
    style:
        description: стиль отображения опции в карточке
        enum:
          - spinner
          - check
        type: string
    title:
        description: Локализованный заголовок для UI
        type: string
    title_forms:
        description: формы title для разного количества от 1 до max_count
        type: object
    value:
        description: Значение варианта выбора
        oneOf:
          - type: string
          - type: number
    weight:
        description: условный вес опции
        exclusiveMinimum: true
        minimum: 0
        type: number
```



