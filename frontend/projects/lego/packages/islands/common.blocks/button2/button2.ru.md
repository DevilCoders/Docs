# button2

Используется для создания кнопок.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [theme](#mods-theme) (req) | `'normal'`, `'raised'`, `'action'`, `'pseudo'`, `'link'`, `'clear'`, `'websearch'` | `BEMJSON`, `JS` | Стилевое оформление. |
| [size](#mods-size) (req) | `'xs'`, `'s'`, `'ns'`, `'n'`, `'m'`, `'l'`, `'head'` | `BEMJSON`, `JS` | Размер кнопки. |
| [type](#mods-type) | `'link'`, `'submit'`, `'check'`, `'radio'` | `BEMJSON` | Тип кнопки. |
| [action](#mods-action) | `'yes'` | `BEMJSON`, `JS` | Стилевое оформление. Используется для визуального выделения кнопки с темой [normal](#theme-normal) или [raised](#theme-raised). |
| [has-control](#mods-has-control) | `'yes'` | `BEMJSON`, `JS` | Добавляет вспомогательный элемент `control`. Используется только для [кнопок-переключателей](#type-check) и [радиокнопок](#type-radio). |
| [pale](#mods-pale) | `'yes'` | `BEMJSON`, `JS` | Полупрозрачный текст кнопки. |
| [pin](#mods-pin) | `'brick-clear'`, `'clear-brick'`, `'round-clear'`, `'clear-round'`, `'circle-clear'`, `'clear-circle'`, `'round-brick'`, `'brick-round'`, `'circle-brick'`, `'brick-circle'`, `'clear-clear'`, `'brick-brick'`,`'round-round'`,`'circle-circle'` | `BEMJSON`, `JS` | Форма кнопки. |
| [tone](#mods-tone) | `'default'`, `'red'`, `'grey'`, `'dark'`, `'market'` | `BEMJSON`, `JS` | Тон кнопки. |
| [view](#mods-view) | `'default'`, `'classic'` | `BEMJSON`, `JS` | Вид кнопки. |
| [width](#mods-width) | `'auto'`, `'max'` | `BEMJSON`, `JS` | Ширина кнопки. |
| [checked](#mods-checked) | `'yes'` | `BEMJSON`, `JS` | Кнопка нажата. Используется для [кнопок-переключателей](#type-check) и [радиокнопок](#type-radio), а также для кнопок со стилевым оформлением отличным от [action](#theme-action). |
| [disabled](#mods-disabled) | `'yes'` | `BEMJSON`, `JS` | Неактивное состояние. |
| [focused](#mods-focused) | `'yes'` | `BEMJSON`, `JS` | Фокус на блоке. |
| [pressed](#mods-pressed) | `'yes'` | — | Нажатие на кнопку. |
| [hovered](#mods-hovered) | `'yes'`, `boolean` | — | Наведение на кнопку курсором. |
| [progress](#mods-progress) | `'yes'` | — | Стилевое оформление. Используется для визуального выделения прогресса. |
| [baseline](#mods-baseline) | `'yes'` | `BEMJSON`, `JS` | Временный модификатор для выравнивания по базовой линии, будет внедрено в следующем мажоре |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [attrs](#field-attrs) | `BEMJSON` | Произвольные атрибуты кнопки. |
| [textAttrs](#field-textattrs) (react-only) | `Object` | Произвольные атрибуты элемента `text`. |
| [text](#field-text) | `String` | Текст кнопки. |
| [icon](#field-icon) | `BEMJSON` | Иконка на кнопке. Формируется блоком [icon](../icon/icon.ru.md). |
| [iconLeft](#field-iconleft) | `BEMJSON` | Иконка слева от текста кнопки. |
| [iconRight](#field-iconright) | `BEMJSON` | Иконка справа от текста кнопки. |
| [content](#field-content) | `BEMJSON` | Содержимое кнопки. Используется для формирования произвольной HTML-разметки, с помощью элементов блока. Переопределяет значения заданные в полях `text`, `icon`, `iconLeft`, `iconRight`. |
| [name](#field-name) | `String` | Уникальное имя блока. Не используется, если [модификатор type выставлен в значение link](#type-link). |
| [val](#field-val) (i-bem-only) | `String` | Значение, отправляемое на сервер. Не используется, если [модификатор type выставлен в значение link](#type-link). |
| [value](#field-value) (react-only) | `String` | Значение, отправляемое на сервер. Не используется, если [модификатор type выставлен в значение link](#type-link). |
| [url](#field-url) | `String` | Адрес. Используется только для кнопки с [модификатором type в значении link](#type-link). |
| [target](#field-target) | `String` | Поведение [кнопки-ссылки](#type-link). |
| [title](#field-title) | `String` | Текст всплывающей подсказки. |
| [id](#field-id) | `String` | Уникальный идентификатор кнопки. |
| [tabindex](#field-tabindex) | `Number` | Последовательность перехода между контролами при нажатии на `Tab`. |
| [pressKeys](#field-presskeys) | `String[]` | Список кнопок с кодами клавиш, по которым произойдет событие `keypress`.|
| [prvntKeys](#field-prvntkeys) | `String[]` | Список кнопок с кодами клавиш, по которым произойдет `e.preventDefault()` для события `keydown`. |
| [control](#field-control) | `Object` |  |
| [innerRef](#field-innerref) | `(element: DOMElement<any, any>) => void` |  |


## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Отвечает за стилевое оформление кнопки. **Обязательный**.

Допустимые значения: `'normal'`, `'raised'`, `'action'`, `'pseudo'`, `'link'`, `'clear'`, `'websearch'`.

Способ установки: `BEMJSON`, `JS`.

<a name="theme-normal"></a>

**Обычная кнопка (модификатор `theme` в значении `normal`)**

Используется в большинстве случаев.

```js
[
    {
        block: 'button2',
        mods: { theme: 'normal', size: 'm', view: 'default', tone: 'default' },
        icon: { mods: { type: 'load' } }
    }, ' ',
    {
        block: 'button2',
        mods: { theme: 'normal', size: 'm', view: 'default', tone: 'default' },
        text: 'Тема normal'
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { type: 'load' } }
        ]
    }
]
```

<a name="theme-raised"></a>

**Поднятая кнопка (модификатор `theme` в значении `raised`)**

Используется для визуального выделения кнопки на странице.

```js
[
    {
        block: 'button2',
        mods: { theme: 'raised', size: 'm', view: 'default', tone: 'default' },
        icon: { mods: { type: 'load' } }
    }, ' ',
    {
        block: 'button2',
        mods: { theme: 'raised', size: 'm', view: 'default', tone: 'default' },
        text: 'Тема raised'
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { type: 'load' } }
        ]
    }
]
```

<a name="theme-action"></a>

**Кнопка действия (модификатор `theme` в значении `action`)**

Используется для визуального выделения кнопки на странице.

```js
[
    {
        block: 'button2',
        mods: { theme: 'action', size: 'm', view: 'default', tone: 'default' },
        icon: { mods: { type: 'load' } }
    }, ' ',
    {
        block: 'button2',
        mods: { theme: 'action', size: 'm', view: 'default', tone: 'default' },
        text: 'Тема action'
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { type: 'load' } }
        ]
    }
]
```

<a name="theme-pseudo"></a>

**Псевдокнопка (модификатор `theme` в значении `pseudo`)**

Используется для изменения внешнего вида блока при необходимости сделать кнопку менее заметной на странице.

```js
[
    {
        block: 'x-area',
        attrs: { style: 'background: #C9DCF6;' },
        content: [
            {
                block: 'button2',
                mods: { theme: 'pseudo', size: 'm', view: 'default', tone: 'default' },
                icon: { mods: { type: 'load' } }
            }, ' ',
            {
                block: 'button2',
                mods: { theme: 'pseudo', size: 'm', view: 'default', tone: 'default' },
                text: 'Тема pseudo'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { type: 'load' } }
        ]
    }
]
```

<a name="theme-link"></a>

**Кнопка-ссылка (модификатор `theme` в значении `link`)**

Используется для визуального выделения кнопки, ссылающейся на другие страницы.

```js
[
    {
        block: 'button2',
        mods: { theme: 'link', size: 'm', view: 'default', tone: 'default' },
        icon: { mods: { glyph: 'type-load' } }
    }, ' ',
    {
        block: 'button2',
        mods: { theme: 'link', size: 'm', view: 'default', tone: 'default' },
        text: 'Тема link'
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { glyph: 'type-load' } }
        ]
    }
]
```

<a name="theme-clear"></a>

**Кнопка-невидимка (модификатор `theme` в значении `clear`)**

Используется при необходимости представить кнопкой другой блок, например, иконку (блок [icon](../icon/icon.ru.md)) или текст.

```js
[
    {
        block: 'button2',
        mods: { theme: 'clear', size: 'm', view: 'default', tone: 'default' },
        icon: { mods: { type: 'load' } }
    }, ' ',
    {
        block: 'button2',
        mods: { theme: 'clear', size: 'm', view: 'default', tone: 'default' },
        text: 'Тема clear'
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { type: 'load' } }
        ]
    }
]
```

<a name="theme-websearch"></a>

**Кнопка «Найти» в желтой поисковой стрелке (модификатор `theme` в значении `websearch`)**

Используется на главной странице Яндекса.

```js
{
    block: 'button2',
    mods: { theme: 'websearch', size: false, type: 'submit' },
    attrs: { tabindex: -1 },
    text: 'Найти'
}
```

> **Важно!**
>
> Необходимо использовать с:
>
> * модификатором `type` в значении `submit`;
> * модификатором `size` в значении `false`;
> * атрибутом `tabindex` в значении `-1`.

<a name="mods-size"></a>

#### Модификатор `size`

Задает размер кнопке. **Обязательный**.

Допустимые значения: `'xs'`, `'s'`, `'ns'`, `'n'`, `'m'`, `'l'`, `'head'`.

> **Примечание.** Модификатор `button2_size_head` экспериментальный и используется в шапке на уровне `desktop`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['xs', 's', 'ns', 'n', 'm', 'l', 'head'],
    body: [
        ['xs', 's', 'ns', 'n', 'm', 'l', 'head'].map(function(size) {
            return {
                block: 'button2',
                mods: { theme: 'normal', size: size },
                text: 'Кнопка'
            };
        })
    ]
}
```

<a name="mods-type"></a>

#### Модификатор `type`

Задает тип кнопки.

Допустимые значения: `'link'`, `'submit'`, `'check'`, `'radio'`.

Способ установки: `BEMJSON`.

<a name="type-link"></a>

**Кнопка-ссылка (модификатор `type` в значении `link`)**

Используется для создания кнопки, обеспечивающей переход по адресу, указанному в поле [url](#field-url).

```js
{
    block: 'button2',
    mods: { theme: 'normal', size: 'm', type: 'link' },
    url: 'https://yandex.ru/',
    text: 'Тип link',
    target: 'blank'
}
```

<a name="type-submit"></a>

**Кнопка отправки формы (модификатор `type` в значении `submit`)**

Используется для создания кнопки, обеспечивающей отправку данных на сервер. Кнопка такого типа всегда должна располагаться в форме.

```js
{
    block: 'button2',
    mods: { theme: 'normal', size: 'm', type: 'submit' },
    text: 'Тип submit'
}
```

<a name="type-check"></a>

**Кнопка-переключатель (модификатор `type` в значении `check`)**

Используется для реализации «залипания» кнопки. Первое нажатие на кнопку вдавливает ее (выставляется модификатор [checked](#mods-checked)), второе – приводит в первоначальное состояние (снимается модификатор [checked](#mods-checked)).

```js
{
    block: 'button2',
    mods: { theme: 'normal', size: 'm', type: 'check' },
    text: 'Тип check'
}
```

<a name="type-radio"></a>

**Радиокнопка (модификатор `type` в значении `radio`)**

Используется для реализации «залипания» кнопки. Нажатие на кнопку вдавливает ее (выставляется модификатор [checked](#mods-checked)), и она может быть приведена в первоначальное состояние только программно.

```js
{
    block: 'button2',
    mods: { theme: 'normal', size: 'm', type: 'radio' },
    text: 'Тип radio'
}
```

<a name="mods-action"></a>

#### Модификатор `action`

Отвечает за визуальное выделение кнопки с темой [normal](#theme-normal) или [raised](#theme-raised).

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

> **Важно!** Необходимо использовать с модификатором `view` в значении `default`.

```js
[
    {
        block: 'x-table',
        head: ['action + normal', 'action + raised'],
        body: [
            ['normal', 'raised'].map(function(theme) {
                return {
                    block: 'button2',
                    mods: { theme: theme, size: 'm', action: 'yes', view: 'default', tone: 'default' },
                    text: 'Кнопка'
                };
            })
        ]
    }
]
```

<a name="mods-has-control"></a>

#### Модификатор `has-control`

Добавляет вспомогательный элемент `control`. Используется только для [кнопок-переключателей](#type-check) и [радиокнопок](#type-radio).

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

> **Примечание.** Указанные атрибуты в полях: `name`, `id`, `val` и модификаторы блока: `button2_type_check`, `button2_disabled` переносятся на элемент `button2__control`. Блок `button2` выражается тегом `<span>`.

```js
{
    block: 'x-table',
    head: ['_has-control'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', type: 'check', 'has-control': 'yes' },
            name: 'control',
            id: 'control',
            val: 'control',
            text: 'Кнопка'
        }
    ]
}
```

<a name="mods-pale"></a>

#### Модификатор `pale`

Задает полупрозрачный цвет тексту кнопки.

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['_pale'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', pale: 'yes' },
            text: 'Кнопка'
        }
    ]
}
```

<a name="mods-pin"></a>

#### Модификатор `pin`

Задает форму кнопке. Используется для группировки с другими блоками, например, с [textinput](../textinput/textinput.ru.md).

Допустимые значения: `'brick-clear'`, `'clear-brick'`, `'round-clear'`, `'clear-round'`, `'circle-clear'`, `'clear-circle'`, `'round-brick'`, `'brick-round'`, `'circle-brick'`, `'brick-circle'`, `'clear-clear'`, `'brick-brick'`, `'round-round'`,`'circle-circle'`.

Допустимыми значениями модификатора являются комбинации двух ключевых слов через  дефис (`-`), которые определяют (слева направо):

* форму уголков;
* видимость границ;
* скругление границ.

Ключевое слово:

* `clear` — нет боковой границы;
* `brick` — прямоугольная граница;
* `round` — граница со скругленными уголками;
* `circle` — граница круглой формы.

Способ установки: `BEMJSON`, `JS`.

**Кнопки со скругленными уголками**

```js
[
    (function() {
        var pins = ['round-round','round-clear', 'clear-round', 'round-brick', 'brick-round'];

        return {
            block: 'x-table',
            head: pins,
            body: pins.map((pin) => {
                return {
                    block: 'button2',
                    mods: { theme: 'normal', size: 'm', pin: pin },
                    text: 'Кнопка'
                };
            })
        };
    })()
]
```

**Кнопки с круглыми границами**

```js
[
    (function() {
        var circlePins = ['circle-circle', 'circle-clear', 'clear-circle', 'circle-brick', 'brick-circle'];

        return {
            block: 'x-table',
            head: circlePins,
            body: circlePins.map(function(circlePin) {
                return {
                    block: 'button2',
                    mods: { theme: 'normal', size: 'm', pin: circlePin },
                    text: 'Кнопка'
                };
            })
        };
    })()
]
```

**Кнопки с прямоугольными уголками**

```js
[
    (function() {
        var pins = ['brick-brick', 'brick-clear', 'clear-brick'];

        return {
            block: 'x-table',
            head: pins,
            body: pins.map(function(pin) {
                return {
                    block: 'button2',
                    mods: { theme: 'normal', size: 'm', pin: pin },
                    text: 'Кнопка'
                };
            })
        };
    })()
]
```

**Кнопка без боковых границ**

```js
[
    (function() {
        var pins = ['clear-clear'];

        return {
            block: 'x-table',
            head: pins,
            body: pins.map(function(pin) {
                return {
                    block: 'button2',
                    mods: { theme: 'normal', size: 'm', pin: pin },
                    text: 'Кнопка'
                };
            })
        };
    })()
]
```

**Пример группировки**

> **Примечание.**
>
> Чтобы кнопка ровно выровнялась по горизонтали с блоком [input](../input/input.ru.md), ему нужно:
>
> * задать аналогичный с кнопкой размер (модификатор `size`);
> * добавить атрибут `vertical-align: baseline;`.

```js
[
    { block: 'x-title', tag: 'h3', text: 'Группировка с блоком input' },
    [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', pin: 'round-clear' },
            text: 'Кнопка'
        },
        {
            block: 'input',
            attrs: { style: 'width: 200px; vertical-align: baseline;' },
            mods: { size: 'm', theme: 'normal' },
            value: 'Инпут',
            content: { elem: 'control' }
        },
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', pin: 'clear-clear' },
            icon: { mods: { type: 'arrow', direction: 'bottom' } }
        },
        {
            block: 'input',
            attrs: { style: 'width: 200px; vertical-align: baseline;' },
            mods: { size: 'm', theme: 'normal'},
            value: 'Инпут',
            content: {elem: 'control'}
        },
        {
            block: 'button2',
            mods: { theme: 'action', size: 'm', pin: 'clear-round' },
            text: 'Найти'
        },
        {
            block: 'x-deps',
            content: [
                { block: 'button2', elem: 'icon' },
                { block: 'icon', mods: { type: 'arrow', direction: 'bottom' } }
            ]
        }
    ],
    { tag: 'br' },
    { block: 'x-title', tag: 'h3', text: 'Пагинация' },
    ['round-clear', 'brick-clear', 'brick-clear', 'brick-clear', 'brick-round'].map(function(pin, i) {
        return {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', pin: pin },
            text: i + 1
        };
    })
]
```

<a name="mods-tone"></a>

#### Модификатор `tone`

Задает тон кнопки.

Допустимые значения: `'default'`, `'red'`, `'grey'`, `'dark'`, `'market'`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Необходимо использовать с модификатором `view` в значении `default`.

```js
{
    block: 'x-table',
    head: ['default', 'red', 'grey', 'dark', 'market'],
    body: [
        ['default', 'red', 'grey', 'dark', 'market'].map(function(tone) {
            return {
                block: 'button2',
                mods: { theme: 'normal', size: 'm', view: 'default', tone: tone },
                text: 'Кнопка'
            };
        })
    ]
}
```

<a name="mods-view"></a>

#### Модификатор `view`

Задает вид кнопки.

Допустимые значения: `'default'`, `'classic'`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Модификатор `view` в значении `default` необходимо использовать с модификатором `tone`.

```js
{
    block: 'x-table',
    head: ['default', 'classic'],
    body: [
        ['default', 'classic'].map(function(view) {
            return {
                block: 'button2',
                mods: { theme: 'normal', size: 'm', view: view, tone: 'default' },
                text: 'Кнопка'
            };
        })
    ]
}
```

<a name="mods-width"></a>

#### Модификатор `width`

Задает ширину кнопки.

Допустимые значения: `'auto'`, `'max'`.

Способы установки: `BEMJSON`, `JS`.

<a name="width-auto"></a>

**auto**

Ширина кнопки определяется шириной текста. Если ширина текста больше ширины контейнера (родительский HTML-элемент), текст обрезается троеточием.

```js
{
    block: 'x-area',
    mods: { bordered: 'yes', resizable: 'yes' },
    content: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', width: 'auto' },
            text: 'Ширина auto'
        }
    ]
}
```

<a name="width-max"></a>

**max**

Ширина кнопки определяется шириной контейнера. Если ширина текста больше ширины контейнера, текст обрезается троеточием.

```js
{
    block: 'x-area',
    mods: { bordered: 'yes', resizable: 'yes' },
    content: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', width: 'max' },
            text: 'Ширина max'
        }
    ]
}
```

<a name="mods-checked"></a>

#### Модификатор `checked`

Отвечает за состояние кнопки «нажата».

Допустимые значения: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

Используется для [кнопок-переключателей](#type-check) и [радиокнопок](#type-radio), а также для кнопок со стилевым оформлением отличным от `'action'`.

```js
[
    (function() {
        var types = ['check', 'radio'],
            heads = ['Переключатель', 'Радиокнопка'];

        return {
            block: 'x-table',
            head: heads,
            body: types.map(function(type) {
                return {
                   block: 'button2',
                   mods: { theme: 'normal', size: 'm', type: type, checked: 'yes' },
                   text: 'Кнопка'
                };
            })
        }
    })()
]
```

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Отвечает за неактивное состояние, при котором кнопка видна, но недоступна для действий пользователя.

Нельзя:

* установить модификаторы `focused`, `pressed` и `hovered` (существующие удаляются);
* вызвать БЭМ-события;
* перейти по ссылке (для кнопки с типом [link](#type-link));
* отправить форму (для кнопки с типом [submit](#type-submit)).

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

> **Примечание.** Неактивное состояние блока можно изменять программно.

```js
{
    block: 'x-table',
    head: ['_disabled'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', disabled: 'yes' },
            text: 'Кнопка'
        }
    ]
}
```

<a name="mods-focused"></a>

#### Модификатор `focused`

Отвечает за установку фокуса.

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

Выставляется автоматически при получении кнопкой фокуса.

```js
{
    block: 'x-table',
    head: ['_focused'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', focused: 'yes' },
            text: 'Кнопка'
        }
    ]
}
```

<a name="mods-pressed"></a>

#### Модификатор `pressed`

Определяет действие «нажатие на кнопку».

Допустимое значение: `yes`.

Способы установки: `—`.

```js
{
    block: 'button2',
    mods: { theme: 'normal', size: 'm', pressed: 'yes' },
    text: 'Кнопка'
}
```

<a name="mods-baseline"></a>

#### Модификатор `baseline`

Выравнивает кнопку по базовой линии. Временный модификатор. Будет внедрено в следующем мажоре.

> **Примечание** В браузера Firefox модификатор перестанет работать, если в блоке добавлено свойство `overflow: hidden`.

Допустимые значения: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['xs', 's', 'm'],
    body: [
        ['xs', 's', 'm'].map(function(size) {
            return {
                block: 'button2',
                mods: { theme: 'normal', size: size, baseline: 'yes' },
                text: 'Кнопка'
            };
        })
    ]
}
```

### Поля блока

<a name="field-attrs"></a>

#### Поле `attrs`

Определяет произвольные атрибуты кнопки.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле attrs'],
    body: [
        {
            block: 'button2',
            attrs: { style: 'margin: 1px 15px;' },
            mods: { theme: 'normal', size: 'm' },
            text: 'Кнопка'
        }
    ]
}
```

<a name="field-text"></a>

#### Поле `text`

Определяет текст, который отображается на кнопке.

Тип: `String`.

> **Примечание.** Поле `text` позволяет определить текст кнопки и подходит для решения большинства задач, однако через него нельзя задать произвольный `BEMJSON`. В случае если необходимо внутри блока `button2` определить некую HTML-разметку, нужно использовать поле [content](#field-content).

```js
{
    block: 'x-table',
    head: ['Поле text'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm' },
            text: 'Кнопка'  // Переданное значение экранируется автоматически
        }
    ]
}
```

<a name="field-icon"></a>

#### Поле `icon`

Определяет иконку, которая отображается на кнопке. Иконка задается с помощью блока [icon](../icon/icon.ru.md).

Тип: `BEMJSON`.

> **Примечание.** Рекомендуется использовать для кнопок без текста.

```js
[
    {
        block: 'x-table',
        head: ['Поле icon'],
        body: [
            {
                block: 'button2',
                mods: { theme: 'normal', size: 'm' },
                icon: {
                    // block: 'icon' указывать не нужно
                    mods: { type: 'load' }
                }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { type: 'load' } }
        ]
    }
]
```

<a name="field-iconleft"></a>

#### Поле `iconLeft`

Определяет иконку, которая отображается слева от текста кнопки. Иконка задается с помощью блока [icon](../icon/icon.ru.md).

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле iconLeft'],
        body: [
            {
                block: 'button2',
                mods: { theme: 'normal', size: 'm' },
                iconLeft: {
                    // block: 'icon' указывать не нужно
                    mods: { type: 'arrow', direction: 'left' }
                },
                text: 'Кнопка'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { type: 'arrow', direction: 'left' } }
        ]
    }
]
```

<a name="field-iconright"></a>

#### Поле `iconRight`

Определяет иконку, которая отображается справа от текста кнопки. Иконка задается с помощью блока [icon](../icon/icon.ru.md).

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле iconRight'],
        body: [
            {
                block: 'button2',
                mods: { theme: 'normal', size: 'm' },
                iconRight: {
                    // block: 'icon' указывать не нужно
                    mods: { type: 'arrow', direction: 'right' }
                },
                text: 'Кнопка'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { type: 'arrow', direction: 'right' } }
        ]
    }
]
```

<a name="field-content"></a>

#### Поле `content`

Определяет содержимое кнопки. Используется для формирования произвольной HTML-разметки.

Тип: `BEMJSON`.

> **Важно!** Переопределяет значения заданные в полях `text`, `icon`, `iconLeft`, `iconRight`.

```js
{
    block: 'x-table',
    head: ['Поле content'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm' },
            content:  {
                block: 'logo',
                attrs: { style: 'margin: 1px 15px;' },
                mods: {
                    name: 'ys-ru-64x27'
                }
            }
        }
    ]
}
```

<a name="field-name"></a>

#### Поле `name`

Определяет уникальное имя блока.

Тип: `String`.

> **Важно!** Не используется, если [модификатор type выставлен в значение link](#type-link).

```js
{
    block: 'x-table',
    head: ['Поле name'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', type: 'submit' },
            name: 'check',
            text: 'Кнопка'
        }
    ]
}
```

<a name="field-val"></a>
<a name="field-value"></a>

#### Поле `val`

Определяет значение кнопки, которое будет отправлено на сервер.

Тип: `String`.

> **Важно!** Не используется, если [модификатор type выставлен в значение link](#type-link).

```js
{
    block: 'x-table',
    head: ['Поле val'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', type: 'submit' },
            val: 'check',
            text: 'Кнопка'
        }
    ]
}
```

<a name="field-url"></a>

#### Поле `url`

Определяет адрес, по которому осуществляется переход при нажатии на кнопку с [модификатором type в значении link](#type-link).

Тип: `String`.

> **Важно!** Не используется с другими типами кнопок.

```js
{
    block: 'x-table',
    head: ['Поле url'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', type: 'link' },
            url: 'https://lego.yandex-team.ru/',
            text: 'Сайт Лего'
        }
    ]
}
```

<a name="field-target"></a>

#### Поле `target`

Определяет поведение [кнопки-ссылки](#type-link). Принимает все допустимые значения HTML-атрибута target: `_blank`, `_self` (используется по умолчанию), `_parent`, `_top`.

Тип: `String`.

> **Важно!** Не используется с другими типами кнопок.

```js
{
    block: 'x-table',
    head: ['Поле target'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', type: 'link' },
            url: 'https://lego.yandex-team.ru/',
            target: '_blank',
            text: 'Сайт Лего'
        }
    ]
}
```

<a name="field-title"></a>

#### Поле `title`

Определяет содержание всплывающей подсказки.

Тип: `String`.

> **Примечание.** Вид такой подсказки зависит от браузера, настроек операционной системы и не может быть изменен с помощью HTML-кода или стилей.

```js
{
    block: 'x-table',
    head: ['Поле title'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', type: 'link' },
            url: 'https://lego.yandex-team.ru/',
            target: '_blank',
            title: 'Сайт Лего',
            text: 'Сайт Лего'
        }
    ]
}
```

<a name="field-id"></a>

#### Поле `id`

Определяет уникальный идентификатор кнопки.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле id'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', type: 'submit' },
            id: 'lego',
            text: 'Кнопка'
        }
    ]
}
```

<a name="field-tabindex"></a>

#### Поле `tabindex`

Определяет порядок получения фокуса при переходе между контролами с помощью клавиши `Tab`.

Тип: `Number`.

```js
{
    block: 'x-table',
    head: ['Поле tabindex'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', type: 'submit' },
            text: 'Кнопка',
            tabindex: 2
        }
    ]
}
```

<a name="field-presskeys"></a>

#### Поле `pressKeys`

Список кнопок с кодами клавиш, по которым произойдет событие `keypress`.

Тип: `String[]`.

```js
{
    block: 'x-table',
    head: ['Поле pressKeys'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', type: 'link' },
            url: 'https://yandex.ru/',
            text: 'Yandex',
            target: 'blank',
            pressKeys: ['ENTER']
        }
    ]
}
```

<a name="field-prvntkeys"></a>

#### Поле `prvntKeys`

Список кнопок с кодами клавиш, по которым произойдет `e.preventDefault()` для события `keydown`.

Тип: `String[]`.

```js
{
    block: 'x-table',
    head: ['Поле prvntKeys'],
    body: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm', type: 'link' },
            url: 'https://yandex.ru/',
            text: 'Yandex',
            target: 'blank',
            prvntKeys: ['SPACE']
        }
    ]
}
```