# header2

Используется для создания шапки страницы.

## Внимание! Блок устарел! Пожалуйста, используйте [serp-header](https://lego.yandex-team.ru/serp-header/).

## Обзор

### Раскладка

![header2](https://jing.yandex-team.ru/files/godfreyd/header2.svg)

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [border](#mods-border) | `'white'`, `'transparent'` | `BEMJSON` | Стилевое оформление нижней границы шапки. |
| [fixed](#mods-fixed) | `'yes'` | `BEMJSON` | Фиксированное позиционирование. Используется совместно с модификатором [border в значении transparent](#border-transparent). |
| [panels](#mods-panels) | `'yes'` | `BEMJSON` | API управления виртуальными панелями. |
| [progress](#mods-progress) | `'yes'` | `BEMJSON` | Полоса прогресса загрузки в верхней части шапки. Формируется блоком [progress](../progress/progress.ru.md). |
| [tableau](#mods-tableau) | `'yes'` | `JS` | Табло сервисов. Формируется блоком [tableau-node](../tableau-node/tableau-node.ru.md). |

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [left](#field-left) (req) | `BEMJSON` | Контейнер для элементов управления, выровненный по левому краю. |
| [logo](#field-logo) | `BEMJSON` | Контейнер для логотипа. |
| [right](#field-right) | `BEMJSON` | Контейнер для элементов управления, выровненный по правому краю. |
| [under](#field-under) | `BEMJSON` | Контейнер для скрытых элементов управления с абсолютным позиционированием, выровненный по нижней границе шапки. |

req — обязательное поле.

<a name="elems"></a>

### Элементы блока

| Элемент | Описание |
| ------- | -------- |
| [gap](#elem-gap) | Вспомогательный отступ слева. |
| [left](#elem-left) | Контейнер для элементов управления, выровненный по левому краю. |
| [logo](#elem-logo) | Контейнер для логотипа. |
| [main](#elem-main) | Основной контейнер. |
| [nameplate](#elem-nameplate) | Метка с названием сервиса (шильдик). Формируется блоком [nameplate](../nameplate/nameplate.ru.md). |
| [paranja](#elem-paranja) | Паранджа. Формируется блоком [paranja](../paranja/paranja.ru.md). |
| [progress](#elem-progress) | Полоса прогресса загрузки в верхней части шапки. |
| [right](#elem-right) | Контейнер для элементов управления, выровненный по правому краю. |
| [under](#elem-under) | Контейнер для скрытых элементов управления с абсолютным позиционированием, выровненный по нижней границе шапки. |

dep — устаревший элемент.

## Подробное описание

### Модификаторы блока

<a name="mods-border"></a>

#### Модификатор `border`

Отвечает за стилевое оформление нижней границы шапки.

> **Примечание.** По умолчанию шапка без модификатора `border` имеет полупрозрачную нижнюю границу шириной в `1px`.

Допустимое значение: `'white'`, `'transparent'`.

Способ установки: `BEMJSON`.

<a name="border-white"></a>

**Шапка без нижней границы (модификатор `border` в значении `white`)**

Убирает нижнюю границу.

```js
[
    {
        block: 'header2',
        mods: { border: 'white' },
        logo: {
            elem: 'logo',
            elemMods: { size: 'm' },
            content: {
                block: 'logo',
                mods: {
                    name: 'ru-84x36',
                    type: 'link'
                }
            }
        },
        left: { block: 'search2', mods: { template: 'websearch' } }
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'logo', mods: { type: 'link', name: ['ru-84x36'] } }
        ]
    }
]
```

<a name="border-transparent"></a>

**Шапка с белой полосой (модификатор `border` в значении `transparent`)**

Отменяет фиксированную высоту шапки `70px` и добавляет под шапкой белую полосу (элемент white-stripe) высотой в `4px`.

```js
[
    {
        block: 'header2',
        mods: { fixed: 'yes', border: 'transparent' },
        logo: {
            elem: 'logo',
            elemMods: { size: 'm' },
            content: {
                block: 'logo',
                mods: {
                    name: 'ru-84x36',
                    type: 'link'
                }
            }
        },
        left: { block: 'search2', mods: { template: 'websearch' }}
    },
    {
        block: 'x-serp',
        content: [
            {
                block: 'tabs-menu',
                attrs: { style: 'margin: 48px 0 0 128px;' },
                mods: {
                    theme: 'search-head',
                    more: 'yes'
                },
                js: true,
                content: [
                    ['Пвввоиск', 'https://yandex.ru'],
                    ['Картинки', 'https://yandex.ru/images'],
                    ['Видео', 'https://yandex.ru/video'],
                    ['Карты', 'https://maps.yandex.ru'],
                    ['Маркет', 'https://market.yandex.ru']
                ].map(function(entry, idx) {
                    return {
                        elem: 'tab',
                        elemMods: idx === 0 ? { active: 'yes' } : {},
                        content: {
                            block: 'link',
                            mods: { theme: false },
                            tabindex: idx === 0 ? -1 : undefined,
                            url: entry[1],
                            text: entry[0]
                        }
                    };
                })
            }
        ]
    },
    {
        block: 'x-deps',
        content: { block: 'i-services', elem: 'uri' }
    }
]
```

<a name="mods-fixed"></a>

#### Модификатор `fixed`

Отвечает за фиксированное позиционирование шапки.

Допустимое значение: `'yes'`.

Способ установки: `BEMJSON`.

Используется совместно с модификатором [border в значении transparent](#border-transparent).

```js
{
    attrs: { style: 'height: 250px; overflow-y: scroll;' },
    content:
    [
        {
            block: 'header2',
            mods: { fixed: 'yes', border: 'transparent' },
            logo: {
                elem: 'logo',
                elemMods: { size: 'm' },
                content: {
                    block: 'logo',
                    mods: {
                        name: 'ru-84x36',
                        type: 'link'
                    }
                }
            },
            left: { block: 'search2', mods: { template: 'websearch' } }
        },
        {
            block: 'x-serp',
            attrs: { style: 'margin: 67px 20px 20px 131px;' },
            content: [
                {
                    block: 'x-lorem',
                    paragraphs: 10
                }
            ]
        },
        {
            block: 'x-deps',
            content: [
                { block: 'i-services', elem: 'uri' },
                { block: 'logo', mods: { type: 'link', name: ['ru-84x36'] } }
            ]
        }
    ]
}
```

<a name="mods-panels"></a>

#### Модификатор `panels`

Определяет API управления виртуальными панелями.

Методы API позволяют:

* определить какая панель открыта;
* открыть/закрыть панель.

В открытом состоянии может находиться только одна панель. При переключении панелей на шапке генерируется событие `panel-switch`.

Допустимое значение: `'yes'`.

Способ установки: `BEMJSON`.

```js
[
    {
        block: 'i-global',
        params: {
            login: 'lego-team',
            uid: '4001140776'
        }
    },
    {
        block: 'header2',
        mods: { panels: 'yes' },
        mix: { block: 'example', js: true, mods: { panels: 'yes' } },
        logo: {
            elem: 'logo',
            elemMods: { size: 'm' },
            content: {
                block: 'logo',
                mods: {
                    name: 'ru-84x36',
                    type: 'link'
                }
            }
        },
        left: { block: 'search2', mods: { template: 'websearch' } },
        right: [
            {
                block: 'button2',
                mods: {
                    type: 'check',
                    theme: 'clear',
                    size: 'm'
                },
                icon: { mods: { action: 'settings' } },
                mix: {
                    block: 'header2',
                    elem: 'action',
                    elemMods: { type: 'settings' }
                },
                js: { panel: 'settings' }
            },
            {
                block: 'button2',
                mods: {
                    type: 'check',
                    theme: 'clear',
                    size: 'm'
                },
                icon: { mods: { action: 'filter' } },
                mix: {
                    block: 'header2',
                    elem: 'action',
                    elemMods: { type: 'filter' }
                },
                js: { panel: 'filter' }
            },
            {
                block: 'button2',
                mods: {
                    type: 'check',
                    theme: 'clear',
                    size: 'm'
                },
                icon: { mods: { action: 'tableau' } },
                mix: [{
                    block: 'header2',
                    elem: 'action',
                    elemMods: { type: 'tableau' }
                }, {
                    block: 'tableau-node',
                    elem: 'trigger'
                }],
                js: { panel: 'tableau' }
            },
            {
                block: 'user2',
                name: 'lego-team',
                avatarId: '0/0-0',
                uid: '123',
            }
        ],
        under:  [
            {
                block: 'tooltip',
                mods: {
                    size: 'm',
                    theme: 'normal',
                    tone: 'default',
                    autoclosable: 'yes'
                },
                js: { to: 'bottom' }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'right' },
            { block: 'header2', elem: 'under' },
            { block: 'logo', mods: { type: 'link', name: ['ru-84x36'] } }

        ]
    }
]
```

<a name="mods-progress"></a>

#### Модификатор `progress`

Определяет полосу загрузки в верхней части шапки.

Для определения полосы в нижней части шапки используйте элемент [progress](#elem-progress).

Допустимое значение: `'yes'`.

Способ установки: `BEMJSON`.

Формируется блоком [progress](../progress/progress.ru.md).

```js
[
    {
        block: 'x-title',
        text: 'Нажмите кнопку «Найти»'
    },
    {
        block: 'x-table',
        head: ['Модификатор progress', 'Элемент progress'],
        body: [
            {
                block: 'header2',
                mods: { progress: 'yes' },
                mix: { block: 'example', js: true, mods: { progress: 'yes' } },
                logo: {
                    elem: 'logo',
                    elemMods: { size: 'm' },
                    content: {
                        block: 'logo',
                        mods: {
                            name: 'ru-84x36',
                            type: 'link'
                        }
                    }
                },
                left: { block: 'search2', mods: { template: 'websearch' } }
            },
            {
                block: 'header2',
                mix: { block: 'example', js: true, mods: { progress: 'yes' } },
                logo: {
                    elem: 'logo',
                    elemMods: { size: 'm' },
                    content: {
                        block: 'logo',
                        mods: {
                            name: 'ru-84x36',
                            type: 'link'
                        }
                    }
                },
                left: { block: 'search2', mods: { template: 'websearch' } },
                under: { elem: 'progress' }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'under' }
        ]
    }
]
```

<a name="mods-tableau"></a>

#### Модификатор `tableau`

Определяет табло сервисов.

Табло открывается на:

* `desktop` — при наведении на логотип;
* `touch` — при нажатии на кнопку показа табло.

Допустимое значение: `'yes'`.

Способ установки: `JS`.

Формируется блоком [tableau-node](../tableau-node/tableau-node.ru.md).

### Поля блока

<a name="field-left"></a>

#### Поле `left`

Определяет контейнер для элементов управления, выровненный по левому краю. **Обязательное**.

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле left'],
        body: [
            {
                block: 'header2',
                logo: {
                    elem: 'logo',
                    elemMods: { size: 'm' },
                    content: {
                        block: 'logo',
                        mods: {
                            name: 'ru-84x36',
                            type: 'link'
                        }
                    }
                },
                left: { block: 'search2', mods: { template: 'websearch' } }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'logo', mods: { type: 'link', name: ['ru-84x36'] } }
        ]
    }
]
```

<a name="field-logo"></a>

#### Поле `logo`

Определяет контейнер для логотипа.

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле logo'],
        body: [
            {
                block: 'header2',
                logo: { elem: 'logo', elemMods: { size: 'm' } }
            }
        ]
    },
    {
        block: 'x-deps',
        content: { block: 'i-services', elem: 'uri' }
    }
]
```

<a name="field-right"></a>

#### Поле `right`

Определяет контейнер для элементов управления, выровненный по правому краю.

Тип: `BEMJSON`.

```js
[
    {
        block: 'i-global',
        params: {
            login: 'lego-team',
            uid: '4001140776'
        }
    },
    {
        block: 'x-table',
        head: ['Поле right'],
        body: [
            {
                block: 'header2',
                mods: { panels: 'yes' },
                mix: { block: 'example', js: true, mods: { panels: 'yes' } },
                right: [
                    {
                        block: 'button2',
                        mods: {
                            type: 'check',
                            theme: 'clear',
                            size: 'm'
                        },
                        icon: { mods: { action: 'settings' } },
                        mix: {
                            block: 'header2',
                            elem: 'action',
                            elemMods: { type: 'settings' }
                        },
                        js: { panel: 'settings' }
                    },
                    {
                        block: 'button2',
                        mods: {
                            type: 'check',
                            theme: 'clear',
                            size: 'm'
                        },
                        icon: { mods: { action: 'filter' } },
                        mix: {
                            block: 'header2',
                            elem: 'action',
                            elemMods: { type: 'filter' }
                        },
                        js: { panel: 'filter' }
                    },
                    {
                        block: 'button2',
                        mods: {
                            type: 'check',
                            theme: 'clear',
                            size: 'm'
                        },
                        icon: { mods: { action: 'tableau' } },
                        mix: [{
                            block: 'header2',
                            elem: 'action',
                            elemMods: { type: 'tableau' }
                        }, {
                            block: 'tableau-node',
                            elem: 'trigger'
                        }],
                        js: { panel: 'tableau' }
                    },
                    {
                        block: 'user2',
                        name: 'lego-team',
                        avatarId: '0/0-0',
                        uid: '123',
                    }
                ],
                under:  [
                    {
                        block: 'tooltip',
                        mods: {
                            size: 'm',
                            theme: 'normal',
                            tone: 'default',
                            autoclosable: 'yes'
                        },
                        js: { to: 'bottom' }
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'right' },
            { block: 'header2', elem: 'under' }

        ]
    }
]
```

<a name="field-under"></a>

#### Поле `under`

Определяет контейнер для скрытых элементов управления с абсолютным позиционированием, выровненный по нижней границе шапки.

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле under (Нажмите кнопку «Найти»)'],
        body: [
            {
                block: 'header2',
                mix: { block: 'example', js: true, mods: { progress: 'yes' } },
                logo: {
                    elem: 'logo',
                    elemMods: { size: 'm' },
                    content: {
                        block: 'logo',
                        mods: {
                            name: 'ru-84x36',
                            type: 'link'
                        }
                    }
                },
                left: { block: 'search2', mods: { template: 'websearch' } },
                under: { elem: 'progress' }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'under' },
            { block: 'logo', mods: { type: 'link', name: ['ru-84x36'] } }
        ]
    }
]
```

### Элементы блока

<a name="elem-gap"></a>

#### Элемент `gap`

Определяет левый отступ шириной `12px`.

Вспомогательный элемент, позволяющий увеличить стандартные отступы между контролами. Подмешивается к элементам управления.

```js
[
    {
        block: 'i-global',
        params: {
            login: 'lego-team',
            uid: '4001140776'
        }
    },
    {
        block: 'x-table',
        head: ['__gap (Увеличенные отступы между панелями)'],
        body: [
            {
                block: 'header2',
                mods: { panels: 'yes' },
                mix: { block: 'example', js: true, mods: { panels: 'yes' } },
                logo: {
                    elem: 'logo',
                    elemMods: { size: 'm' },
                    content: {
                        block: 'logo',
                        mods: {
                            name: 'ru-84x36',
                            type: 'link'
                        }
                    }
                },
                left: [
                    {
                        block: 'search2',
                        mods: { template: 'websearch' }
                    },
                    {
                        block: 'tooltip',
                        mods: {
                            size: 'm',
                            theme: 'normal',
                            tone: 'default',
                            autoclosable: 'yes'
                        },
                        js: { to: 'bottom' }
                    }
                ],
                right: [
                    {
                        block: 'button2',
                        mods: {
                            type: 'check',
                            theme: 'clear',
                            size: 'm'
                        },
                        icon: { mods: { action: 'settings' } },
                        mix: {
                            block: 'header2',
                            elem: 'action',
                            elemMods: { type: 'settings' }
                        },
                        js: { panel: 'settings' }
                    },
                    {
                        block: 'button2',
                        mods: {
                            type: 'check',
                            theme: 'clear',
                            size: 'm'
                        },
                        icon: { mods: { action: 'filter' } },
                        mix: {
                            block: 'header2',
                            elem: 'action',
                            elemMods: { type: 'filter' }
                        },
                        js: { panel: 'filter' }
                    },
                    {
                        block: 'button2',
                        mods: {
                            type: 'check',
                            theme: 'clear',
                            size: 'm'
                        },
                        icon: { mods: { action: 'tableau' } },
                        mix: [{
                            block: 'header2',
                            elem: 'action',
                            elemMods: { type: 'tableau' }
                        }, {
                            block: 'tableau-node',
                            elem: 'trigger'
                        }],
                        js: { panel: 'tableau' }
                    },
                    {
                        block: 'user2',
                        name: 'lego-team',
                        avatarId: '0/0-0',
                        uid: '123',
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'right' },
            { block: 'logo', mods: { type: 'link', name: ['ru-84x36'] } }
        ]
    }
]
```

> **Примечание.** Используется для самостоятельной настройки параметров шапки.

<a name="elem-left"></a>

#### Элемент `left`

Определяет контейнер для элементов управления, выровненный по левому краю.

```js
[
    {
        block: 'x-table',
        head: ['__left'],
        body: [
            {
                block: 'header2',
                content: [
                    {
                        elem: 'main',
                        content: [
                            {
                                elem: 'logo',
                                elemMods: { size: 'm' },
                                content: '__logo'
                            },
                            {
                                elem: 'left',
                                attrs: { style: 'background: #C9DCF6;' },
                                content: '__left'
                            },
                            {
                                elem: 'right',
                                content: '__right'
                            }
                        ]
                    },
                    {
                        elem: 'under',
                        content: '__under'
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'right' },
            { block: 'header2', elem: 'under' }
        ]
    }
]
```

> **Примечание.** Используется для самостоятельной настройки параметров шапки.

<a name="elem-logo"></a>

#### Элемент `logo`

Определяет контейнер для логотипа.

```js
[
    {
        block: 'x-table',
        head: ['__logo'],
        body: [
            {
                block: 'header2',
                content: [
                    {
                        elem: 'main',
                        content: [
                            {
                                elem: 'logo',
                                attrs: { style: 'background: #C9DCF6;' },
                                elemMods: { size: 'm' },
                                content: '__logo'
                            },
                            {
                                elem: 'left',
                                content: '__left'
                            },
                            {
                                elem: 'right',
                                content: '__right'
                            }
                        ]
                    },
                    {
                        elem: 'under',
                        content: '__under'
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'right' },
            { block: 'header2', elem: 'under' }
        ]
    }
]
```

> **Примечание.** Используется для самостоятельной настройки параметров шапки.

<a name="elem-main"></a>

#### Элемент `main`

Определяет основной контейнер для шапки.

```js
[
    {
        block: 'x-table',
        head: ['__main'],
        body: [
            {
                block: 'header2',
                content: [
                    {
                        elem: 'main',
                        attrs: { style: 'background: #C9DCF6;' },
                        content: [
                            {
                                elem: 'logo',
                                elemMods: { size: 'm' },
                                content: '__logo'
                            },
                            {
                                elem: 'left',
                                content: '__left'
                            },
                            {
                                elem: 'right',
                                content: '__right'
                            }
                        ]
                    },
                    {
                        elem: 'under',
                        content: '__under'
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'right' },
            { block: 'header2', elem: 'under' }
        ]
    }
]
```

> **Примечание.** Используется для самостоятельной настройки параметров шапки.

<a name="elem-nameplate"></a>

#### Элемент `nameplate`

Определяет метку с названием сервиса (шильдик).

**Поля элемента**

| Поле    | Тип      | Описание                                    |
| ------- | -------- | ------------------------------------------- |
| name    | `String` | Название сервиса, отображаемое на шильдике. |
| url     | `String` | URL главной страницы сервиса.               |
| service | `String` | Ключ сервиса.                               |

> **Примечание.** Следует указывать либо оба поля `name` и `url`, либо только поле `service`. Во втором случае название и адрес сервиса будут получены по ключу из блока [i-services](../i-services/i-services.ru.md).

Формируется блоком [nameplate](../nameplate/nameplate.ru.md).

```js
[
    {
        block: 'x-table',
        head: ['__nameplate (name и url)', '__nameplate (service)'],
        body: [
            {
                block: 'header2',
                content: [
                    {
                        elem: 'main',
                        content: [
                            {
                                elem: 'logo',
                                elemMods: { size: 'm' },
                                content: '__logo'
                            },
                            {
                                elem: 'left',
                                content: [
                                    {
                                        elem: 'nameplate',
                                        name: 'Market',
                                        url: 'https://market.yandex.com'
                                    }
                                ]
                            },
                            {
                                elem: 'right',
                                content: '__right'
                            }
                        ]
                    },
                    {
                        elem: 'under',
                        content: '__under'
                    }
                ]
            },
            {
                block: 'header2',
                content: [
                    {
                        elem: 'main',
                        content: [
                            {
                                elem: 'logo',
                                elemMods: { size: 'm' },
                                content: '__logo'
                            },
                            {
                                elem: 'left',
                                content: [
                                    {
                                        elem: 'nameplate',
                                        service: 'market'
                                    }
                                ]
                            },
                            {
                                elem: 'right',
                                content: '__right'
                            }
                        ]
                    },
                    {
                        elem: 'under',
                        content: '__under'
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'right' },
            { block: 'header2', elem: 'under' }
        ]
    }
]
```

<a name="elem-paranja"></a>

#### Элемент `paranja`

Определяет паранджу, которая появляется при раскрытии виртуальной панели.

Формируется блоком [paranja](../paranja/paranja.ru.md).

```js
[
    {
        block: 'i-global',
        params: {
            login: 'lego-team',
            uid: '4001140776'
        }
    },
    {
        block: 'x-table',
        head: ['__paranja (Нажмите на любую панель)'],
        body: [
            {
                block: 'header2',
                mods: { panels: 'yes' },
                mix: { block: 'example', js: true, mods: { paranja: 'yes' } },
                content: [
                    {
                        elem: 'main',
                        content: [
                            {
                                elem: 'logo',
                                elemMods: { size: 'm' },
                                content: '__logo'
                            },
                            {
                                elem: 'left',
                                content: '__left'
                            },
                            {
                                elem: 'right',
                                content: [
                                    {
                                        block: 'button2',
                                        mods: {
                                            type: 'check',
                                            theme: 'clear',
                                            size: 'm'
                                        },
                                        icon: { mods: { action: 'settings' } },
                                        mix: {
                                            block: 'header2',
                                            elem: 'action',
                                            elemMods: { type: 'settings' }
                                        },
                                        js: { panel: 'settings' }
                                    },
                                    {
                                        block: 'button2',
                                        mods: {
                                            type: 'check',
                                            theme: 'clear',
                                            size: 'm'
                                        },
                                        icon: { mods: { action: 'filter' } },
                                        mix: {
                                            block: 'header2',
                                            elem: 'action',
                                            elemMods: { type: 'filter' }
                                        },
                                        js: { panel: 'filter' }
                                    },
                                    {
                                        block: 'button2',
                                        mods: {
                                            type: 'check',
                                            theme: 'clear',
                                            size: 'm'
                                        },
                                        icon: { mods: { action: 'tableau' } },
                                        mix: [{
                                            block: 'header2',
                                            elem: 'action',
                                            elemMods: { type: 'tableau' }
                                        }, {
                                            block: 'tableau-node',
                                            elem: 'trigger'
                                        }],
                                        js: { panel: 'tableau' }
                                    },
                                    {
                                        block: 'user2',
                                        name: 'lego-team',
                                        avatarId: '0/0-0',
                                        uid: '123',
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        elem: 'under',
                        content: {
                            elem: 'paranja',
                            content: '__paranja'
                        }
                    }
                ]
            },

        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'right' },
            { block: 'header2', elem: 'under' }
        ]
    }
]
```

<a name="elem-progress"></a>

#### Элемент `progress`

Определяет полосу загрузки в нижней части шапки.

Формируется блоком [progress](../progress/progress.ru.md).

```js
[
    {
        block: 'x-table',
        head: ['__progress (Нажмите кнопку «Найти»)'],
        body: [
            {
                block: 'header2',
                mix: { block: 'example', js: true, mods: { progress: 'yes' } },
                logo: {
                    elem: 'logo',
                    elemMods: { size: 'm' },
                    content: {
                        block: 'logo',
                        mods: {
                            name: 'ru-84x36',
                            type: 'link'
                        }
                    }
                },
                left: { block: 'search2', mods: { template: 'websearch' } },
                under: { elem: 'progress' }
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'under' }
        ]
    }
]
```

<a name="elem-right"></a>

#### Элемент `right`

Определяет контейнер для элементов управления, выровненный по правому краю.

```js
[
    {
        block: 'x-table',
        head: ['__right'],
        body: [
            {
                block: 'header2',
                content: [
                    {
                        elem: 'main',
                        content: [
                            {
                                elem: 'logo',
                                elemMods: { size: 'm' },
                                content: '__logo'
                            },
                            {
                                elem: 'left',
                                content: '__left'
                            },
                            {
                                elem: 'right',
                                attrs: { style: 'background: #C9DCF6;' },
                                content: '__right'
                            }
                        ]
                    },
                    {
                        elem: 'under',
                        content: '__under'
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'right' },
            { block: 'header2', elem: 'under' }
        ]
    }
]
```

> **Примечание.** Используется для самостоятельной настройки параметров шапки.

<a name="elem-under"></a>

#### Элемент `under`

Определяет контейнер для скрытых элементов управления с абсолютным позиционированием ([__paranja](#elem-paranja), [__progress](#elem-progress)), выровненный по нижней границе шапки.

```js
[
    {
        block: 'x-table',
        head: ['__under'],
        body: [
            {
                block: 'header2',
                content: [
                    {
                        elem: 'main',
                        content: [
                            {
                                elem: 'logo',
                                elemMods: { size: 'm' },
                                content: '__logo'
                            },
                            {
                                elem: 'left',
                                content: '__left'
                            },
                            {
                                elem: 'right',
                                content: '__right'
                            }
                        ]
                    },
                    {
                        elem: 'under',
                        attrs: { style: 'background: #C9DCF6;' },
                        content: '__under'
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'i-services', elem: 'uri' },
            { block: 'header2', elem: 'right' },
            { block: 'header2', elem: 'under' }
        ]
    }
]
```

> **Примечание.** Используется для самостоятельной настройки параметров шапки.
