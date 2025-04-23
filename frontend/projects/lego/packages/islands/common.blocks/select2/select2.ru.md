# select2

Используется для создания раскрывающегося списка с возможностью одиночного или множественного выбора.

> **Важно!** Не стоит использовать блок внутри элементов с position `sticky` в браузерах Chromium, Google Chrome и Яндекс Браузер. (Например https://st.yandex-team.ru/SERP-63753)

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [theme](#mods-theme) (req) | `'normal'`, `'pseudo'` | `BEMJSON`, `JS` | Стилевое оформление. |
| [size](#mods-size) (req) | `'xs'`, `'s'`, `'m'`, `'n'` | `BEMJSON`, `JS` | Размер блока. |
| [type](#mods-type) | `'check'`, `'radio'`, `'radiocheck'` | `BEMJSON` | Режим выбора пунктов раскрывающегося списка. В большинстве случаев используется с модификатором [text](#mods-text). |
| [text](#mods-text) | `'vary'` | `BEMJSON`, `JS` | Возможность обновить текст на кнопке раскрывающегося списка при изменении значения. |
| [item-icon-hidden](#mods-item-icon-hidden) | `'yes'` | `BEMJSON`, `JS` | Возможность скрыть иконки в пунктах раскрывающегося списка. |
| [native](#mods-native) | `'yes'` | `BEMJSON`, `JS` | Возможность использовать нативный элемент управления для `touch`-устройств. Необходимо использовать с модификатором `type` в значении `check`/`radio` и полем [control](#field-control). |
| [tone](#mods-tone) | `'default'`, `'red'`, `'grey'`, `'dark'` | `BEMJSON`, `JS` | Тон блока. Необходимо использовать с модификатором `view` в значении `default`. |
| [view](#mods-view) | `'classic'`, `'default'` | `BEMJSON`, `JS` | Вид блока. |
| [width](#mods-width) | `'fixed'`, `'max'` | `BEMJSON`, `JS` | Ширина блока. |
| [disabled](#mods-disabled) | `'yes'` | `BEMJSON`, `JS` | Неактивное состояние. |
| [focused](#mods-focused) | `'yes'` | `BEMJSON`, `JS` | Фокус на блоке. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [text](#field-text) | `String` | Значение, которое отображается в кнопке раскрывающегося списка. Если установлен модификатор [text](#mods-text), значение поля подменяется текстом выбранного пункта. |
| [items](#field-items) | `Array` | Пункты списка или группы пунктов с опциональным названием. |
| [control](#field-control) | `Boolean`, `BEMJSON` | Вспомогательный элемент управления для отправки данных формы на сервер. Формируется элементом `control`. |
| [name](#field-name) | `String` | Уникальное имя раскрывающегося списка. Используется совместно с полем [control](#field-control). |
| [val](#field-val) | `String`, `Number`, `Array` | Значение, которое будет отправлено на сервер. Принимает массив, если блоку установлен модификатор `type` в значении `check`. |
| [button](#field-button) | `BEMJSON` | Доопределение кнопки раскрывающегося списка. |
| [menu](#field-menu) | `BEMJSON` | Доопределение раскрывающегося списка. |
| [required](#field-required) | `Boolean` | Валидация блока. Используется совместно с полем [control](#field-control). |

<a name="elems"></a>

### Элементы блока

| Элемент | Описание |
| ------- | -------- |
| `button` | Кнопка раскрывающегося списка. |
| `control` | Вспомогательный элемент, позволяющий использовать функциональность нативного элемента управления `INPUT type="hidden"`. |
| `menu` | Меню. |
| `popup` | Всплывающее окно. |

## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Отвечает за стилевое оформление блока. **Обязательный**.

Допустимое значение: `'normal'`, `'pseudo'`.

Способ установки: `BEMJSON`, `JS`.

<a name="theme-normal"></a>

**Обычный список (модификатор `theme` в значении `normal`)**

Используется в большинстве случаев.

```js
[
    {
        block: 'x-table',
        head: ['Тема normal'],
        body: [
            {
                block: 'select2',
                mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary' },
                text: 'Сервис',
                items: [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ]
            }
        ]
    }
]
```

<a name="theme-pseudo"></a>

**Псевдосписок (модификатор `theme` в значении `pseudo`)**

Используется для изменения внешнего вида блока при необходимости сделать список менее заметным на странице.

```js
[
    {
        block: 'x-table',
        mods: { tone: 'default' },
        head: ['Тема pseudo'],
        body: [
            {
                block: 'select2',
                mods: { theme: 'pseudo', size: 'm', type: 'radio', text: 'vary' },
                text: 'Сервис',
                items: [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ]
            }
        ]
    }
]
```

<a name="mods-size"></a>

#### Модификатор `size`

Задает размер блоку. **Обязательный**.

Допустимые значения: `'xs'`, `'s'`, `'m'`, `'n'`.

Способ установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['xs', 's', 'm', 'n'],
        body: [
            ['xs', 's', 'm', 'n'].map(function(size) {
                return {
                    block: 'select2',
                    mods: { theme: 'normal', size: size, type: 'radio', text: 'vary' },
                    text: 'Сервис',
                    items: [
                        { val: 'disk', text: 'Яндекс.Диск' },
                        { val: 'maps', text: 'Яндекс.Карты' },
                        { val: 'pogoda', text: 'Яндекс.Погода' },
                        { val: 'translate', text: 'Яндекс.Переводчик' }
                    ]
                };
            })
        ]
    }
]
```

<a name="mods-type"></a>

#### Модификатор `type`

Определяет режим выбора пунктов раскрывающегося списка.

Допустимые значения: `'check'`, `'radio'`, `'radiocheck'`.

Способ установки: `BEMJSON`.

| Значение | Описание |
| -------- | -------- |
| `'check'` | Позволяет выбрать произвольное количество пунктов в раскрывающемся списке. |
| `'radio'` | Позволяет выбрать только один пункт. Если пункт не выбран, то по умолчанию выбирается первое значение из списка. |
| `'radiocheck'` | Позволяет выбрать только один пункт. Принципиальное отличие от значения `'radio'` в том, что в значении `'radiocheck'` есть возможность оставить список без выбранных пунктов. |

В большинстве случаев используется с модификатором [text](#mods-text).

```js
[
    {
        block: 'x-table',
        head: ['check', 'radio', 'radiocheck'],
        body: [
            ['check', 'radio', 'radiocheck'].map(function(type) {
                return {
                    block: 'select2',
                    mods: { theme: 'normal', size: 'm', type: type, text: 'vary' },
                    text: 'Сервис',
                    items: [
                        { val: 'disk', text: 'Яндекс.Диск' },
                        { val: 'maps', text: 'Яндекс.Карты' },
                        { val: 'pogoda', text: 'Яндекс.Погода' },
                        { val: 'translate', text: 'Яндекс.Переводчик' }
                    ]
                };
            })
        ]
    }
]
```

<a name="mods-text"></a>

#### Модификатор `text`

Определяет возможность обновить текст на кнопке раскрывающегося списка при изменении значения.

По умолчанию текст на кнопке списка не изменяется и определяется полем [text](#field-text).

Допустимые значения: `'vary'`.

Способ установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['без _text_vary', 'с _text_vary'],
        body: [
            ['', 'vary'].map(function(value) {
                return {
                    block: 'select2',
                    mods: { theme: 'normal', size: 'm', type: 'check', text: value },
                    text: 'Сервис',
                    items: [
                        { val: 'disk', text: 'Яндекс.Диск' },
                        { val: 'maps', text: 'Яндекс.Карты' },
                        { val: 'pogoda', text: 'Яндекс.Погода' },
                        { val: 'translate', text: 'Яндекс.Переводчик' }
                    ]
                };
            })
        ]
    }
]
```

<a name="mods-item-icon-hidden"></a>

#### Модификатор `item-icon-hidden`

Определяет возможность скрыть иконки в пунктах раскрывающегося списка.

Допустимые значения: `'yes'`.

Способ установки: `BEMJSON`, `JS`.

> **Примечание.** Для списка с модификатором `type` в значении `check`, иконка на кнопке не определяется.

```js
[
    {
        block: 'x-table',
        head: ['С иконками', '_item-icon-hidden'],
        body: [
            ['', 'yes'].map(function(value) {
                return {
                    block: 'select2',
                    mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary', 'item-icon-hidden': value },
                    text: 'Сервис',
                    items: [
                        { val: 'disk', text: 'Яндекс.Диск', icon: { mods: { service: 'disk' } } },
                        { val: 'maps', text: 'Яндекс.Карты', icon: { mods: { service: 'maps' } } },
                        { val: 'pogoda', text: 'Яндекс.Погода', icon: { mods: { service: 'pogoda' } } },
                        { val: 'translate', text: 'Яндекс.Переводчик', icon: { mods: { service: 'translate' } } }
                    ]
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'menu', content: [
                { elem: 'text'},
                { elem: 'icon'}
            ]},
            { block: 'icon', mods: { service: 'disk' } },
            { block: 'icon', mods: { service: 'maps' } },
            { block: 'icon', mods: { service: 'pogoda' } },
            { block: 'icon', mods: { service: 'translate' } }
        ]
    }
]
```

<a name="mods-native"></a>

#### Модификатор `native`

Определяет возможность использовать нативный элемент управления для `touch`-устройств.

Допустимые значения: `'yes'`.

Способ установки: `BEMJSON`, `JS`.

> **Важно.** Необходимо использовать с модификатором `type` в значении `check`/`radio` и полем [control](#field-control).

```js
[
    {
        block: 'x-table',
        head: ['_native'],
        body: [
            {
                block: 'select2',
                mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary', native: 'yes' },
                text: 'Сервис',
                control: true,
                items: [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'select2', elem: 'control' }
        ]
    }
]
```

<a name="mods-tone"></a>

#### Модификатор `tone`

Задает тон блоку.

Допустимые значения: `'default'`, `'red'`, `'grey'`, `'dark'`, `'market'`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Необходимо использовать с модификатором `view` в значении `default`.

```js
[
    {
        block: 'x-table',
        head: ['default', 'red', 'grey', 'dark'],
        body: [
            ['default', 'red', 'grey', 'dark'].map(function(tone) {
                return {
                    block: 'select2',
                    mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary', tone: tone, view: 'default' },
                    text: 'Сервис',
                    items: [
                        { val: 'disk', text: 'Яндекс.Диск' },
                        { val: 'maps', text: 'Яндекс.Карты' },
                        { val: 'pogoda', text: 'Яндекс.Погода' },
                        { val: 'translate', text: 'Яндекс.Переводчик' }
                    ]
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'menu', content: [
                { elem: 'text'}
            ]},
            {
                block: 'select2',
                mods: { tone: ['red', 'grey', 'dark'] }
            }
        ]
    }
]
```

<a name="mods-view"></a>

#### Модификатор `view`

Определяет вид блока.

Допустимые значения: `'classic'` (используется по умолчанию), `'default'`.

Способ установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['classic', 'default'],
        body: [
            ['classic', 'default'].map(function(view) {
                return {
                    block: 'select2',
                    mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary', tone: 'default', view: view },
                    text: 'Сервис',
                    items: [
                        { val: 'disk', text: 'Яндекс.Диск' },
                        { val: 'maps', text: 'Яндекс.Карты' },
                        { val: 'pogoda', text: 'Яндекс.Погода' },
                        { val: 'translate', text: 'Яндекс.Переводчик' }
                    ]
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'menu', content: [
                { elem: 'text'}
            ]}
        ]
    }
]
```

<a name="mods-width"></a>

#### Модификатор `width`

Задает ширину блока.

Допустимые значения: `'fixed'`, `'max'`.

Способы установки: `BEMJSON`, `JS`.

<a name="width-fixed"></a>

**fixed**

Ширина блока фиксированная и зависит от ширины текста в пунктах раскрывающегося списка. Если ширина текста больше ширины контейнера (родительский HTML-элемент), текст обрезается троеточием.

```js
{
    block: 'x-area',
    mods: { bordered: 'yes', resizable: 'yes' },
    content: [
        {
            block: 'select2',
            mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary', width: 'fixed' },
            text: 'Сервис',
            items: [
                { val: 'disk', text: 'Яндекс.Диск' },
                { val: 'maps', text: 'Яндекс.Карты' },
                { val: 'pogoda', text: 'Яндекс.Погода' },
                { val: 'translate', text: 'Яндекс.Переводчик' }
            ]
        }
    ]
}
```

<a name="width-max"></a>

**max**

Ширина блока определяется шириной контейнера. Если ширина текста больше ширины контейнера, текст обрезается троеточием.

```js
{
    block: 'x-area',
    mods: { bordered: 'yes', resizable: 'yes' },
    content: [
        {
            block: 'select2',
            mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary', width: 'max' },
            text: 'Сервис',
            items: [
                { val: 'disk', text: 'Яндекс.Диск' },
                { val: 'maps', text: 'Яндекс.Карты' },
                { val: 'pogoda', text: 'Яндекс.Погода' },
                { val: 'translate', text: 'Яндекс.Переводчик' }
            ]
        }
    ]
}
```

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Отвечает за неактивное состояние, при котором блок виден, но недоступен для действий пользователя.

Нельзя:

* установить модификатор `focused` (существующий удаляется);
* вызвать БЭМ-события;
* открыть список.

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

> **Примечание.**
>
> Неактивное состояние можно:
>
> * выставлять как отдельным элементам списка, так и всему блоку;
> * изменять программно.

```js
[
    {
        block: 'x-table',
        head: ['_disabled на блоке', '_disabled на пункте списка'],
        body: [
            {
                block: 'select2',
                mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary', disabled: 'yes' },
                text: 'Сервис',
                items: [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ]
            },
            {
                block: 'select2',
                mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary' },
                text: 'Сервис',
                items: [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты', elemMods: { disabled: 'yes' } },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ]
            }
        ]
    }
]
```

<a name="mods-focused"></a>

#### Модификатор `focused`

Отвечает за установку фокуса.

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

Выставляется автоматически при получении блоком фокуса.

```js
[
    {
        block: 'x-table',
        head: ['_focused'],
        body: [
            {
                block: 'select2',
                mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary', focused: 'yes' },
                text: 'Сервис1',
                button: { mods: { focused: 'yes' } },
                items: [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ]
            }
        ]
    }
]
```

### Поля блока

<a name="field-text"></a>

#### Поле `text`

Определяет текст, который отображается на кнопке раскрывающегося списка.

Тип: `String`.

> **Примечание.** Если установлен модификатор [text](#mods-text), значение поля подменяется текстом выбранного пункта.

```js
{
    block: 'x-table',
    head: ['Поле text'],
    body: [
        {
            block: 'select2',
            mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary' },
            text: 'Сервис', // Переданное значение экранируется автоматически
            items: [
                { val: 'disk', text: 'Яндекс.Диск' },
                { val: 'maps', text: 'Яндекс.Карты' },
                { val: 'pogoda', text: 'Яндекс.Погода' },
                { val: 'translate', text: 'Яндекс.Переводчик' }
            ]
        }
    ]
}
```

<a name="field-items"></a>

#### Поле `items`

Определяет пункты списка или группы пунктов с опциональным названием.

Тип: `Array`.

```js
[
    {
        block: 'x-table',
        head: ['список', 'группы списков'],
        body: [
            [
                [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ],
                [
                    {
                        title: 'Группа 1',
                        items: [
                            { val: 'disk', text: 'Яндекс.Диск' },
                            { val: 'maps', text: 'Яндекс.Карты' },
                            { val: 'pogoda', text: 'Яндекс.Погода' },
                            { val: 'translate', text: 'Яндекс.Переводчик' }
                        ]
                    },
                    {
                        title: 'Группа 2',
                        items: [
                            { val: 'disk', text: 'Яндекс.Диск' },
                            { val: 'maps', text: 'Яндекс.Карты' },
                            { val: 'pogoda', text: 'Яндекс.Погода' },
                            { val: 'translate', text: 'Яндекс.Переводчик' }
                        ]
                    }
                ]
            ].map(function(items){
                return {
                    block: 'select2',
                    mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary' },
                    text: 'Сервис',
                    items: items
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'menu', content: [
                { elem: 'group' }
            ]}
        ]
    }
]
```

<a name="field-control"></a>

#### Поле `control`

Добавляет вспомогательный элемент `control`.

Тип: `Boolean`, `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Boolean', 'BEMJSON'],
        body: [
            [true, { elem: 'control' }].map(function(value) {
                return {
                    block: 'select2',
                    mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary' },
                    text: 'Сервис',
                    name: 'services',
                    control: value,
                    items: [
                        { val: 'disk', text: 'Яндекс.Диск' },
                        { val: 'maps', text: 'Яндекс.Карты' },
                        { val: 'pogoda', text: 'Яндекс.Погода' },
                        { val: 'translate', text: 'Яндекс.Переводчик' }
                    ]
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'select2', elem: 'control' }
        ]
    }
]
```

<a name="field-name"></a>

#### Поле `name`

Определяет уникальное имя блока.

Тип: `String`.

> **Важно!** Необходимо использовать с полем [control](#field-control).

```js
[
    {
        block: 'x-table',
        head: ['Поле name'],
        body: [
            {
                block: 'select2',
                mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary' },
                text: 'Сервис',
                name: 'services',
                control: true,
                items: [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'select2', elem: 'control' }
        ]
    }
]
```

<a name="field-val"></a>

#### Поле `val`

Определяет значение блока, которое будет отправлено на сервер.

Тип: `String`, `Number`, `Array` (для модификатора `type` в значении `check`).

```js
[
    {
        block: 'x-table',
        head: ['String', 'Number', 'Array'],
        body: [
            ['disk', 2, ['pogoda', 'translate']].map(function(value){
                return {
                    block: 'select2',
                    mods: { theme: 'normal', size: 'm', type: 'check', text: 'vary' },
                    text: 'Сервис',
                    val: value,
                    items: [
                        { val: 'disk', text: 'Яндекс.Диск' },
                        { val: 2, text: 'Яндекс.Карты' },
                        { val: 'pogoda', text: 'Яндекс.Погода' },
                        { val: 'translate', text: 'Яндекс.Переводчик' }
                    ]
                };
            })
        ]
    }
]
```

<a name="field-button"></a>

#### Поле `button`

Доопределяет кнопку раскрывающегося списка.

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле button'],
        body: [
            {
                block: 'select2',
                mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary' },
                text: 'Сервис',
                button: { id: 'service', tabindex: '1' },
                items: [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ]
            }
        ]
    }
]
```

<a name="field-menu"></a>

#### Поле `menu`

Доопределяет список пунктов (элемент `menu`).

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле menu'],
        body: [
            {
                block: 'select2',
                mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary' },
                text: 'Сервис',
                menu: { mods: { custom: 'mod' } },
                items: [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ]
            }
        ]
    }
]
```

<a name="field-required"></a>

#### Поле `required`

Определяет возможность валидации блока.

Тип: `Boolean`.

> **Важно!** Необходимо использовать с полем [control](#field-control).

```js
[
    {
        block: 'x-table',
        head: ['Поле required'],
        body: [
            {
                block: 'select2',
                mods: { theme: 'normal', size: 'm', type: 'radio', text: 'vary' },
                text: 'Сервис',
                required: true,
                control: true,
                items: [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'select2', elem: 'control' }
        ]
    }
]
```
