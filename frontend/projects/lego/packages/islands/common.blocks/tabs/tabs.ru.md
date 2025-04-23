# tabs

Используется для создания вкладок в виде меню или кнопок.

> **Примечание.** Вы можете [реализовать собственный блок](#custom-control) с вкладками нужного вида.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [control](#mods-control) (req) | `menu`, `buttons` | `BEMJSON`, `JS` | Вид вкладок и реализующий блок. |
| [size](#mods-size) | `s`, `m` | `BEMJSON`, `JS` | Размер вкладок. |
| [theme](#mods-theme) | `normal` | `BEMJSON`, `JS` | Стиливое оформления вкладок. |
| [layout](#mods-layout) | `horiz` | `BEMJSON`, `JS` | Расположение вкладок. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [panes](#fields-panes) | `String` | Строковый идентификатор, для связи `tabs` и `tabs-panes`. |

## Подробное описание

### Модификаторы блока

<a name="mods-control"></a>

#### Модификатор `control`

Определяет вид вкладок и блок, на основе которого они будут реализованы. **Обязательный**.

Допустимые значения | Описание
--- | ---
`menu` | Меню вкладок на основе блока [tabs-menu](../tabs-menu/tabs-menu.ru.md). Содержимое блока `tabs` передается в `соntent` блока `tabs-menu`. При этом все элементы и модификаторы будут находиться в контексте `tabs-menu`, а не `tabs`. Для блока `tabs-menu` нужно самостоятельно передать модификаторы `size`, `theme`, `layout` и добавить их зависимости.
`buttons` | Вкладки в виде кнопок на основе блока [radio-button](../radio-button/radio-button.ru.md). Содержимое элементов `tab` преобразуется в элементы `radio` блока `radio-button`. В контексте элементов `tab` можно передать любые параметры, специфичные для `radio`. По умолчанию для `value` радиокнопки выставляется его порядковый номер (начиная с 0). Также в `BEMJSON` блока `tabs` можно передать `nam`e для `radio-button`, иначе он будет сгенерирован автоматически.
Для блока `radio-button` нужно самостоятельно передать модификаторы `size`, `theme` и добавить их в зависимости.

Способы установки: `BEMJSON`, `JS`.

**Вкладки в виде меню**

```js
[
    {
        block: 'tabs',
        mods: { control: 'menu', size: 'm', theme: 'normal', layout: 'horiz' },
        panes: 'tabs',
        content: [
            { elem: 'tab', content: 'Tab 1', elemMods: { active: 'yes' } },
            { elem: 'tab', content: 'Tab 2' },
            { elem: 'tab', content: 'Tab 3', elemMods: { disabled: 'yes' } },
            { elem: 'tab', content: 'Tab 4' }
        ]
    },
    {
        block: 'tabs-panes',
        id: 'tabs',
        content: [
            { elem: 'pane', content: 'Pane 1', elemMods: { active: 'yes' } },
            { elem: 'pane', content: 'Pane 2' },
            { elem: 'pane', content: 'Pane 3' },
            { elem: 'pane', content: 'Pane 4' }
        ]
    },
    {
        block: 'x-deps',
        content: { block: 'tabs-menu', mods: { theme: 'normal', size: 'm', layout: 'horiz' } }
    }
]
```

**Вкладки в виде кнопок**

```js
[
    {
        block: 'tabs',
        mods: { control: 'buttons', size: 'm', theme: 'normal', layout: 'horiz' },
        panes: 'tabs',
        content: [
            { elem: 'tab', content: 'Tab 1', elemMods: { active: 'yes' } },
            { elem: 'tab', content: 'Tab 2' },
            { elem: 'tab', content: 'Tab 3', elemMods: { disabled: 'yes' } },
            { elem: 'tab', content: 'Tab 4' }
        ]
    },
    {
        block: 'tabs-panes',
        id: 'tabs',
        content: [
            { elem: 'pane', content: 'Pane 1', elemMods: { active: 'yes' } },
            { elem: 'pane', content: 'Pane 2' },
            { elem: 'pane', content: 'Pane 3' },
            { elem: 'pane', content: 'Pane 4' }
        ]
    },
    {
        block: 'x-deps',
        content: { block: 'radio-button', mods: { theme: 'normal', size: 'm' } }
    }
]
```

<a name="mods-size"></a>

#### Модификатор `size`

Определяет размер вкладок.

Допустимые значения: `s`, `m`.

Способы установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['s', 'm'],
        body: [
            ['s', 'm'].map((size) => {
                return {
                    block: 'tabs',
                    mods: { control: 'buttons', size: size, theme: 'normal', layout: 'horiz' },
                    content: [
                        { elem: 'tab', content: 'Tab 1', elemMods: { active: 'yes' } },
                        { elem: 'tab', content: 'Tab 2' },
                        { elem: 'tab', content: 'Tab 3', elemMods: { disabled: 'yes' } },
                        { elem: 'tab', content: 'Tab 4' }
                    ]
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'radio-button', mods: { theme: 'normal', size: 's'} },
            { block: 'radio-button', mods: { theme: 'normal', size: 'm'} }
            ]
    }
]
```

<a name="mods-theme"></a>

#### Модификатор `theme`

Определяет тему оформления вкладок.

Допустимые значения: `normal`.

Способы установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'tabs',
        mods: { control: 'buttons', size: 'm', theme: 'normal', layout: 'horiz' },
        content: [
            { elem: 'tab', content: 'Tab 1', elemMods: { active: 'yes' } },
            { elem: 'tab', content: 'Tab 2' },
            { elem: 'tab', content: 'Tab 3', elemMods: { disabled: 'yes' } },
            { elem: 'tab', content: 'Tab 4' }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'radio-button', mods: { theme: 'normal', size: 'm'} }
            ]
    }
]
```

<a name="mods-layout"></a>

#### Модификатор `layout`

Определяет расположение вкладок. Необходимо использовать с модификатором `control` в значении `menu`.

Допустимые значения: `horiz`.

Способы установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'tabs',
        mods: { control: 'menu', size: 'm', theme: 'normal', layout: 'horiz' },
        content: [
            { elem: 'tab', content: 'Tab 1', elemMods: { active: 'yes' } },
            { elem: 'tab', content: 'Tab 2' },
            { elem: 'tab', content: 'Tab 3', elemMods: { disabled: 'yes' } },
            { elem: 'tab', content: 'Tab 4' }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'tabs-menu', mods: { theme: 'normal', size: 'm', layout: 'horiz' } }
        ]
    }
]
```

### Поля блока

<a name="fields-panes"></a>

#### Поле `panes`

Определяет строковый идентификатор, для связи `tabs` и `tabs-panes`.

> **Примечание.** Чтобы панели переключались по клику на вкладку, в блоке `tabs-panes` значения полей `panes` и `id`  должны совпадать.

Тип: `String`.

```js
[
    {
        block: 'tabs',
        mods: { control: 'menu', size: 'm', theme: 'normal', layout: 'horiz' },
        panes: 'tabs',
        content: [
            { elem: 'tab', content: 'Tab 1', elemMods: { active: 'yes' } },
            { elem: 'tab', content: 'Tab 2' }
        ]
    },
    {
        block: 'tabs-panes',
        id: 'tabs',
        content: [
            { elem: 'pane', content: 'Pane 1', elemMods: { active: 'yes' } },
            { elem: 'pane', content: 'Pane 2' }
        ]
    },
    {
        block: 'x-deps',
        content: { block: 'tabs-menu', mods: { theme: 'normal', size: 'm', layout: 'horiz' } }
    }
]
```