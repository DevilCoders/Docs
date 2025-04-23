# dropdown2

Используется для создания выпадающих элементов интерфейса. Формируется блоком [popup2](../popup2/popup2.ru.md) и блоком-переключателем: кнопкой или ссылкой.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [switcher](#mods-switcher) (req) | `button` (dep), `button2`, `link` | `BEMJSON` | Тип блока-переключателя. |
| [theme](#mods-theme) (req) | Соответствуют значениям блока-переключателя. | `BEMJSON`, `JS` | Тема оформления. |
| [size](#mods-size) | Соответствуют значениям блока-переключателя. | `BEMJSON`, `JS` | Размер блока-переключателя. |
| [tone](#mods-tone) | `default`, `red`, `grey`, `dark` | `BEMJSON`, `JS` | Цветовой тон блока. |
| [view](#mods-view) | `default`, `classic` | `BEMJSON`, `JS` | Вид блока. |
| [has-tail](#mods-has-tail) | `yes` | `BEMJSON`, `JS` | «Хвостик» выпадающего окна. Формируется элементом [popup2__tail](../popup2/popup2.ru.md). |
| [has-tick](#mods-has-tick) | `yes` | `BEMJSON`, `JS` | Иконка-стрелка на кнопке-переключателе. Формируется блоком [icon](../icon/icon.ru.md). |
| [disabled](#mods-disabled) | `yes` | `BEMJSON`, `JS` | Неактивное состояние. |
| [opened](#mods-opened) | `yes` | `BEMJSON`, `JS` | Выпадающее окно раскрыто. |

req — обязательный модификатор.

dep — устаревшее значение.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [switcher](#field-switcher) | `String`, `Number`, `BEMJSON` | Содержимое блока-переключателя. |
| [popup](#field-popup) | `String`, `Number`, `BEMJSON` | Содержимое выпадающего окна. |

## Подробное описание

### Модификаторы блока

<a name="mods-switcher"></a>

#### Модификатор `switcher`

Определяет блок-переключатель: кнопку, ссылку. **Обязательный**.

Допустимые значения: `button2`, `link`.

Способ установки: `BEMJSON`, `JS`.

> **Примечание.** Кнопка формируется блоком [button2](../button2/button2.ru.md). Ссылка формируется блоком [link](../link/link.ru.md) с обязательным модификатором `link_pseudo_yes`.

```js
[
    {
        block: 'x-table',
        head: ['_switcher_button2', '_switcher_link'],
        body: [
            ['button2', 'link'].map((switcher) => {
                return {
                    block: 'dropdown2',
                    mods: { switcher: switcher, theme: 'normal', size: 'm' },
                    switcher: 'Сервис',
                    popup: {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk' },
                            { text: 'Яндекс.Карты', val: 'maps' },
                            { text: 'Яндекс.Погода', val: 'pogoda' },
                            { text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            ['link', 'button2'].map((block) => {
                return {
                    block: block,
                    mods: (block == 'button2') ? { theme: 'normal', size: 'm' } :
                    { theme: 'normal' }
                };
            })
        ]
    }
]
```

<a name="mods-theme"></a>

#### Модификатор `theme`

Отвечает за тему оформления кнопки. **Обязательный**.

Допустимые значения: в зависимости от блока-переключателя см.: [button2](../button2/button2.ru.md), [link](../link/link.ru.md).

Способ установки: `BEMJSON`, `JS`.

**Переключатель — кнопка (dropdown2_switcher_button2)**

```js
[
    {
        block: 'x-table',
        head: ['_theme_normal', '_theme_raised', '_theme_action', '_theme_pseudo', '_theme_link', '_theme_clear'],
        body: [
            ['normal', 'raised', 'action', 'pseudo', 'link', 'clear'].map((theme) => {
                return {
                    block: 'dropdown2',
                    mods: { switcher: 'button2', theme: theme, size: 'm' },
                    switcher: 'Сервис',
                    popup: {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk' },
                            { text: 'Яндекс.Карты', val: 'maps' },
                            { text: 'Яндекс.Погода', val: 'pogoda' },
                            { text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            ['normal', 'raised', 'action', 'pseudo', 'link', 'clear'].map((theme) => {
                return {
                    block: 'button2', mods: { theme: theme, size: 'm' }
                };
            })
        ]
    }
]
```

**Переключатель — ссылка (dropdown2_switcher_link)**

```js
[
    {
        block: 'x-table',
        head: ['_theme_normal', '_theme_black', '_theme_ghost', '_theme_outer', '_theme_pseudo', '_theme_strong'],
        body: [
            ['normal', 'black', 'ghost', 'outer', 'pseudo', 'strong'].map((theme) => {
                return {
                    block: 'dropdown2',
                    mods: { switcher: 'link', theme: theme },
                    switcher: 'Сервис',
                    popup: {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk' },
                            { text: 'Яндекс.Карты', val: 'maps' },
                            { text: 'Яндекс.Погода', val: 'pogoda' },
                            { text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            ['normal', 'black', 'ghost', 'outer', 'pseudo', 'strong'].map((theme) => {
                return {
                    block: 'link', mods: { theme: theme }
                };
            })
        ]
    }
]
```

<a name="mods-size"></a>

#### Модификатор `size`

Определяет размер кнопки-переключателя. **Обязательный**, если модификатор `switcher` в значении `button2`.

Допустимые значения: `xs`, `s`, `ns`, `n`, `m`, `l`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Ссылка-переключатель формируется блоком [link](../link/link.ru.md), поэтому не имеет модификатора `size`.

```js
[
    {
        block: 'x-table',
        head: ['_size_xs', '_size_s', '_size_ns', '_size_n', '_size_m', '_size_l'],
        body: [
            ['xs', 's', 'ns', 'n', 'm', 'l'].map((size) => {
                return {
                    block: 'dropdown2',
                    mods: { switcher: 'button2', theme: 'normal', size: size },
                    switcher: 'Сервис',
                    popup: {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk' },
                            { text: 'Яндекс.Карты', val: 'maps' },
                            { text: 'Яндекс.Погода', val: 'pogoda' },
                            { text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            ['xs', 's', 'ns', 'n', 'm', 'l'].map((size) => {
                return {
                    block: 'button2', mods: { theme: 'normal', size: size }
                };
            })
        ]
    }
]
```

<a name="mods-tone"></a>

#### Модификатор `tone`

Определяет цветовой тон блока.

Допустимые значения: `default`, `red`, `grey`, `dark`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Необходимо использовать с модификатором `view` в значении `default`.

```js
[
    {
        block: 'x-table',
        head: ['_tone_default', '_tone_red', '_tone_grey', '_tone_dark'],
        body: [
            ['default', 'red', 'grey', 'dark'].map((tone) => {
                return {
                    block: 'dropdown2',
                    mods: { switcher: 'button2', theme: 'normal', size: 'm', view: 'default', tone: tone },
                    switcher: 'Сервис',
                    popup: tone
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            ['default', 'red', 'grey', 'dark'].map((tone) => {
                return [
                    {
                        block: 'button2', mods: { theme: 'normal', size: 'm', view: 'default', tone: tone }
                    },
                    {
                        block: 'popup2', mods: { theme: 'normal', size: 'm', view: 'default', tone: tone }
                    }
                ];
            })
        ]
    }
]
```

<a name="mods-view"></a>

#### Модификатор `view`

Определяет вид блока.

Допустимые значения: `default`, `classic`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Модификатор `view` в значении `default` необходимо использовать с модификатором `tone`.

```js
[
    {
        block: 'x-table',
        head: ['_view_default', '_view_classic'],
        body: [
            ['default', 'classic'].map((view) => {
                return {
                    block: 'dropdown2',
                    mods: { switcher: 'button2', theme: 'normal', size: 'm', view: view, tone: 'default' },
                    switcher: 'Сервис',
                    popup: view
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            ['default', 'classic'].map((view) => {
                return [
                    {
                        block: 'button2', mods: { theme: 'normal', size: 'm', view: view, tone: 'default' }
                    },
                    {
                        block: 'popup2', mods: { theme: 'normal', size: 'm', view: view, tone: 'default' }
                    }
                ];
            })
        ]
    }
]
```

<a name="mods-has-tail"></a>

#### Модификатор `has-tail`

Добавляет «Хвостик» выпадающему окну.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['_has-tail_yes'],
        body: [
            ['default', 'red', 'grey', 'dark'].map((tone) => {
                return {
                    block: 'dropdown2',
                    mods: { switcher: 'button2', theme: 'normal', size: 'm', view: 'default', tone: tone, 'has-tail': 'yes' },
                    switcher: 'Сервис',
                    popup: tone
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            ['default', 'red', 'grey', 'dark'].map((tone) => {
                return [
                    {
                        block: 'button2', mods: { theme: 'normal', size: 'm', view: 'default', tone: tone }
                    },
                    {
                        block: 'popup2', mods: { theme: 'normal', size: 'm', view: 'default', tone: tone }
                    }
                ];
            })
        ]
    }
]
```

<a name="mods-has-tick"></a>

#### Модификатор `has-tick`

Добавляет иконку-стрелку на кнопку-переключатель. Формируется блоком [icon](../icon/icon.ru.md).

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Не используется с ссылкой-переключателем (т.е. модификатор `switcher` выставлен в значение [link](#mods-switcher)).

```js
[
    {
        block: 'x-table',
        head: ['_has-tick_yes'],
        body: [
            {
                block: 'dropdown2',
                mods: { switcher: 'button2', theme: 'normal', size: 'm', 'has-tick': 'yes' },
                switcher: 'Сервис',
                popup: {
                    block: 'menu',
                    mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                    items: [
                        { text: 'Яндекс.Диск', val: 'disk' },
                        { text: 'Яндекс.Карты', val: 'maps' },
                        { text: 'Яндекс.Погода', val: 'pogoda' },
                        { text: 'Яндекс.Переводчик', val: 'translate' }
                    ]
                }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', mods: { theme: 'normal', size: 'm' } },
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { type: 'arrow' } }
        ]
    }
]
```

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Определяет неактивное состояние, при котором блок виден, но недоступен для действий пользователя.

С модификатором `disabled` невозможно:

* установить модификаторы на блоки-переключатели: `opened`, `focused`, `pressed` и `hovered` (существующие удаляются);
* вызвать БЭМ-события.

Допустимое значение: `yes`.

Способы установки: `BEMJSON`, `JS`.

> **Примечание.** Неактивное состояние блока можно изменять программно.

```js
[
    {
        block: 'x-table',
        head: ['_disabled'],
        body: [
            {
                block: 'dropdown2',
                mods: { switcher: 'button2', theme: 'normal', size: 'm', disabled: 'yes' },
                switcher: 'Сервис',
                popup: {
                    block: 'menu',
                    mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                    items: [
                        { text: 'Яндекс.Диск', val: 'disk' },
                        { text: 'Яндекс.Карты', val: 'maps' },
                        { text: 'Яндекс.Погода', val: 'pogoda' },
                        { text: 'Яндекс.Переводчик', val: 'translate' }
                    ]
                }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', mods: { theme: 'normal', size: 'm' } }
        ]
    }
]
```

<a name="mods-opened"></a>

#### Модификатор `opened`

Определяет открытое состояние выпадающего окна на странице. Выставляется автоматически при открытии окна.

Допустимое значение: `yes`.

Способы установки: `JS`.

### Поля блока

<a name="field-switcher"></a>

#### Поле `switcher`

Определяет содержимое блока-переключателя.

Тип: `String`, `Number`, `BEMJSON`.

> **Примечание.** Тип `BEMJSON` используется для самостоятельной настройки параметров блока-переключателя.

```js
[
    {
        block: 'x-table',
        head: ['String', 'Number', 'BEMJSON'],
        body: [
            ['Сервис', 1, {
                block: 'button2',  // Переопределяет значения заданные в поле mods блока dropdown2
                mods: { theme: 'action', size: 'm' },
                icon: { mods: { type: 'load' } }
            } ].map((switcher) => {
                return {
                    block: 'dropdown2',
                    mods: { switcher: 'button2', theme: 'normal', size: 'm' },
                    switcher: (switcher == 1) ? new Date().getFullYear() : switcher,
                    popup: {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk' },
                            { text: 'Яндекс.Карты', val: 'maps' },
                            { text: 'Яндекс.Погода', val: 'pogoda' },
                            { text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            ['normal', 'action'].map((theme) => {
                return {
                    block: 'button2', mods: { theme: theme, size: 'm' }
                };
            }),
            { block: 'button2', elem: 'icon' },
            { block: 'icon', mods: { type: 'load' } }
        ]
    }
]
```

<a name="field-popup"></a>

#### Поле `popup`

Определяет содержимое выпадающего окна.

Тип: `String`, `Number`, `BEMJSON`.

> **Примечание.** Тип `BEMJSON` используется для самостоятельной настройки параметров выпадающего окна (блок [popup2](../popup2/popup2.ru.md)). По умолчанию блоку `popup2` добавляются следующие модификаторы: `_target_anchor`, `_autoclosable_yes`, `_theme_normal`.

```js
[
    {
        block: 'x-table',
        head: ['String', 'Number', 'BEMJSON'],
        body: [
            ['popup', 1, {
                block: 'popup2',
                directions: ['right-center'],
                content: 'custom directions' }
            ].map((popup) => {
                return {
                    block: 'dropdown2',
                    mods: { switcher: 'button2', theme: 'normal', size: 'm', view: 'default', tone: 'red', 'has-tail': 'yes' },
                    switcher: 'Сервис',
                    popup: (popup == 1) ? new Date().getFullYear() : popup
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            {
                block: 'button2', mods: { theme: 'normal', size: 'm', view: 'default', tone: 'red' }
            },
            {
                block: 'popup2', mods: { theme: 'normal', size: 'm', view: 'default', tone: 'red' }
            }
        ]
    }
]
```