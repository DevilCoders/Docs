# textarea

Используется для создания многострочного текстового поля.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [theme](#mods-theme) (req) | `normal` | `BEMJSON`, `JS` | Тема оформления текстового поля. |
| [size](#mods-size) (req) | `xs`, `s`, `m` | `BEMJSON`, `JS` | Размер текстового поля. |
| [view](#mods-view) | `default`, `classic` | `BEMJSON` `JS` | Вид текстового поля. |
| [tone](#mods-tone) | `default`, `dark`, `grey`, `red` | `BEMJSON`, `JS` | Цветовой тон текстового поля. |
| [has-clear](#mods-has-clear) | `yes` | `BEMJSON`, `JS` | Крестик для очистки текстового поля. |
| [disabled](#mods-disabled) | `yes` | `BEMJSON`, `JS` | Неактивное состояние текстового поля. |
| [focused](#mods-focused) | `yes` | `BEMJSON`, `JS` | Фокус на текстовом поле. |
| [hovered](#mods-hovered) | `yes` | — | Действие при наведении на текстовое поле курсором. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [text](#field-text) | `String`, `Number` | Содержимое текстового поля. |
| [name](#field-name) | `String` | Уникальное имя текстового поля. |
| [placeholder](#field-placeholder) | `String` | Подсказка в текстовом поле. Исчезает при вводе текста. |
| [autocomplete](#field-autocomplete) | `Boolean` | Отключение автозаполнения текстового поля. |
| [cols](#field-cols) | `Number` | Ширина текстового поля в символах. |
| [rows](#field-rows) | `Number` | Высота текстового поля в строках текста. |
| [id](#field-id) | `String` | Уникальный идентификатор текстового поля. |
| [tabindex](#field-tabindex) | `Number` | Последовательность перехода между контролами при нажатии на `Tab`. |
| [controlAttrs](#field-controlAttrs) | `Object` | Произвольный набор HTML-атрибутов для элемента `control`. |

> **Важно!** Поле `content` не определено.

## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Определяет тему оформления текстового поля. **Обязательный**.

Допустимое значение: `normal`.

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

Определяет размер текстового поля. **Обязательный**.

Допустимые значения: `xs`, `s`, `m`.

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

<a name="mods-view"></a>

#### Модификатор `view`

Определяет вид текстового поля.

Допустимые значения:  `default`, `classic`.

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['classic', 'default'],
    body: [
        ['classic', 'default'].map((view) => {
            return {
                block: 'textarea',
                mods: { theme: 'normal', size: 'm', tone: 'default', view: view },
                text: 'Текстовое поле'
            };
        })
    ]
}
```

<a name="mods-tone"></a>

#### Модификатор `tone`

Определяет цветовой тон блока.

Допустимые значения:  `default`, `dark`, `grey`, `red`.

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['default', 'dark', 'grey', 'red'],
    body: [
        ['default', 'dark', 'grey', 'red'].map((tone) => {
            return {
                block: 'textarea',
                mods: { theme: 'normal', size: 'm', tone: tone, view: 'default' },
                text: 'Текстовое поле'
            };
        })
    ]
}
```

<a name="mods-has-clear"></a>

#### Модификатор `has-clear`

Добавляет крестик для очистки содержимого текстового поля.

Допустимые значения: `yes`.

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

Определяет неактивное состояние, при котором текстовое поле становится недоступно для действий пользователя.

С включенным модификатором `disabled` невозможно:

* установить модификаторы `focused`, `pressed` и `hovered` — они автоматически удалятся;
* вызвать БЭМ-события.

Допустимое значение: `yes`.

Способы установки: `BEMJSON`, `JS`.

> **Примечание.** Неактивное состояние поля можно изменять программно.

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

<a name="mods-focused"></a>

#### Модификатор `focused`

Устанавливает фокус на блоке. Выставляется автоматически.

Допустимое значение: `yes`.

Способы установки: `BEMJSON`, `JS`.

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

Определяет действие блока при наведении на него курсором. Выставляется автоматически.

Допустимое значение: `yes`.

Способы установки: `—`.

### Поля блока

<a name="field-text"></a>

#### Поле `text`

Определяет содержимое текстового поля.

Тип: `String`, `Number`.

> **Примечание.** Переданное значение экранируется автоматически.

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

> **Примечание.** По умолчанию автозаполнение включено и зависит от настроек браузера.

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

Определяет произвольный набор HTML-атрибутов для элемента `control`.

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
