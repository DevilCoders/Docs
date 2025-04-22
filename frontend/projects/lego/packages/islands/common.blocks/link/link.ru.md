# link

Используется для создания ссылок различных типов.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [theme](#mods-theme) (req) | `'normal'`, `'black'`, `'ghost'`, `'outer'`, `'pseudo'`, `'strong'` | `BEMJSON` | Стилевое оформление. |
| [pseudo](#mods-pseudo) | `'yes'` | `BEMJSON` | Псевдоссылка. |
| [inner](#mods-inner) | `'yes'` | `BEMJSON` | Ссылка с вложенным элементом. |
| [nonvisual](#mods-nonvisual) | `'yes'` | `BEMJSON` | Невизуальная ссылка. |
| [disabled](#mods-disabled) | `'yes'` | `BEMJSON`, `JS` | Неактивное состояние. |
| [focused](#mods-focused) | `'yes'` | `BEMJSON`, `JS` | Фокус на блоке. |
| [pressed](#mods-pressed) | `'yes'` | — | Нажатие на ссылку. |
| [hovered](#mods-hovered) | `'yes'` | — | Наведение на ссылку курсором. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [text](#field-text) | `String`, `BEMJSON` | Текст ссылки (`String`. Переданное значение экранируется автоматически). Доопределение элемента [inner](#elem-inner) (`BEMJSON`). |
| [icon](#field-icon) | `BEMJSON` | Иконка ссылки. Формируется блоком [icon](../icon/icon.ru.md). |
| [iconLeft](#field-iconLeft) | `BEMJSON` | Иконка слева от текста ссылки. Формируется блоком [icon](../icon/icon.ru.md). |
| [iconRight](#field-iconLeft) | `BEMJSON` | Иконка справа от текста ссылки. Формируется блоком [icon](../icon/icon.ru.md). |
| [content](#field-content) | `BEMJSON` | Содержимое ссылки. Используется для формирования произвольной HTML-разметки, с помощью [элементов блока](#elems). Переопределяет значения заданные в полях `text`, `icon`. |
| [name](#field-name) | `String` | Уникальное имя блока. |
| [url](#field-url) | `String` | Адрес ссылки. |
| [target](#field-target) | `String` | Поведение ссылки. |
| [title](#field-title) | `String` | Текст всплывающей подсказки. |
| [id](#field-id) | `String` | Уникальный идентификатор ссылки. |
| [tabindex](#field-tabindex) | `Number` | Последовательность перехода между контролами при нажатии на `Tab`. |

<a name="elems"></a>

### Элементы блока

| Элемент | Описание |
| ------- | -------- |
| [inner](#elem-inner) | Текст ссылки с левым отступом. |
| [icon](#elem-icon) | Иконка ссылки. Формируется блоком [icon](../icon/icon.ru.md). |

## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Отвечает за стилевое оформление ссылок.

Допустимое значение: `'normal'`, `'black'`, `'ghost'`, `'outer'`, `'pseudo'`, `'strong'`.

Способ установки: `BEMJSON`.

<a name="theme-normal"></a>

**Обычная ссылка (модификатор `theme` в значении `normal`)**

Используется в большинстве случаев.

```js
{
    block: 'link',
    mods: { theme: 'normal' },
    text: 'Тема normal'
}
```

<a name="theme-black"></a>

**Ссылка черного цвета (модификатор `theme` в значении `black`)**

Используется при необходимости сделать ссылку под цвет текста.

```js
{
    block: 'link',
    mods: { theme: 'black' },
    text: 'Тема black'
}
```

<a name="theme-ghost"></a>

**Ссылка серого цвета (модификатор `theme` в значении `ghost`)**

Используется при необходимости сделать ссылку менее заметной на странице.

```js
{
    block: 'link',
    mods: { theme: 'ghost' },
    text: 'Тема ghost'
}
```

<a name="theme-outer"></a>

**Внешняя ссылка (модификатор `theme` в значении `outer`)**

Используется для визуального выделения ссылок, которые ведут на внешние ресурсы.

```js
{
    block: 'link',
    mods: { theme: 'outer' },
    text: 'Тема outer'
}
```

<a name="theme-pseudo"></a>

**Второстепенная ссылка (модификатор `theme` в значении `pseudo`)**

Используется для визуального выделения второстепенных ссылок на странице.

```js
{
    block: 'link',
    mods: { theme: 'pseudo', pseudo: 'yes' },
    text: 'Тема pseudo'
}
```

> **Важно!** Необходимо использовать с модификатором `pseudo`.

<a name="theme-strong"></a>

**Жирная ссылка (модификатор `theme` в значении `strong`)**

Используется для визуального выделения важных ссылок на странице.

```js
{
    block: 'link',
    mods: { theme: 'strong' },
    text: 'Тема strong'
}
```

<a name="mods-pseudo"></a>

#### Модификатор `pseudo`

Определяет псевдоссылку. Отличается от обычной ссылки тем, что при клике по ссылке переход на новую страницу не осуществляется.

Допустимое значение: `'yes'`.

Способ установки: `BEMJSON`.

```js
{
    block: 'x-table',
    head: ['_pseudo'],
    body: [
        {
            block: 'link',
            mods: { theme: 'pseudo', pseudo: 'yes' },
            url: 'https://lego.yandex-team.ru',
            text: 'Псевдоссылка'
        }
    ]
}
```

> **Примечание.** При отсутствии поля `url` в `BEMJSON`, ссылка в HTML будет представлена тегом `<span>`.

<a name="mods-inner"></a>

#### Модификатор `inner`

Ссылка с вложенным элементом.

Допустимое значение: `'yes'`.

Способ установки: `BEMJSON`.

Используется для формирования произвольной HTML-разметки, например, ссылок с иконками.

```js
{
    block: 'x-table',
    head: ['_inner'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal', inner: 'yes' },
            attrs: { style: 'font-size: 14px;' },
            url: 'https://lego.yandex-team.ru',
            icon: {
                    block: 'country-flag',
                    mods: { s16: 'ar' },
                    mix: { block: 'link', elem: 'icon' }
            },
            text: 'Ссылка с иконкой'
        }
    ]
}
```

> **Примечание.** Обязательно задавайте иконке микс `link__icon`.

<a name="mods-nonvisual"></a>

#### Модификатор `nonvisual`

Определяет невидимую ссылку.

Допустимое значение: `'yes'`.

Способ установки: `BEMJSON`.

```js
[
    {
        tag: 'p',
        content: 'Ссылка станет видимой при получении фокуса'
    },
    {
        block: 'link',
        mods: { theme: 'normal' },
        url: '#nonvisual',
        text: 'Невизуальная ссылка'
    },
    '.\u00a0\u00a0',
    {
        block: 'link',
        mods: { theme: 'normal', nonvisual: 'yes' },
        id: 'nonvisual',
        url: 'https://lego.yandex-team.ru',
        text: 'Привет, я Невизуальная ссылка'
    }
]
```

> **Примечание.** Применяется только в шапке.

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Отвечает за неактивное состояние, при котором ссылка видна, но недоступна для действий пользователя, а именно нельзя:

* установить модификаторы `focused`, `pressed` и `hovered` (существующие удаляются);
* вызвать БЭМ-события;
* перейти по ссылке (существующий атрибут `href` удаляется).

> **Примечание.** Неактивное состояние ссылки можно изменять программно.

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['_disabled'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal', disabled: 'yes' },
            url: 'https://lego.yandex-team.ru',
            content: 'Ссылка неактивна'
        }
    ]
}
```

<a name="mods-focused"></a>

#### Модификатор `focused`

Отвечает за установку фокуса.

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

Выставляется автоматически при получении блоком фокуса.

```js
{
    block: 'x-table',
    head: ['_focused'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal', focused: 'yes' },
            url: 'https://lego.yandex-team.ru',
            content: 'В фокусе'
        }
    ]
}
```

<a name="mods-pressed"></a>

#### Модификатор `pressed`

Определяет действие «нажатие на ссылку».

Допустимое значение: `yes`.

Способы установки: `—`.

Выставляется автоматически.

<a name="mods-hovered"></a>

#### Модификатор `hovered`

Определяет действие «наведение на ссылку курсором».

Допустимое значение: `yes`.

Способы установки: `—`.

Выставляется автоматически.

### Поля блока

<a name="field-text"></a>

#### Поле `text`

Определяет текст ссылки.

Тип: `String`, `BEMJSON`.

```js
{
    block: 'x-table',
    head: ['String', 'BEMJSON'],
    body: [
        ['Black & White', { content: 'Black & White' }].map(function(value) {
            return {
                block: 'link',
                mods: { theme: 'normal' },
                url: 'https://lego.yandex-team.ru',
                text: value  // Переданное значение экранируется автоматически
            };
        })
    ]
}
```

> **Примечание.** Переданное значение экранируется автоматически.

<a name="field-icon"></a>

#### Поле `icon`

Определяет иконку ссылки. Иконка задается с помощью блока [icon](../icon/icon.ru.md).

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле icon'],
        body: [
            {
                block: 'link',
                mods: { theme: 'normal' },
                url: 'https://lego.yandex-team.ru',
                icon: {
                    mods: { type: 'load' }
                },
                text: 'Ссылка с иконкой'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'link', elem: 'icon' },
            { block: 'icon', mods: { type: 'load' } }
        ]
    }
]
```

<a name="field-iconLeft"></a>

#### Поля `iconLeft` / `iconRight`

Определяет иконку, которая отображается слева (или справа) от текста ссылки. Иконка задается с помощью блока [icon](../icon/icon.ru.md).

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле icon'],
        body: [
            {
                block: 'link',
                mods: { theme: 'normal' },
                url: 'https://lego.yandex-team.ru',
                iconLeft: {
                    mods: { type: 'load' }
                },
                iconRight: {
                    mods: { type: 'load' }
                },
                text: 'Ссылка с иконкой слева'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'link', elem: 'icon' },
            { block: 'icon', mods: { type: 'load' } }
        ]
    }
]
```
<a name="field-content"></a>

#### Поле `content`

Определяет содержимое ссылки отличное от текстового. Используется для формирования произвольной HTML-разметки.

Тип: `BEMJSON`.

```js
{
    block: 'x-table',
    head: ['Поле content'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal' },
            url: 'https://lego.yandex-team.ru',
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

> **Важно!** Переопределяет значения заданные в полях `text`, `icon`.

<a name="field-name"></a>

#### Поле `name`

Определяет уникальное имя блока.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле name'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal' },
            url: 'https://lego.yandex-team.ru',
            name: 'lego',
            text: 'Сайт Лего'
        }
    ]
}
```

<a name="field-url"></a>

#### Поле `url`

Определяет адрес ссылки.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле url'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal' },
            url: 'https://lego.yandex-team.ru',
            text: 'Сайт Лего'
        }
    ]
}
```

<a name="field-target"></a>

#### Поле `target`

Определяет поведение ссылки. Принимает все допустимые значения HTML-атрибута target: `_blank`, `_self` (используется по умолчанию), `_parent`, `_top`.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле target'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal' },
            url: 'https://lego.yandex-team.ru',
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

```js
{
    block: 'x-table',
    head: ['Поле title'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal' },
            url: 'https://lego.yandex-team.ru',
            title: 'Сайт Лего',
            text: 'Сайт Лего'
        }
    ]
}
```

> **Примечание.** Вид такой подсказки зависит от браузера, настроек операционной системы и не может быть изменен с помощью HTML-кода или стилей.

<a name="field-id"></a>

#### Поле `id`

Определяет уникальный идентификатор ссылки.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле id'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal' },
            url: 'https://lego.yandex-team.ru',
            id: 'lego',
            text: 'Сайт Лего'
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
            block: 'link',
            mods: { theme: 'normal' },
            url: 'https://lego.yandex-team.ru',
            text: 'Сайт Лего',
            tabIndex: 2
        }
    ]
}
```

### Элементы блока

<a name="elem-inner"></a>

#### Элемент `inner`

Определяет текст ссылки с левым отступом.

Используется вместе с иконкой.

```js
{
    block: 'x-table',
    head: ['__inner'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal' },
            attrs: { style: 'font-size: 14px;' },
            url: 'https://lego.yandex-team.ru',
            content: [
                {
                    block: 'country-flag',
                    mods: { s16: 'ar' },
                    mix: { block: 'link', elem: 'icon' }
                },
                {
                    elem: 'inner',
                    content: 'Ссылка с иконкой'
                }
            ]
        }
    ]
}
```

> **Примечание.** Используется для самостоятельной настройки параметров блока.

<a name="elem-icon"></a>

#### Элемент `icon`

Определяет иконку ссылки. Элемент `icon` миксуется к блоку [icon](../icon/icon.ru.md).

```js
{
    block: 'x-table',
    head: ['__icon'],
    body: [
        {
            block: 'link',
            mods: { theme: 'normal' },
            url: 'https://lego.yandex-team.ru',
            content: {
                block: 'icon',
                mods: { type: 'load' },
                mix: { block: 'link', elem: 'icon' }
            }
        }
    ]
}
```

> **Примечание.** Используется для самостоятельной настройки параметров блока.
