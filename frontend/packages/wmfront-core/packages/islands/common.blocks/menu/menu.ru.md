# menu

Используется для создания различных типов меню.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [theme](#mods-theme) (req) | `'normal'` | `BEMJSON`, `JS` | Стилевое оформление. |
| [size](#mods-size) (req) | `'xs'`, `'s'`, `'m'`, `'n'` | `BEMJSON`, `JS` | Размер меню. |
| [type](#mods-type) | `'check'`, `'radio'`, `'radiocheck'`, `'navigation'` | `BEMJSON` | Режим выбора пунктов меню. |
| [tone](#mods-tone) | `'default'`, `'red'`, `'grey'`, `'dark'` | `BEMJSON`, `JS` | Тон блока. Необходимо использовать с модификатором `view` в значении `default`. |
| [view](#mods-view) | `'classic'`, `'default'` | `BEMJSON`, `JS` | Вид меню. |
| [width](#mods-width) | `'auto'`, `'max'` | `BEMJSON`, `JS` | Ширина меню. |
| [disabled](#mods-disabled) | `'yes'` | `BEMJSON`, `JS` | Неактивное состояние. |
| [focused](#mods-focused) | `'yes'` | `BEMJSON`, `JS` | Фокус на блоке. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [items](#field-items) | `Array` | Массив пунктов меню. |
| [content](#field-content) | `BEMJSON` | Содержимое меню. Используется для формирования произвольной HTML-разметки, с помощью [элементов блока](#elems). Переопределяет значения заданные в полях: [items](#field-items), [val](#field-val). |
| [val](#field-val) | `String`, `Number`, `Array` | Выбранное значение из списка. Принимает массив, если блоку установлен модификатор `type` в значении `check`. |
| [tabindex](#field-tabindex) | `Number` | Последовательность перехода между контролами при нажатии на `Tab`. |

<a name="elems"></a>

### Элементы блока

| Элемент | Описание |
| ------- | -------- |
| [text](#elem-text) | Текст пункта меню. |
| [icon](#elem-icon) | Иконка пункта меню. Формируется блоком [icon](../icon/icon.ru.md). |
| [item](#elem-item) | Пункт меню. |
| [group](#elem-group) | Группа пунктов меню. |
| [title](#elem-title) | Заголовок группы пунктов. |

## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Отвечает за стилевое оформление блока. **Обязательный**.

Допустимое значение: `'normal'`.

Способ установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['Тема normal'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: {
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
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
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
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: {
                        block: 'menu',
                        mods: { theme: 'normal', size: size,  type: 'radio', width: 'max' },
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
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

<a name="mods-type"></a>

#### Модификатор `type`

Определяет режим выбора пунктов меню.

Допустимые значения: `'check'`, `'radio'`, `'radiocheck'`, `'navigation'`.

Способ установки: `BEMJSON`.

| Значение | Описание |
| -------- | -------- |
| `'check'` | Позволяет выбрать произвольное количество пунктов. |
| `'radio'` | Позволяет выбрать только один пункт меню. Если пункт не выбран, то по умолчанию выбирается первое значение из списка. |
| `'radiocheck'` | Позволяет выбрать только один пункт меню. Принципиальное отличие от значения `'radio'` в том, что в значении `'radiocheck'` есть возможность не выбирать ни одного пункта меню. |
| `'navigation'` | Меню из ссылок. |

```js
[
    {
        block: 'x-table',
        head: ['check', 'radio', 'radiocheck', 'navigation'],
        body: [
            ['check', 'radio', 'radiocheck', 'navigation'].map(function(type) {
                return {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: type, width: 'max' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk', url: type === 'navigation' ? 'https://disk.yandex.ru' : undefined },
                            { text: 'Яндекс.Карты', val: 'maps', url: type === 'navigation' ? 'https://yandex.ru/maps/' : undefined },
                            { text: 'Яндекс.Погода', val: 'pogoda', url: type === 'navigation' ? 'https://yandex.ru/pogoda/' : undefined },
                            { text: 'Яндекс.Переводчик', val: 'translate', url: type === 'navigation' ? 'https://translate.yandex.ru/' : undefined }
                        ]
                    }
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

<a name="mods-tone"></a>

#### Модификатор `tone`

Задает тон меню.

Допустимые значения: `'default'`, `'red'`, `'grey'`, `'dark'`.

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
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm',  type: 'radio', width: 'max', view: 'default', tone: tone },
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
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

<a name="mods-view"></a>

#### Модификатор `view`

Определяет вид меню.

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
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max', view: view, tone: 'default' },
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
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

<a name="mods-width"></a>

#### Модификатор `width`

Задает ширину блока.

Допустимые значения: `'auto'`, `'max'`.

Способы установки: `BEMJSON`, `JS`.

<a name="width-auto"></a>

**auto**

Ширина меню определяется шириной текста. Если ширина текста больше ширины контейнера (родительский HTML-элемент), текст обрезается троеточием.

```js
[
    {
        block: 'x-table',
        head: ['auto'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes', resizable: 'yes' },
                content: [
                    {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'auto' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk' },
                            { text: 'Яндекс.Карты', val: 'maps' },
                            { text: 'Яндекс.Погода', val: 'pogoda' },
                            { text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

<a name="width-max"></a>

**max**

Ширина блока определяется шириной контейнера. Если ширина текста больше ширины контейнера, текст обрезается троеточием.

```js
[
    {
        block: 'x-table',
        head: ['max'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes', resizable: 'yes' },
                content: [
                    {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk' },
                            { text: 'Яндекс.Карты', val: 'maps' },
                            { text: 'Яндекс.Погода', val: 'pogoda' },
                            { text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Отвечает за неактивное состояние, при котором блок виден, но недоступен для действий пользователя.

Нельзя:

* установить модификатор `focused` (существующий удаляется);
* вызвать БЭМ-события;
* выбрать пункт меню.

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

> **Примечание.**
>
> Неактивное состояние можно:
>
> * выставлять как отдельным пунктам меню, так и всему блоку;
> * изменять программно.

```js
[
    {
        block: 'x-table',
        head: ['_disabled на блоке', '_disabled на пункте списка'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: [
                    {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max', disabled: 'yes' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk' },
                            { text: 'Яндекс.Карты', val: 'maps' },
                            { text: 'Яндекс.Погода', val: 'pogoda' },
                            { text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                ]
            },
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: [
                    {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk' },
                            { text: 'Яндекс.Карты', val: 'maps', elemMods: { disabled: 'yes' } },
                            { text: 'Яндекс.Погода', val: 'pogoda' },
                            { text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
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
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: [
                    {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max', focused: 'yes' },
                        items: [
                            { text: 'Яндекс.Диск', val: 'disk' },
                            { text: 'Яндекс.Карты', val: 'maps' },
                            { text: 'Яндекс.Погода', val: 'pogoda' },
                            { text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

### Поля блока

<a name="field-items"></a>

#### Поле `items`

Определяет пункты меню или группы пунктов с опциональным названием.

Тип: `Array`.

```js
[
    {
        block: 'x-table',
        head: ['пункты', 'пункты c иконками', 'группы пунктов'],
        body: [
            [
                [
                    { val: 'disk', text: 'Яндекс.Диск' },
                    { val: 'maps', text: 'Яндекс.Карты' },
                    { val: 'pogoda', text: 'Яндекс.Погода' },
                    { val: 'translate', text: 'Яндекс.Переводчик' }
                ],
                [
                    { val: 'disk', text: 'Яндекс.Диск', icon: { mods: { service: 'disk' } } },
                    { val: 'maps', text: 'Яндекс.Карты', icon: { mods: { service: 'maps' } } },
                    { val: 'pogoda', text: 'Яндекс.Погода', icon: { mods: { service: 'pogoda' } } },
                    { val: 'translate', text: 'Яндекс.Переводчик', icon: { mods: { service: 'translate' } } }
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
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: [
                        {
                            block: 'menu',
                            mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                            items: items
                        }
                    ]
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', elem: 'icon' },
           { block: 'menu', mods: { view: 'default' } },
           { block: 'icon', mods: { service: 'disk' } },
           { block: 'icon', mods: { service: 'maps' } },
           { block: 'icon', mods: { service: 'pogoda' } },
           { block: 'icon', mods: { service: 'translate' } }
        ]
    }
]
```

<a name="field-content"></a>

#### Поле `content`

Определяет содержимое меню. Используется для формирования произвольной HTML-разметки.

Тип: `BEMJSON`.

> **Важно!** Переопределяет значения заданные в поле `items`.

```js
[
    {
        block: 'x-table',
        head: ['Поле content'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: [
                    {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                        content: [
                            { elem: 'item', elemMods: { type: 'option' }, text: 'Яндекс.Диск', val: 'disk' },
                            { elem: 'item', elemMods: { type: 'option', checked: 'yes' }, text: 'Яндекс.Карты', val: 'maps' },
                            { elem: 'item', elemMods: { type: 'option' }, text: 'Яндекс.Погода', val: 'pogoda' },
                            { elem: 'item', elemMods: { type: 'option' }, text: 'Яндекс.Переводчик', val: 'translate' }
                        ]
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
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
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: {
                        block: 'menu',
                        mods: { theme: 'normal', size: 'm', type: 'check', width: 'max' },
                        val: value,
                        items: [
                            { val: 'disk', text: 'Яндекс.Диск' },
                            { val: 2, text: 'Яндекс.Карты' },
                            { val: 'pogoda', text: 'Яндекс.Погода' },
                            { val: 'translate', text: 'Яндекс.Переводчик' }
                        ]
                    }
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

<a name="field-tabindex"></a>

#### Поле `tabindex`

Определяет порядок получения фокуса при переходе между контролами с помощью клавиши `Tab`.

Тип: `Number`.

```js
[
    {
        block: 'x-table',
        head: ['Поле tabindex'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: {
                    block: 'menu',
                    mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                    tabindex: 2,
                    items: [
                        { val: 'disk', text: 'Яндекс.Диск' },
                        { val: 'maps', text: 'Яндекс.Карты' },
                        { val: 'pogoda', text: 'Яндекс.Погода' },
                        { val: 'translate', text: 'Яндекс.Переводчик' }
                    ]
                }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

### Элементы блока

<a name="elem-text"></a>

#### Элемент `text`

Определяет текст пункта меню.

> **Примечание.** Переданное значение необходимо экранировать самостоятельно `content: xmlEscape('Яндекс.Диск')`.

```js
[
    {
        block: 'x-table',
        head: ['__text'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: {
                    block: 'menu',
                    mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                    content: [
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'disk',
                            content: { elem: 'text', content: 'Яндекс.Диск' }
                        },
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'maps',
                            content: { elem: 'text', content: 'Яндекс.Карты' }
                        },
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'pogoda',
                            content: { elem: 'text', content: 'Яндекс.Погода' }
                        },
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'translate',
                            content: { elem: 'text', content: 'Яндекс.Переводчик' }
                        }
                    ]
                }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

<a name="elem-icon"></a>

#### Элемент `icon`

Определяет иконку пункта меню. Элемент `icon` миксуется к блоку [icon](../icon/icon.ru.md).

> **Примечание.** Используется для самостоятельной настройки параметров кнопки.

```js
[
    {
        block: 'x-table',
        head: ['__icon'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: {
                    block: 'menu',
                    mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                    content: [
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'disk',
                            content: [
                                {
                                    block: 'icon',
                                    mods: { size: 'm', service: 'disk' },
                                    mix: { block: 'menu', elem: 'icon' }
                                },
                                {
                                    elem: 'text',
                                    content: 'Яндекс.Диск'
                                }
                            ]
                        },
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'maps',
                            content: [
                                {
                                    block: 'icon',
                                    mods: { size: 'm', service: 'maps' },
                                    mix: { block: 'menu', elem: 'icon' }
                                },
                                {
                                    elem: 'text',
                                    content: 'Яндекс.Карты'
                                }
                            ]
                        },
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'pogoda',
                            content: [
                                {
                                    block: 'icon',
                                    mods: { size: 'm', service: 'pogoda' },
                                    mix: { block: 'menu', elem: 'icon' }
                                },
                                {
                                    elem: 'text',
                                    content: 'Яндекс.Погода'
                                }
                            ]
                        },
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'translate',
                            content: [
                                {
                                    block: 'icon',
                                    mods: { size: 'm', service: 'translate' },
                                    mix: { block: 'menu', elem: 'icon' }
                                },
                                {   
                                    elem: 'text',
                                    content: 'Яндекс.Переводчик'
                                }
                            ]
                        }
                    ]
                }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'menu', elem: 'item' },
            { block: 'menu', elem: 'icon' },
            { block: 'menu', mods: { view: 'default' } },
            { block: 'icon', mods: { service: 'disk' } },
            { block: 'icon', mods: { service: 'maps' } },
            { block: 'icon', mods: { service: 'pogoda' } },
            { block: 'icon', mods: { service: 'translate' } }
        ]
    }
]
```

<a name="elem-item"></a>

#### Элемент `item`

Определяет пункт меню.

**Модификаторы элемента**

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| `type` | `'link'`, `'option'` | `BEMJSON` | Тип пунктов меню. Тип `'link'` используется для меню c [модификатором type в значении navigation](#mods-type). |
| `checked` | `'yes'` | `BEMJSON`, `JS` | Пункт выбран. Не используется для меню из ссылок. |
| `disabled` | `'yes'` | `BEMJSON`, `JS` | Неактивное состояние. |
| `hovered` | `'yes'` | — | Наведение на пункт курсором. |

**Поля элемента**

| Поле | Тип | Описание |
| ---- | --- | -------- |
| `text` | `String` | Текст пункта меню. Переданное значение автоматически экранируется. |
| `val`  | `String`, `Number` | Значение пункта меню. |
| `icon` | `BEMJSON` | Иконка пункта меню. Формируется блоком [icon](../icon/icon.ru.md). |
| `url`  | `String` | Адрес. Используется только для меню с [модификатором type в значении navigation](#mods-type). |
| `target` | `String` | Поведение пункта-ссылки. |

> **Примечание.** Используется для самостоятельной настройки параметров кнопки.

```js
[
    {
        block: 'x-table',
        head: ['__item'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: {
                    block: 'menu',
                    mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                    content: [
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'disk',
                            content: { elem: 'text',  content: 'Яндекс.Диск' }
                        },
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'maps',
                            content: { elem: 'text', content: 'Яндекс.Карты' }
                        },
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'pogoda',
                            content: { elem: 'text', content: 'Яндекс.Погода' }
                        },
                        {
                            elem: 'item',
                            elemMods: { type: 'option' },
                            val: 'translate',
                            content: { elem: 'text', content: 'Яндекс.Переводчик' }
                        }
                    ]
                }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

<a name="elem-group"></a>

#### Элемент `group`

Определяет группу пунктов меню.

Позволяет задать группе пунктов произвольный заголовок с помощью поля `title`. Формируется элементом [title](#elem-title).

**Поля элемента**

| Поле | Тип | Описание |
| ---- | --- | -------- |
| `title` | String | Заголовок группы пунктов. Переданное значение автоматически экранируется.|

> **Примечание.** Используется для самостоятельной настройки параметров кнопки.

```js
[
    {
        block: 'x-table',
        head: ['__group'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: {
                    block: 'menu',
                    mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                    content: [
                        {
                            elem: 'group',
                            title: 'Группа 1',
                            content: [
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'disk',
                                    content: { elem: 'text', content: 'Яндекс.Диск' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'maps',
                                    content: { elem: 'text', content: 'Яндекс.Карты' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'pogoda',
                                    content: { elem: 'text', content: 'Яндекс.Погода' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'translate',
                                    content: { elem: 'text', content: 'Яндекс.Переводчик' }
                                }

                            ]
                        },
                        {
                            elem: 'group',
                            title: 'Группа 2',
                            content: [
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'disk',
                                    content: { elem: 'text', content: 'Яндекс.Диск' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'maps',
                                    content: { elem: 'text', content: 'Яндекс.Карты' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'pogoda',
                                    content: { elem: 'text', content: 'Яндекс.Погода' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'translate',
                                    content: { elem: 'text', content: 'Яндекс.Переводчик' }
                                }
                            ]
                        }
                    ]
                }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```

<a name="elem-title"></a>

#### Элемент `title`

Определяет заголовок группы пунктов меню.

> **Примечание.** Используется для самостоятельной настройки параметров кнопки.

```js
[
    {
        block: 'x-table',
        head: ['__title'],
        body: [
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: {
                    block: 'menu',
                    mods: { theme: 'normal', size: 'm', type: 'radio', width: 'max' },
                    content: [
                        {
                            elem: 'group',
                            content: [
                                {
                                    elem: 'title',
                                    content: 'Группа 1'
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'disk',
                                    content: { elem: 'text', content: 'Яндекс.Диск' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'maps',
                                    content: { elem: 'text', content: 'Яндекс.Карты' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'pogoda',
                                    content: { elem: 'text', content: 'Яндекс.Погода' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'translate',
                                    content: { elem: 'text', content: 'Яндекс.Переводчик' }
                                }

                            ]
                        },
                        {
                            elem: 'group',
                            content: [
                                {
                                    elem: 'title',
                                    content: 'Группа 2'
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'disk',
                                    content: { elem: 'text', content: 'Яндекс.Диск' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'maps',
                                    content: { elem: 'text', content: 'Яндекс.Карты' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'pogoda',
                                    content: { elem: 'text', content: 'Яндекс.Погода' }
                                },
                                {
                                    elem: 'item',
                                    elemMods: { type: 'option' },
                                    val: 'translate',
                                    content: { elem: 'text', content: 'Яндекс.Переводчик' }
                                }
                            ]
                        }
                    ]
                }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
           { block: 'menu', elem: 'item' },
           { block: 'menu', mods: { view: 'default' } }
        ]
    }
]
```
