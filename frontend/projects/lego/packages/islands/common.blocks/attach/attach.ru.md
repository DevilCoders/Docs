# attach

Используется для выбора файла, предназначенного для отправки на сервер.

Реализация блока не позволяет:

- прикреплять несколько файлов;
- перетаскивать элементы (`drag-and-drop`).

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы использования | Описание |
| ----------- | ------------------- | -------------------- | -------- |
| [theme](#mods-theme) (req)  | `normal` | `BEMJSON` | Стилевое оформление блока. |
| [size](#mods-size) (req)  | `s`, `m` | `BEMJSON` | Размер блока. |
| [disabled](#mods-disabled) | `yes` | `BEMJSON`, `JS` | Неактивное состояние блока. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [name](#field-name) | `String` | Уникальное имя блока. |
| [id](#field-id) | Уникальный идентификатор кнопки, по которой выбирается файл. |
| [text](#field-text) | `String`| Текст кнопки для выбора файла. |
| [button](#field-button) | `BEMJSON` | Внешний вид и тип кнопки для выбора файла. |
| [holder](#field-holder) | `Boolean`, `String` | Добавляет текст сообщения, по умолчанию «файл не выбран». |
| [content](#field-content) | `BEMJSON`| Определяет внутри блока `attach` произвольную HTML-разметку. Если поле `content` задано, поля `text`, `holder`, `button` будут проигнорированы. |
| [tabindex](#field-tabindex)| `Number` | Порядок переключения фокуса между контролами при нажатии клавиши `Tab`. |

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Определяет стилевое оформление блока. **Обязательный**

Допустимое значение: `normal`.

Способ установки: `BEMJSON`.

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' }
}
```

<a name="mods-size"></a>

#### Модификатор `size`

Определяет размер блока. **Обязательный**

Допустимые значения: `s`, `m`.

Способы установки: `BEMJSON`.

```js
{
    block: 'x-table',
    head: ['s', 'm'],
    body: [
        ['s', 'm'].map(function(size) {
            return {
                block: 'attach',
                mods: { theme: 'normal', size: size }
            };
        })
    ]
}
```

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Отвечает за неактивное состояние, при котором блок виден, но недоступен для действий пользователя.

Допустимое значение: `yes`.

Способы установки: `BEMJSON`, `JS`.

**Кнопка выбора файла в неактивном состоянии**

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm', disabled: 'yes' }
}
```

### Поля блока

<a name="field-name"></a>

#### Поле `name`

Определяет уникальное имя блока. По умолчанию имеет значение `attachment`.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['attachment', 'attach-logo'],
    body: [
        ['', 'attach-logo'].map(function(name) {
            return {
                block: 'attach',
                mods: { theme: 'normal', size: 'm', name: name }
            };
        })
    ]
}
```

<a name="field-id"></a>

#### Поле `id`

Определяет уникальный идентификатор блока.

Тип: `String`.

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' },
    id: 'attach-logo'
}
```

<a name="field-text"></a>

#### Поле `text`

Определяет текст кнопки выбора файла. По умолчанию имеет значение `Выбрать файл`.

Поле будет проигнорировано, если задано поле `content`.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Текст по умолчанию', 'Произвольный текст'],
    body: [
        ['', 'Давай выберим файл'].map(function(text) {
            return {
                block: 'attach',
                mods: { theme: 'normal', size: 'm' },
                text: text
            };
        })
    ]
}
```

<a name="field-button"></a>

#### Поле `button`

Определяет внешний вид и тип кнопки для выбора файла. Значения API как для блока `button2`.

Поле будет проигнорировано, если задано поле `content`.

Тип: `BEMJSON`.

```js
[
    {
        block: 'attach',
        mods: { theme: 'normal', size: 'm' },
        button: {
            mods: { theme: 'action', size: 'm', action: 'yes', view: 'default', tone: 'default' },
            text: 'Загрузить'
        }
    },
    {
        block: 'x-deps',
        content: [
            { block: 'button2', mods: { theme: 'action', size: 'm', action: 'yes', view: 'default', tone: 'default' } }
        ]
    }
]
```

<a name="field-holder"></a>

#### Поле `holder`

Определяет текст сообщения возле кнопки выбора файла. Текст возможно отключить — значение поля `false`, либо отобразить по умолчанию `файл не выбран` — значение поля `true`.

Поле будет проигнорировано, если задано поле `content`.

Тип: `String`, `Boolean`.

```js
{
    block: 'x-table',
    head: ['Boolean', 'String'],
    body: [
        [true, 'Выберите файл'].map(function(holder) {
            return {
                block: 'attach',
                mods: { theme: 'normal', size: 'm' },
                holder: holder
            };
        })
    ]
}
```

<a name="field-content"></a>

#### Поле `content`

Определяет внутри блока `attach` произвольную HTML-разметку. Всю логику работы блока необходимо будет реализовывать самостоятельно.

Если поле `content` задано, поля `text`, `holder`, `button` будут проигнорированы.

Способ установки: `BEMJSON`.

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' },
    content: {
        block: 'button2',
        mods: { theme: 'action', size: 'm', view: 'default', tone: 'default', 'has-control': 'yes' },
        name: 'attachment',
        text: 'Выбрать файл'
    }
}
```

<a name="field-tabindex"></a>

#### Поле `tabindex`

Определяет в каком порядке будет переключаться фокус между контролами при нажатии клавиши `Tab`.

Тип: `Number`.

```js
{
  block: 'attach',
  mods: { theme: 'normal', size: 'm' },
  tabindex: 2
}
```
