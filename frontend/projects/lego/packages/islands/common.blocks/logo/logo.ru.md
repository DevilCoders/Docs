# logo

Используется для создания логотипа.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [name](#mods-name) (req) | `'en-63x27'`, `'en-84x36'`, `'en-98x42'`, `'en-w-63x27'`, `'en-w-84x36'`, `'en-w-98x42'`, `'ru-63x27'`, `'ru-84x36'`, `'ru-98x42'`, `'ru-w-63x27'`, `'ru-w-84x36'`, `'ru-w-98x42'`, `'ys-en-66x27'`, `'ys-en-69x28'`, `'ys-en-84x35'`, `'ys-en-87x35'`, `'ys-en-102x42'`, `'ys-en-w-66x27'`, `'ys-en-w-69x28'`, `'ys-en-w-84x35'`, `'ys-en-w-87x35'`, `'ys-en-w-102x42'`, `'ys-ru-64x27'`, `'ys-ru-69x28'`, `'ys-ru-84x35'`, `'ys-ru-86x35'`, `'ys-ru-98x42'`, `'ys-ru-w-64x27'`, `'ys-ru-w-69x28'`, `'ys-ru-w-84x35'`, `'ys-ru-w-86x35'`, `'ys-ru-w-98x42'` | `BEMJSON`, `JS` | Набор стандартных логотипов. |
| [type](#mods-type) | `'link'` | `BEMJSON` | Логотип-ссылка. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [title](#field-title) | `String` | Текст всплывающей подсказки. |
| [url](#field-url) | `String` | Адрес. |
| [text](#field-text) | `String` | Альтернативный текст для логотипа. |

## Подробное описание

### Модификаторы блока

<a name="mods-name"></a>

#### Модификатор `name`

Определяет логотип Яндекса (Yandex).

Допустимые значения:

| | 63x27 | 64x27 | 66x27 | 69x28 | 84x35 | 84x36 | 86x35 | 87x35 | 98x42 | 102x42 |
| :--: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Английский** | `'en-63x27'` | — | — | — | — | `'en-84x36'` |  — | — | `'en-98x42'` | — |
| **Русский** | `'ru-63x27'` | — | — | — | — | `'ru-84x36'` | — | — | `'ru-98x42'` | — |
| **Английский (белый)** | `'en-w-63x27'` | — | — | — | — | `'en-w-84x36'` | — | — | `'en-w-98x42'` | — |
| **Русский (белый)** | `'ru-w-63x27'` | — | — | — | — | `'ru-w-84x36'` | — | — | `'ru-w-98x42'` | — |
| **Английский (Yandex Sans)** | — | — | `'ys-en-66x27'` | `'ys-en-69x28'` | `'ys-en-84x35'` | — | — | `'ys-en-87x35'` | — | `'ys-en-102x42'` |
| **Русский (Yandex Sans)** | — | `'ys-ru-64x27'` | — | `'ys-ru-69x28'` | `'ys-ru-84x35'` | — | `'ys-ru-86x35'` | — | `'ys-ru-98x42'` | — |
| **Английский (Yandex Sans белый)** | — | — | `'ys-en-w-66x27'` | `'ys-en-w-69x28'` | `'ys-en-w-84x35'` | — | — | `'ys-en-w-87x35'` | — | `'ys-en-w-102x42'` |
| **Русский (Yandex Sans белый)** | — | `'ys-ru-w-64x27'` | — | `'ys-ru-w-69x28'` | `'ys-ru-w-84x35'` | — | `'ys-ru-w-86x35'` | — | `'ys-ru-w-98x42'` | — |

Способ установки: `BEMJSON`.

**Стандартный английский логотип**

```js
{
    block: 'x-area',
    mods: {
        bordered: 'yes',
        role: 'logos-wrap',
        has: 'state',
        state: 'cur'
    },
    content: ['en-63x27', 'en-84x36', 'en-98x42'].map(function(name) {
        return {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        name: name
                    }
                },
                {
                    elem: 'caption',
                    content: name
                }
            ]
        };
    })
}
```

**Стандартный русский логотип**

```js
{
    block: 'x-area',
    mods: {
        bordered: 'yes',
        role: 'logos-wrap',
        has: 'state',
        state: 'cur'
    },
    content: ['ru-63x27', 'ru-84x36', 'ru-98x42'].map(function(name) {
        return {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        name: name
                    }
                },
                {
                    elem: 'caption',
                    content: name
                }
            ]
        };
    })
}
```

**Английский логотип (белый)**

```js
{
    block: 'x-area',
    attrs: { id: 'logos-white' },
    mods: {
        bordered: 'yes',
        role: 'logos-wrap'
    },
    content: ['en-w-63x27', 'en-w-84x36', 'en-w-98x42'].map(function(name) {
        return {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        name: name
                    }
                },
                {
                    elem: 'caption',
                    content: name
                }
            ]
        };
    })
}
```

**Русский логотип (белый)**

```js
{
    block: 'x-area',
    attrs: { id: 'logos-white' },
    mods: {
        bordered: 'yes',
        role: 'logos-wrap'
    },
    content: ['ru-w-63x27', 'ru-w-84x36', 'ru-w-98x42'].map(function(name) {
        return {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        name: name
                    }
                },
                {
                    elem: 'caption',
                    content: name
                }
            ]
        };
    })
}
```

**Английский логотип (Yandex Sans)**

```js
{
    block: 'x-area',
    mods: {
        bordered: 'yes',
        role: 'logos-wrap',
        has: 'state',
        state: 'cur'
    },
    content: ['ys-en-66x27', 'ys-en-69x28', 'ys-en-84x35', 'ys-en-87x35', 'ys-en-102x42'].map(function(name) {
        return {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        name: name
                    }
                },
                {
                    elem: 'caption',
                    content: name
                }
            ]
        };
    })
}
```

**Русский логотип (Yandex Sans)**

```js
{
    block: 'x-area',
    mods: {
        bordered: 'yes',
        role: 'logos-wrap',
        has: 'state',
        state: 'cur'
    },
    content: ['ys-ru-64x27', 'ys-ru-69x28', 'ys-ru-84x35', 'ys-ru-86x35', 'ys-ru-98x42'].map(function(name) {
        return {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        name: name
                    }
                },
                {
                    elem: 'caption',
                    content: name
                }
            ]
        };
    })
}
```

**Английский логотип (Yandex Sans белый)**

```js
{
    block: 'x-area',
    attrs: { id: 'logos-white' },
    mods: {
        bordered: 'yes',
        role: 'logos-wrap'
    },
    content: ['ys-en-w-66x27', 'ys-en-w-69x28', 'ys-en-w-84x35', 'ys-en-w-87x35', 'ys-en-w-102x42'].map(function(name) {
        return {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        name: name
                    }
                },
                {
                    elem: 'caption',
                    content: name
                }
            ]
        };
    })
}
```

**Русский логотип (Yandex Sans белый)**

```js
{
    block: 'x-area',
    attrs: { id: 'logos-white' },
    mods: {
        bordered: 'yes',
        role: 'logos-wrap'
    },
    content: ['ys-ru-w-64x27', 'ys-ru-w-69x28', 'ys-ru-w-84x35', 'ys-ru-w-86x35', 'ys-ru-w-98x42'].map(function(name) {
        return {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        name: name
                    }
                },
                {
                    elem: 'caption',
                    content: name
                }
            ]
        };
    })
}
```

> **Примечание.** Чтобы создать собственный логотип, нужно добавить новое значение для модификатора `name` с нужным изображением.

```js
{
    block: 'x-area',
    mods: {
        bordered: 'yes',
        role: 'logos-wrap',
        has: 'state',
        state: 'cur'
    },
    content: ['home', 'ppr'].map(function(name) {
        return {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        name: name
                    }
                },
                {
                    elem: 'caption',
                    content: name
                }
            ]
        };
    })
}
```

<a name="mods-type"></a>

#### Модификатор `type`

Определяет логотип ссылкой.

Допустимое значение: `'link'`.

Способ установки: `BEMJSON`.

> **Примечание.** По умолчанию обеспечивает переход на главную страницу сервиса в текущей локализации (определяется из блока [i-services](../i-services/i-services.ru.md)). Адрес перехода можно определять самостоятельно в поле [url](#field-url).

```js
{
    block: 'x-area',
    mods: {
        bordered: 'yes',
        role: 'logos-wrap',
        has: 'state',
        state: 'cur'
    },
    content: [
        {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        type: 'link',
                        name: 'ys-ru-84x35'
                    },
                    title: 'На главную'
                },
                {
                    elem: 'caption',
                    content: 'default url'
                }
            ]
        },
        {
            block: 'x-area',
            content: [
                {
                    block: 'logo',
                    mods: {
                        type: 'link',
                        name: 'ys-ru-84x35'
                    },
                    text: 'ya.ru',
                    url: 'https://ya.ru',
                    title: 'На главную'
                },
                {
                    elem: 'caption',
                    content: 'custom url'
                }
            ]
        }
    ]
}
```

### Поля блока

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
            block: 'logo',
            mods: {
                type: 'link',
                name: 'ys-ru-84x35'
            },
            title: 'На главную'
        }
    ]
}
```

<a name="field-url"></a>

#### Поле `url`

Определяет адрес для ссылки логотипа.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле url'],
    body: [
        {
            block: 'logo',
            mods: {
                type: 'link',
                name: 'ys-ru-84x35'
            },
            url: 'https://ya.ru',
            title: 'На главную'
        }
    ]
}
```

<a name="field-text"></a>

#### Поле `text`

Определяет альтернативный текст для логотипа.

Используется для нужд SEO или программ экранного доступа.

Тип: `String`.

> **Примечание.** Значение по умолчанию: локализованное слово «Яндекс» («Yandex»). Текст скрыт от пользователя (`text-indent: 100%`).

```js
{
    block: 'x-table',
    head: ['Поле text'],
    body: [
        {
            block: 'logo',
            mods: {
                type: 'link',
                name: 'ys-ru-84x35'
            },
            text: 'ya.ru',
            url: 'https://ya.ru',
            title: 'На главную'
        }
    ]
}
```
