# search2

Используется для создания поисковой формы.

# Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [template](#mods-template) | `websearch` | `BEMJSON` | Шаблон контента для поисковой формы |

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [input](#fields-input)| `BEMJSON` | Содержимое контейнера для поля ввода поисковой формы |
| [button](#fields-button)| `BEMJSON` | Содержимое контейнера для кнопки поиска |
| [hidden](#fields-hidden) | `Object` | Ключи и значения скрытых полей поисковой формы |
| [label](#fields-label)| `String` | Значение атрибута `aria-label` для программ экранного доступа |
| [url](#fields-url)| `String` | Адрес перехода при нажатии на кнопку поиска |

## Подробное описание

### Модификаторы блока

<a name="mods-template"></a>

#### Модификатор `template`

Определяет для поисковой формы шаблон контента по умолчанию. Значения полей определены в шаблоне [BEMHTML](../../common.blocks/search2/_template/search2_template_websearch.bemhtml.js). Рекомендуется использовать в ознакомительных целях или когда кастомизация поисковой формы не нужна.

> **Примечание.** Чтобы использовать опциональный модификатор `template`, укажите его в зависимостях блока на проектном уровне.

Допустимое значение: `websearch`.

Способ установки: `BEMJSON`.

```js
[
    {
        block: 'search2',
        mods: {
            template: 'websearch'
        }
    },
    {
        block: 'x-deps',
        content: [
            { block: 'search2', mods: { template: 'websearch' } }
        ]
    }
]
```

### Поля блока

<a name="fields-input"></a>

#### Поле `input`

Определяет содержимое контейнера для поля ввода поисковой формы.

Тип: `BEMJSON`.

```js
{
    block: 'search2',
    input: {
        block: 'input',
        mods: { size: 'm', theme: 'normal', pin: 'round-clear'},
        value: 'islands',
        content: {elem: 'control', attrs: {name: 'text'}}
    },
    button: {
        block: 'button2',
        mods: { size: 'm', theme: 'action', type: 'submit', pin: 'brick-round'},
        text: 'Найти'
    }
}
```

<a name="fields-button"></a>

#### Поле `button`

Определяет содержимое контейнера для кнопки поиска.

Тип: `BEMJSON`.

```js
{
    block: 'search2',
    input: {
        block: 'input',
        mods: { size: 'm', theme: 'normal', pin: 'round-clear' },
        value: 'islands',
        content: { elem: 'control', attrs: { name: 'text'} }
    },
    button: {
        block: 'button2',
        mods: { size: 'm', theme: 'action', type: 'submit', pin: 'brick-round'},
        text: 'Найти'
    }
}
```

<a name="fields-hidden"></a>

#### Поле `hidden`

Определяет ключи и значения скрытых полей поисковой формы. Содержит набор пар вида `name: value`.

Тип: `BEMJSON`.

```js
{
    block: 'search2',
    hidden: {
        name: 'Finn',
        kind: 'Human'
    },
    input: {
        block: 'input',
        mods: { size: 'm', theme: 'normal', pin: 'round-clear' },
        value: 'islands',
        content: { elem: 'control', attrs: { name: 'text'} }
    },
    button: {
        block: 'button2',
        mods: { size: 'm', theme: 'action', type: 'submit', pin: 'brick-round'},
        text: 'Найти'
    }
}
```

<a name="fields-label"></a>

#### Поле `label`

Определяет значение атрибута `aria-label`, который используется в качестве ярлыка для программ экранного доступа.

Тип: `String`.

```js
{
    block: 'search2',
    label: 'Искать в Яндексе',
    input: {
        block: 'input',
        mods: { size: 'm', theme: 'normal', pin: 'round-clear' },
        content: { elem: 'control', attrs: { name: 'text'} }
    },
    button: {
        block: 'button2',
        mods: { size: 'm', theme: 'action', type: 'submit', pin: 'brick-round'},
        text: 'Найти'
    }
}
```

<a name="fields-url"></a>

#### Поле `url`

Определяет адрес, по которому осуществляется переход при нажатии кнопки поиска.

Тип: `String`.

```js
{
    block: 'search2',
    url: 'https://yandex.ru/search',
    input: {
        block: 'input',
        mods: { size: 'm', theme: 'normal', pin: 'round-clear' },
        content: { elem: 'control', attrs: { name: 'text'} }
    },
    button: {
        block: 'button2',
        mods: { size: 'm', theme: 'action', type: 'submit', pin: 'brick-round'},
        text: 'Найти'
    }
}
```