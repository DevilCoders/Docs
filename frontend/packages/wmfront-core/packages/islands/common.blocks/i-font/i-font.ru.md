# i-font

Используется для установки шрифта текстовым элементам.

> **Примечание.** Шрифты доступны на [yastatic.net](https://lego-staging.dev.yandex-team.ru/islands/dev/desktop.examples/i-font/all/all.html#Шрифты).

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [face](#mods-face) (req) | `'konkord'`, `'rub-arial-regular'`, `'textbook-new-bold'`, `'textbook-new-light'`, `'textbook'`, `'yandex-en'`, `'yandex-ru'`, `'yandex-sans-display-bold'`, `'yandex-sans-display-light'`, `'yandex-sans-display-regular'`, `'yandex-sans-display-thin'`, `'yandex-sans-text-bold'`, `'yandex-sans-text-light'`, `'yandex-sans-text-medium'`, `'yandex-sans-text-regular'`, `'yandex-sans-text-thin'`, `'yandex-sans-text'`, `'ys-display-bold'`, `'ys-display-heavy'`, `'ys-display-light'`, `'ys-display-medium'`, `'ys-display-regular'`, `'ys-display-thin'`, `'ys-text-bold-italic'`, `'ys-text-bold'`, `'ys-text-light-italic'`, `'ys-text-light'`, `'ys-text-medium-italic'`, `'ys-text-medium'`, `'ys-text-regular-italic'`, `'ys-text-regular'` | `BEMJSON`, `JS` | Шрифт. |
| [antialiased](#mods-antialiased) | `'yes'` | `BEMJSON`, `JS` | Сглаживание шрифтов на дисплеях со стандартной плотностью пикселей. |

## Подробное описание

### Модификаторы блока

<a name="mods-face"></a>

#### Модификатор `face`

Отвечает за установку шрифта. **Обязательный**.

Допустимые значения: `'konkord'`, `'rub-arial-regular'`, `'textbook-new-bold'`, `'textbook-new-light'`, `'textbook'`, `'yandex-en'`, `'yandex-ru'`, `'yandex-sans-display-bold'`, `'yandex-sans-display-light'`, `'yandex-sans-display-regular'`, `'yandex-sans-display-thin'`, `'yandex-sans-text-bold'`, `'yandex-sans-text-light'`, `'yandex-sans-text-medium'`, `'yandex-sans-text-regular'`, `'yandex-sans-text-thin'`, `'yandex-sans-text'`, `'ys-display-bold'`, `'ys-display-heavy'`, `'ys-display-light'`, `'ys-display-medium'`, `'ys-display-regular'`, `'ys-display-thin'`, `'ys-text-bold-italic'`, `'ys-text-bold'`, `'ys-text-light-italic'`, `'ys-text-light'`, `'ys-text-medium-italic'`, `'ys-text-medium'`, `'ys-text-regular-italic'`, `'ys-text-regular'`.

Способ установки: `BEMJSON`, `JS`.

**Konkord**

```js
{
    block: 'x-table',
    xhead: ['konkord'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes', size: 'l' },
            mix: { block: 'i-font', mods: { face: 'konkord' } },
            content: [
                {
                    block: 'x-lorem',
                    paragraphs: 1
                }
            ]
        }
    ]
}
```

**rub-arial-regular**

```js
[
    {
        block: 'x-table',
        xhead: ['text', 'radio-button'],
        body: [
            [
                {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    mix: { block: 'i-font', mods: { face: 'rub-arial-regular' } },
                    content: '150 Р'
                },
                {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: [
                        {
                            block: 'i-lego-example',
                            content: [
                                {
                                    block: 'radio-button',
                                    mods: { size: 'm', theme: 'normal' },
                                    name: 'show_to',
                                    content: [
                                        {
                                            elem: 'radio',
                                            controlAttrs: { value: 'a' },
                                            content: [
                                                '0 – 100 ',
                                                {
                                                    elem: 'rub',
                                                    content: 'Р'
                                                }
                                            ]
                                        },
                                        {
                                            elem: 'radio',
                                            controlAttrs: { value: 'b' },
                                            content: [
                                                '101 – 200 ',
                                                {
                                                    elem: 'rub',
                                                    content: 'Р'
                                                }
                                            ]
                                        },
                                        {
                                            elem: 'radio',
                                            controlAttrs: { value: 'c' },
                                            content: [
                                                '201 – 300 ',
                                                {
                                                    elem: 'rub',
                                                    content: 'Р'
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        ]
    }
]
```

**Textbook**

```js
{
    block: 'x-table',
    xhead: ['textbook', 'textbook-new-bold', 'textbook-new-light'],
    body: [
        ['textbook', 'textbook-new-bold', 'textbook-new-light'].map(function(face) {
            return  [
                {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    mix: { block: 'i-font', mods: { face: face } },
                    content: [
                        {
                            block: 'x-lorem',
                            paragraphs: 1
                        }
                    ]
                }
            ];
        })
    ]
}
```

**Yandex En**

```js
{
    block: 'x-table',
    xhead: ['yandex-en'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes', size: 'l' },
            mix: { block: 'i-font', mods: { face: 'yandex-en' } },
            content: [
                {
                    block: 'x-lorem',
                    paragraphs: 1
                }
            ]
        }
    ]
}
```

**Yandex Ru**

```js
{
    block: 'x-table',
    xhead: ['yandex-ru'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes', size: 'l' },
            mix: { block: 'i-font', mods: { face: 'yandex-ru' } },
            content: ['Вполне вероятно, что это даже многострочный текст получится.', 'Нельзя быть абсолютно уверенным, но такое возможно.'].join(' ')
        }
    ]
}
```

**Yandex Sans Text**

```js
{
    block: 'x-table',
    xhead: ['yandex-sans-text-regular', 'yandex-sans-text-bold', 'yandex-sans-text-medium', 'yandex-sans-text-light', 'yandex-sans-text-thin', 'yandex-sans-text'],
    body: [
        ['yandex-sans-text-regular', 'yandex-sans-text-bold', 'yandex-sans-text-medium', 'yandex-sans-text-light', 'yandex-sans-text-thin', 'yandex-sans-text'].map(function(face) {
            return  [
                {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    mix: { block: 'i-font', mods: { face: face } },
                    content: [
                        {
                            block: 'x-lorem',
                            paragraphs: 1
                        }
                    ]
                }
            ];
        })
    ]
}
```

**Yandex Sans Display**

```js
{
    block: 'x-table',
    xhead: ['yandex-sans-display-regular', 'yandex-sans-display-bold', 'yandex-sans-display-light', 'yandex-sans-display-thin'],
    body: [
        ['yandex-sans-display-regular', 'yandex-sans-display-bold', 'yandex-sans-display-light', 'yandex-sans-display-thin'].map(function(face) {
            return  [
                {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    mix: { block: 'i-font', mods: { face: face } },
                    content: [
                        {
                            block: 'x-lorem',
                            paragraphs: 1
                        }
                    ]
                }
            ];
        })
    ]
}
```

**YS Display**

```js
{
    block: 'x-table',
    xhead: ['ys-display-regular', 'ys-display-medium', 'ys-display-heavy', 'ys-display-bold', 'ys-display-light', 'ys-display-thin'],
    body: [
        ['ys-display-regular', 'ys-display-medium', 'ys-display-heavy', 'ys-display-bold', 'ys-display-light', 'ys-display-thin'].map(function(face) {
            return  [
                {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    mix: { block: 'i-font', mods: { face: face } },
                    content: [
                        {
                            block: 'x-lorem',
                            paragraphs: 1
                        }
                    ]
                }
            ];
        })
    ]
}
```

**YS Text (bold, regular)**

```js
{
    block: 'x-table',
    xhead: ['ys-text-bold', 'ys-text-bold-italic', 'ys-text-regular', 'ys-text-regular-italic' ],
    body: [
        ['ys-text-bold', 'ys-text-bold-italic', 'ys-text-regular', 'ys-text-regular-italic'].map(function(face) {
            return  [
                {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    mix: { block: 'i-font', mods: { face: face } },
                    content: [
                        {
                            block: 'x-lorem',
                            paragraphs: 1
                        }
                    ]
                }
            ];
        })
    ]
}
```

**YS Text (medium, light)**

```js
{
    block: 'x-table',
    xhead: ['ys-text-medium', 'ys-text-medium-italic', 'ys-text-light', 'ys-text-light-italic'],
    body: [
        ['ys-text-medium', 'ys-text-medium-italic', 'ys-text-light', 'ys-text-light-italic'].map(function(face) {
            return  [
                {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    mix: { block: 'i-font', mods: { face: face } },
                    content: [
                        {
                            block: 'x-lorem',
                            paragraphs: 1
                        }
                    ]
                }
            ];
        })
    ]
}
```

<a name="mods-antialiased"></a>

#### Модификатор `antialiased`

Сглаживает шрифт на дисплеях со стандартной плотностью пикселей.

Допустимое значение: `'yes'`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    xhead: ['normal', 'antialiased'],
    body: [
        [
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                mix: { block: 'i-font', mods: { face: 'ys-text-regular' } },
                content: [
                    {
                        block: 'x-lorem',
                        paragraphs: 1
                    }
                ]
            },
            {
                block: 'x-area',
                mods: { bordered: 'yes', theme: 'dark' },
                mix: { block: 'i-font', mods: { face: 'ys-text-regular', antialiased: 'yes' } },
                content: [
                    {
                        block: 'x-lorem',
                        paragraphs: 1
                    }
                ]
            }
        ],
        [
            {
                block: 'x-area',
                mods: { bordered: 'yes', theme: 'dark' },
                mix: { block: 'i-font', mods: { face: 'ys-text-regular' } },
                content: [
                    {
                        block: 'x-lorem',
                        paragraphs: 1
                    }
                ]
            },
            {
                block: 'x-area',
                mods: { bordered: 'yes' },
                mix: { block: 'i-font', mods: { face: 'ys-text-regular', antialiased: 'yes' } },
                content: [
                    {
                        block: 'x-lorem',
                        paragraphs: 1
                    }
                ]
            }
        ]
    ]
}
```
