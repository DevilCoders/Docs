# Продуктовое описание

Научиться отображать "горизонтальные/квадратные/турбо" кнопки сервисов. Представляют из себя аналог динамических кирпичей, являются точкой входа в вертикаль.

![Турбокнопки](https://jing.yandex-team.ru/files/privet/Untitled%202.d509c93.png)

* Турбокнопки могут находиться как сразу после динамических кирпичей, так и в произвольном ряду выдачи
* На турбокнопках нужно сохранить трекинг, если он был у кирпичика
* Отображение disabled-состояния, если оно было у кирпичика
* Оверлеи, если они поддерживались в кирпичиках (сейчас это справедливо для shape=label)

# Решения

Турбокнопки нельзя выразить в существующей сетке: их размер и положение не попадает в "клетки". Можно измененить формат сетки (например, уменьшить ширину и высоту клетки, увеличив их количество) и дополнить протокол средствами выравнивания контента. Это сложное и дорогое изменение.

## Вариант с "секциями" [развиваем]

Представить ряд кнопок в существующей сетке нельзя. Нужен обратно-совместимый способ сообщить клиенту, что какие-то элементы подчиняются одним правилам отображения (например, сетка шорткатов), а какие-то — другим (например, ряд турбо-кнопок). Секция является таким способ определить правила отображения для набора элементов.
Верхнеуровневый пример:

```json
{
    "modes": [{
        "mode": "taxi",
        "layout": { "width": 6, "type": "linear_grid", "grid_id": "..." },
        "offers": {
            "header": [{"shortcut_id": "sid1"}],
            "items": [{"shortcut_id": "sid2"}],
            "buttons": [{"id": "button_id"}] //  buttons API below
        },
        "sections": [  // NEW
            {
               "type": "header_linear_grid",
               "shortcut_ids": ["sid1", "..."], // shortcuts from offers.header
            },
            {
                "type": "buttons_container",
                "button_ids": ["..."],
            },
            {
               "type": "items_linear_grid",
               "shortcut_ids": ["sid2", "..."], // shortcuts from offers.items
            },
        ]
    }]
}
```

## Обратная совместимость

Старые клиенты продолжат использовать offers.items и offers.header.

Новые должны иметь возможность работать без `sections` в ответе, т.к. фоллбек на бекенде не умеет их формировать (и не будет уметь)


## Типы секций

**"type": "linear_grid"**

Секция с сеткой шорткатов. Элементами сеции являются шорткаты из массивов `offers.header` и `offers.items`. Порядок шорткатов в секции определяется порядком айдишников из массива `shortcut_ids`.

**"type": "buttons_container"**

Секция с рядом кнопок. Элементами сеции являются объекты из массива `offers.buttons`. Порядок кнопок в секции определяется порядком айдишников из массива `button_ids`.

### API кнопок

```json
{
    "offers": {
        "buttons": [
            {
                "id": "some-unique-id",
                "title": "Доставка",
                "icon_tag": "delivery_icon_tag",
                "background": { "color": "#D9D4BE" },
                "text_style": { "color": "#000000" },
                "service": "grocery|eats|pharmacy|delivery...",
                "overlays": {
                    "shape": "label",
                    "background": {"...": "..."},
                    "attributed_text": {"items": []}
                },
                "action": {
                    "type": "deeplink", // Will elaborate below
                    "deeplink": "yandextaxi://..."
                }
            }
        ]
    }
}
```

### Типы действий для `offers.buttons`

Не вижу смысла вводить "типы" кнопок внутри , т.к. непонятно как они будут сочетаться с типами шорткатов. Вместо этого предлагаю разделять "представления" и "действия", чтобы действия из кнопок можно было использовать в шорткатах. Поддерживаемые действия сообщать в запросе v1/products. На данный момент нам нужны следующие типы действий:

**taxi:summary-redirect**
Действие из нативного кирпичика доставки, позволяющее перейти на саммари к вертикали/тарифу, см. taxi_summary_brick.md

```json
{
    "action": {
        "type": "taxi:summary-redirect",
        "class": "express",
        "vertical": "vertical_id",
        "state": "expanded|collapsed|anchored"
    }
}
```

**deeplink**
```json
{
    "action": {
        "type": "deeplink",
        "deeplink": "yandextaxi://..."
    }
}
```

**taxi:route-input**
```json
{
    "action": {"type": "taxi:route-input"}
}
```

Схема действия
```yaml
TypedSummaryRedirectAction:
    type:
        description: "taxi:summary-redirect"
        type: string
    class:
        type: string
        description: class to use on summary
        example: express
    vertical:
        type: string
        description: vertical to use on summary
        example: delivery
    state:
        type: string
        description: state to use on summary (expanded|collapsed|anchored)
        example: express

TypedDeeplinkAction:
    type:
        description: "deeplink"
        type: string
    deeplink:
        type: string
        example: yandextaxi://external?service=grocery

TypedRouteInputAction:
    type:
      type: string
      enum:
        - taxi:route-input

TypedAction:
    oneOf:
        - TypedDeeplinkAction
        - TypedSummaryRedirectAction
        - TypedDiscoveryAction # check discovery_action.md
        - TypedRouteInputAction
```

### Типы представлений

На данный момент представления кнопок описываются одинаково

```json
{
    "title": "some title",
    "icon_tag": "some_icon_tag",
    "background": { "color": "#F1F0ED" },
    "text_style": { "color": "#000000" },
    "service": "grocery",
    "overlays": [{ "...": "..."}],
}
```

Кажется, вводить типы представлений пока рано, т.к. он сейчас один

### Поле `service`

В динамических кирпичах есть поле `service`, по которому клиент понимает где отображать трекинг того или иного сервиса. Ещё это поле скоро будет использоваться в кирпичике доставки.

С одной стороны, это поле связано скорее с отображением, чем с действием. С другой стороны, это скорее какая-то метаинформация о сути "кнопки". Что делать? TODO

**Решение** поле `service` делаем частью представления.

## Изменения в запросе

Изменения в запросе отражены в `products.md`

### аналитика

TODO не хватает аналитического идентификатора для кнопки
TODO аналитические идентификаторы секции?

### backend

* Кто будет возвращать секции?
* Уточнить продуктовые требования для мвп: сейчас у нас всего три сервиса, для полноценной раскатки решения нужно как минимум четыре(?)

## Вариант с "псевдошорткатом" [отклонено]

В сетку можно поместить расположение *ряда* с турбокнопоками, а также содержимое этого ряда. Бекенд не будет управлять расстоянием между кнопками.

Высокоуровнево, ряд с кнопками с точки зрения API будет выглядеть как шорткат нового типа:

```json
{
    "shortcut_id": "???",
    "type": "verticals-buttons-container???",
    "items": [
        { "title": "Доставка", "...": "..." },
        { "title": "рестораны" },
        { "title": "лавка" },
        { "title": "транспорт" },
    ]
}
```

Плюс: вводим мало новых сущностей (фактически только новый тип шортката)

Минус: "ряд" с кнопками фактически не является шорткатом: его размер нельзя выразить в юнитах сетки, отсутствуют свойства `height`/`width`, неприменимы свойства `overlays` и `action`.