### Сетка карточек
На больших разрешениях сетка имеет 4 колонки, на маленьких 3. Шаги для media queries задаются в `platform/components/news-constants.scss`.

В turbo-json мы должны передать 2 свойства: positionList и content. В content в общем случае передаётся список карточек.

Для формирования positionList указываются 3 свойства:
1. **type — ELayoutItemType (Тип)**
* SINGLE — Одинарная
* HORIZONTAL_2 — Двойная
* HORIZONTAL_2_3 — На маленьких разрешениях двойная, на больших тройная
* HORIZONTAL_3 — Тройная
* FULL_WIDTH — На всю ширину
2. **pos — ELayoutItemPos (Позиция)**
* NONE — Стандартное поведение
* LEFT — Прибивается к левому краю сетки
* RIGHT — Прибивается к правому (двойные карточки должны быть либо LEFT, либо RIGHT)
3. **hidden — ELayoutItemHidden (Возможность скрыть элемент). Необязательный, можно передать массив.**
* STEP_1 — Скрывается на ширине step-1 (см. news-constants.scss)
* STEP_2 — Скрывается на ширине step-2
* STEP_3 — Скрывается на ширине step-3
* STEP_4 — Скрывается на ширине step-4

Пример использования:
```
{
    block: 'mg-page-layout',
    props: {
        positionList: [
            {
                type: ELayoutItemType.HORIZONTAL_2,
                pos: ELayoutItemPos.LEFT
            },
            {
                type: ELayoutItemType.SINGLE,
                pos: ELayoutItemPos.NONE
            },
            {
                type: ELayoutItemType.SINGLE,
                pos: ELayoutItemPos.NONE
            },
            {
                type: ELayoutItemType.SINGLE,
                pos: ELayoutItemPos.NONE
            },
            {
                type: ELayoutItemType.FULL_WIDTH,
                pos: ELayoutItemPos.RIGHT
            }
        ],
    },
    content: [
        {
            block: 'card',
            theme: 'sport',
            data: {
                id: <id>,
                date: <timestamp>,
                timezone: 0,
                url: <url>,
                title: <заголовок>,
                text: <аннотация>,
                source: <источник>,
                doubleWidth: true
            }
        },
        {
            block: 'card',
            theme: 'sport',
            data: {
                id: <id>,
                date: <timestamp>,
                timezone: 0,
                url: <url>,
                title: <заголовок>,
                text: <аннотация>,
                source: <источник>,
                doubleWidth: false
            }
        },
        {
            block: 'card',
            theme: 'sport',
            data: {
                id: <id>,
                date: <timestamp>,
                timezone: 0,
                url: <url>,
                title: <заголовок>,
                text: <аннотация>,
                source: <источник>,
                doubleWidth: false
            }
        },
        {
            block: 'card',
            theme: 'sport',
            data: {
                id: <id>,
                date: <timestamp>,
                timezone: 0,
                url: <url>,
                title: <заголовок>,
                text: <аннотация>,
                source: <источник>,
                doubleWidth: false
            }
        },
        {
            block: 'news-carousel',
            props: {
                title: 'Популярные видео'
            },
            content: <список видео>
        }
    ]
}
```
