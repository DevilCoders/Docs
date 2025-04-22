# summary modifiers

## Описание
Что такое модификаторы:
1. [task](https://st.yandex-team.ru/TAXIPROJECTS-1896)
2. [wiki](https://wiki.yandex-team.ru/taxi/client-product/uber-rider/modifikatory/?from=%2Fusers%2Fakruglyak%2Fklientskijj-produkt-taksi%2Fuber-rider%2Fmodifikatory%2F)
3. [figma](https://www.figma.com/file/DASlfE3PypeGshIJTmPLNN/Uber-Rider?node-id=3322%3A1925)

А также

![](https://jing.yandex-team.ru/files/ulturgashev/photo_2021-01-12_17-49-54.jpg)

### Резюме
Хочется уметь управлять карточками тарифа на саммари максимально гибко для проведения различного рода экспериментов

## Логика для отображения текста

### Модификаторы

Сурж:
- ~~риск роста цены~~
- ~~спрос растёт~~
- высокий спрос х1.3

Скидки:
- скидка 40Р

Подпись на карточке с промоушеном более быстрого тарифа:
- ~~приедет быстрее~~
- ~~быстрее на 7 минут~~
- ждать 4 минуты

Промоутим классы:
- дешёвые поездки
- популярный выбор
- быстрая подача
- дешево и быстро

### Цена
- значёк суржа - подставляем на клинтах
- значёк более дешевого тарифа - подставляем на клиентах
- 150 Р ~~180~~ - основное отличие в цвете цены со скидкой и в знаках рубля.

### Виды шаблонов:

- `скидка 40 %SIGN$$CURRENCY$`

- `обычный текст`
  
## API

routestats response

### new fileds way
```(json)
{
    "service_levels": [
        ...
        {
            "override": { // все объекты и сам объект override - опциональные
                "price": {
                    "properties": [
                        {
                            "types": ["selected"],
                            "attributed_text": { "items": [...] }
                        },
                        {
                            "types": ["unselected"],
                            "attributed_text": { "items": [...] }
                        }
                    ]
                },
                "class": {
                    "properties": [
                        {
                            "types": ["selected", "unselected"],
                            "attributed_text": { "items": [...] }
                        }
                    ]
                },
                "modifier": {
                    "properties": [
                        {
                            "types": ["selected", "unselected"],
                            "attributed_text": { "items": [...] }
                        }
                    ]
                },
                "overlay": {
                    "properties": [
                        "types": ["selected", "unselected"],
                        "shape": "label", // (пока что других типов нет)
                        "attributed_text": { "items": [...] }
                    ]
                }
            }
        },
        ...
    ]
}
```

`price` - оверайд для цены
`class` - оверайд для класса
`modifier` - новое поле, модификатор тарифа(на самом деле, это доп инфа тарифа)
`overlay` - значек, располагающийся в правом перхнем углу, будет использоваться для скидки

`types` - список состояний селектора тарифа

Может иметь следующие значения:
`selected` - выбранный селектор тарифа
`unselected` - невыбранный селектор тарифа

`attributed_text` - attributed-text
`shape` - тип, так же определяет где располагается данный тип оверлеев


### brandings base way <- current variant

Для решения задачи используем существуюший массив `service_levels.brandings`

Добавляем в объект брендинга `show_mode` и `attributed_text`

```(yaml)
AttributedText:
    type: object
    additionalProperties: false
    required:
        - items
    properties:
        items:
            type: array
            items:
                oneOf:
                    - $ref: "ATTextProperty"
                    - $ref: "ATImageProperties"

ShowMode:
    type: string
    enum:
        - selected
        - unselected

ServiceLevelBranding:
    type: object
    description: service level branding
    additionalProperties: false
    required:
        - type
    properties:
        type:
            type: string
        attributed_info:
            type: object
            description: 
            additionalProperties: false
            required:
                - attributed_text
            properties:
                show_mode:
                    type: array
                    items:
                        $ref: "ShowMode"
                attributed_text:
                    $ref: "AttributedText"
```

Добавляем новые типы брендингов:
- `price_field`
- `class_field`
- `modifier_field`
- `overlay`

В каждом `service_levels.brandings` может находится несколько различных элементов брендинга с одним и тем же типом, но разным `show_mode`.

## Клиентская логика

Условия показа оверайдов для цены:
- На активном тарифе показываем оверайд с типом `selected`, иначе `unselected`, если оверайд для состояния - отсутствует, ничего не показываем;
- клиент не отображает строчку модификатора, если текст не поместился в строку (добавить метрику, на данное событие);

## Бэкенд

Вся новая логика будет существовать в сервисе routestats в виде отдельного плагина.

На первом этапе, модификаторы и цены будем считать на основе ответа `backend-cpp/routestats`.

Имеется следующие модификаторы.
1. surge
2. discounts
3. cheap
4. min_eta

Бэкенд будет гарантировать, что в ответе routestats, будет сущестовать модификатор только одного типа.

Приоритет показа модификаторов:
1. surge - проверяем наличие `forced_surge`
2. discounts - проверяем наличие `original_price?` в ответе routestats
3. min_eta - ищем тариф с минимальным eta, в пределах заданного интервала времени
4. cheap - ищем самый дешевый тариф

Управление приоритетом сделать на основе эксперимента: `routestats_modifiers`

```(json)
{
    "properties": [
        {
            "name": "min_eta",
            "supported_tariffs": ["uberx", "select"],
            "threshold_eta_min": 5, // only for min_eta
            "definitions": [
                {
                    "show_modes": ["selected", "unselected"],
                    "tanker_key": "attributed_text_tanker_key"
                }
            ]
        },
        ...
    ]
}
```

Дополнительный эксперимент по замене цены в селекторе  (TODO)
