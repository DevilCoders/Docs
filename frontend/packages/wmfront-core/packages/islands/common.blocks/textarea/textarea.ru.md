# textarea

Используется для создания многострочного текстового поля.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [theme](#mods-theme) (req) | `'normal'` | `BEMJSON`, `JS` | Стилевое оформление. |
| [size](#mods-size) (req) | `'xs'`, `'s'`, `'m'` | `BEMJSON`, `JS` | Размер текстового поля. |
| [has-clear](#mods-has-clear) | `'yes'` | `BEMJSON`, `JS` | Крестик для очистки текстового поля. |
| [disabled](#mods-disabled) | `'yes'` | `BEMJSON`, `JS` | Неактивное состояние. |
| [focused](#mods-focused) | `'yes'` | `BEMJSON`, `JS` | Фокус на блоке. |
| [hovered](#mods-hovered) | `'yes'` | — | Наведение на текстовое поле курсором. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [text](#field-text) | `String`, `Number` | Содержимое текстового поля. |
| [name](#field-name) | `String` | Уникальное имя блока. |
| [placeholder](#field-placeholder) | `String` | Подсказка в текстовом поле. Исчезает при вводе текста. |
| [autocomplete](#field-autocomplete) | `Boolean` | Отключение автозаполнения текстового поля. |
| [cols](#field-cols) | `Number` | Ширина поля в символах. |
| [rows](#field-rows) | `Number` | Высота поля в строках текста. |
| [id](#field-id) | `String` | Уникальный идентификатор блока. |
| [tabindex](#field-tabindex) | `Number` | Последовательность перехода между контролами при нажатии на `Tab`. |
| [controlAttrs](#field-controlAttrs) | `Object` | Произвольный набор HTML-атрибутов для элемента [control](#elem-control). |

> **Важно!** Поле `content` не определено.

<a name="elems"></a>

### Элементы блока

| Элемент | Описание |
| ------- | -------- |
| `box` | Фон и рамка текстового поля. |
| `clear` | Крестик для очистки текстового поля. Формируется блоком [icon](../icon/icon.ru.md). |
| `control` | Нативный элемент текстовой области `<textarea>`. Используется для реализации функциональности блока. Может принимать произвольный набор HTML-атрибутов через поле [controlAttrs](#field-controlAttrs). |
| `wrap` | Контейнер для текстового поля. |

> **Важно!** В API блока не предусмотрена возможность формирования произвольной HTML-разметки, с помощью элементов блока.

## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Отвечает за стилевое оформление текстового поля. **Обязательный**.

Допустимое значение: `'normal'`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['normal'],
    body: [
        {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm' },
            text: 'Тема normal'
        }
    ]
}
```

<a name="mods-size"></a>

#### Модификатор `size`

Задает размер текстового поля. **Обязательный**.

Допустимые значения: `'xs'`, `'s'`, `'m'`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['xs', 's', 'm'],
    body: [
        ['xs', 's', 'm'].map(function(size) {
            return {
                block: 'textarea',
                mods: { theme: 'normal', size: size },
                text: 'Размер ' + size
            };
        })
    ]
}
```

<a name="mods-has-clear"></a>

#### Модификатор `has-clear`

Добавляет крестик для очистки содержимого текстового поля.

Допустимые значения: `'yes'`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['_has-clear'],
    body: [
        {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm', 'has-clear': 'yes' },
            text: 'Текстовое поле с крестиком'
        }
    ]
}
```

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Отвечает за неактивное состояние, при котором текстовое становится недоступно для действий пользователя.

Нельзя:

* установить модификаторы `focused`, `pressed` и `hovered` (существующие удаляются);
* вызвать БЭМ-события.

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['_disabled'],
    body: [
        {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm', disabled: 'yes' },
            text: 'Текстовое поле неактивно'
        }
    ]
}
```

> **Примечание.** Неактивное состояние поля можно изменять программно.

<a name="mods-focused"></a>

#### Модификатор `focused`

Отвечает за наличие фокуса на блоке.

Допустимое значение:`'yes'`.

Способы установки: `BEMJSON`, `JS`.

Выставляется автоматически при получении блоком фокуса.

```js
{
    block: 'x-table',
    head: ['_focused'],
    body: [
        {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm', focused: 'yes' },
            text: 'Текстовое поле в фокусе'
        }
    ]
}
```

<a name="mods-hovered"></a>

#### Модификатор `hovered`

Определяет действие «наведение на текстовое поле курсором».

Допустимое значение: `'yes'`.

Способы установки: `—`.

Выставляется автоматически.

### Поля блока

<a name="field-text"></a>

#### Поле `text`

Определяет содержимое текстового поля.

Тип: `String`, `Number`.

```js
{
    block: 'x-table',
    head: ['Поле text'],
    body: [
        {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm' },
            text: 'Текстовое поле' // Переданное значение экранируется автоматически
        }
    ]
}
```

> **Примечание.** Переданное значение экранируется автоматически.

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
            block: 'textarea',
            mods: { theme: 'normal', size: 'm' },
            name: 'the-name',
            text: 'Текстовое поле'
        }
    ]
}
```

<a name="field-placeholder"></a>

#### Поле `placeholder`

Определяет текст подсказки. Исчезает при вводе текста.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле placeholder'],
    body: [
        {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm' },
            placeholder: 'The placeholder'
        }
    ]
}
```

<a name="field-autocomplete"></a>

#### Поле `autocomplete`

Отключает автозаполнение текстового поля введенным ранее текстом.

Допустимое значение: `false`.

Тип: `Boolean`.

```js
{
    block: 'x-table',
    head: ['Поле autocomplete'],
    body: [
        {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm' },
            autocomplete: false,
            text: 'Текстовое поле'
        }
    ]
}
```

> **Примечание.** По умолчанию автозаполнение включено и зависит от настроек браузера.

<a name="field-cols"></a>

#### Поле `cols`

Определяет ширину текстового поля в символах.

Тип: `Number`.

```js
{
    block: 'x-table',
    mods: { theme: 'area' },
    head: [10, 30, 40],
    body: [10, 30, 40].map(function(colsNum) {
        return {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm' },
            cols: colsNum,
            text: ['Вполне вероятно, что это даже многострочный текст получится.', 'Нельзя быть абсолютно уверенным, но такое возможно.'].join(' ')
        };
    })
}
```

<a name="field-rows"></a>

#### Поле `rows`

Определяет высоту текстового поля в строках.

Тип: `Number`.

```js
{
    block: 'x-table',
    mods: { theme: 'area' },
    head: [10, 15, 20],
    body: [10, 15, 20].map(function(rowsNum) {
        return {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm' },
            rows: rowsNum,
            text: ['Вполне вероятно, что это даже многострочный текст получится.', 'Нельзя быть абсолютно уверенным, но такое возможно.'].join(' ')
        };
    })
}
```

<a name="field-id"></a>

#### Поле `id`

Определяет уникальный идентификатор текстового поля.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле id'],
    body: [
        {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm' },
            id: 'the-id',
            text: 'Текстовое поле'
        }
    ]
}
```

<a name="field-tabindex"></a>

#### Поле `tabIndex`

Определяет последовательность перехода между контролами при нажатии на `Tab`.

Тип: `Number`.

```js
{
    block: 'x-table',
    head: ['Поле tabIndex'],
    body: [
        {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm' },
            tabIndex: 1,
            text: 'Текстовое поле'
        }
    ]
}
```

<a name="field-controlattrs"></a>

#### Поле `controlAttrs`

Определяет произвольный набор HTML-атрибутов для элемента [control](#elem-control).

Тип: `Object`.

```js
{
    block: 'x-table',
    head: ['Поле controlAttrs'],
    body: [
        {
            block: 'textarea',
            mods: { theme: 'normal', size: 'm' },
            controlAttrs: { autofocus: true },
            text: 'Текстовое поле c автофокусом'
        }
    ]
}
```
