# textinput

Используется для создания однострочного текстового поля.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [theme](#mods-theme) (req) | `normal`, `websearch` | `BEMJSON`, `JS` | Тема оформления текстового поля. |
| [size](#mods-size) (req) | `xs`, `s`, `m`, `n` | `BEMJSON`, `JS` | Размер текстового поля. |
| [view](#mods-view) | `default`, `classic` | `BEMJSON` `JS` | Вид текстового поля. |
| [tone](#mods-tone) | `default`, `dark`, `grey`, `red` | `BEMJSON`, `JS` | Цветовой тон текстового поля. |
| [type](#mods-type) | `text`, `email`, `tel`, `password`, `number` | `BEMJSON` | Тип текстового поля. |
| [pin](#mods-pin) | `brick-brick`, `brick-clear`, `clear-brick`, `round-clear`, `clear-round`, `round-brick`, `brick-round`, `clear-clear`, `round-round` | `BEMJSON`, `JS` | Форма текстового поля. |
| [poll](#mods-poll) | `yes` | `BEMJSON`, `JS` | Работа блока в режиме частых опросов. |
| [has-clear](#mods-has-clear) | `yes` | `BEMJSON`, `JS` | Наличие крестика для очистки текстового поля. |
| [has-icon](#mods-has-icon) | `yes` | `BEMJSON`, `JS` | Возможность использовать иконки в текстовом поле. |
| [has-nameplate](#mods-has-nameplate) (dep) | `yes` | `BEMJSON`, `JS` | Метка сервиса в текстовом поле. Формируется блоком [nameplate](../nameplate/nameplate.ru.md). |
| [disabled](#mods-disabled) | `yes` | `BEMJSON`, `JS` | Неактивное состояние текстового поля. |
| [focused](#mods-focused) | `yes` | `BEMJSON`, `JS` | Фокус на текстовом поле. |
| [hovered](#mods-hovered) | `yes` | — | Действие при наведении на текстовое поле курсором. |
| [baseline](#mods-baseline) | `false`, `true` | `BEMJSON`, `JS` | Выравнивание текстового поля по базовой линии. |

* req — обязательный модификатор.
* dep — устаревший модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [text](#field-text) | `String`, `Number` | Содержимое текстового поля. |
| [icon](#field-icon) | `BEMJSON` | Иконка в текстовом поле. Формируется блоком [icon](../icon/icon.ru.md). Используется только для поля с [модификатором has-icon](#mods-has-icon). |
| [iconLeft](#field-iconleft) | `BEMJSON` | Иконка слева от текста поля. Используется только для поля с [модификатором has-icon](#mods-has-icon). |
| [iconRight](#field-iconright) | `BEMJSON` | Иконка справа от текста поля. Используется только для поля с [модификатором has-icon](#mods-has-icon). |
| [name](#field-name) | `String` | Уникальное имя блока. |
| [placeholder](#field-placeholder) | `String` | Подсказка в текстовом поле. Исчезает при вводе текста. |
| [autocomplete](#field-autocomplete) | `Boolean` | Отключение автозаполнения текстового поля. |
| [id](#field-id) | `String` | Уникальный идентификатор текстового поля. |
| [tabindex](#field-tabindex) | `Number` | Последовательность перехода между контролами при нажатии на `Tab`. |
| [controlAttrs](#field-controlAttrs) | `Object` | Произвольный набор HTML-атрибутов для элемента `control`. |

## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Определяет тему оформления текстового поля. **Обязательный**.

Допустимые значения: `normal`, `websearch`.

Способ установки: `BEMJSON`, `JS`.

<a name="theme-normal"></a>

**Обычное поле (модификатор `theme` в значении `normal`)**

Используется в большинстве случаев.

```js
{
    block: 'x-table',
    head: ['normal'],
    body: [
        {
            block: 'textinput',
            mods: { theme: 'normal', size: 'm' },
            text: 'Тема normal'
        }
    ]
}
```

<a name="theme-websearch"></a>

**Текстовое поле в желтой поисковой стрелке (модификатор `theme` в значении `websearch`)**

Используется на главной странице Яндекса.

> **Важно!** Необходимо использовать c модификатором `size` в значении `false`.

```js
{
    block: 'x-table',
    head: ['websearch'],
    body: [
        {
            block: 'textinput',
            mods: { theme: 'websearch', size: false },
            text: 'Тема websearch'
        }
    ]
}
```

<a name="mods-size"></a>

#### Модификатор `size`

Определяет размер поля. **Обязательный**.

Допустимые значения: `xs`, `s`, `m`, `n`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['xs', 's', 'm'],
    body: [
        ['xs', 's', 'm'].map(function(size) {
            return {
                block: 'textinput',
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

Допустимое значение: `default`, `classic`.

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['classic', 'default'],
    body: [
        ['classic', 'default'].map((view) => {
            return {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', view: view, tone: 'default' },
                text: 'Текстовое поле'
            };
        })
    ]
}
```

<a name="mods-tone"></a>

#### Модификатор `tone`

Определяет цветовой тон блока.

Допустимые значения: `default`, `dark`, `grey`, `red`.

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['default', 'dark', 'grey', 'red'],
    body: [
        ['default', 'dark', 'grey', 'red'].map((tone) => {
            return {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', view: 'default', tone: tone },
                text: 'Текстовое поле'
            };
        })
    ]
}
```

<a name="mods-type"></a>

#### Модификатор `type`

Определяет тип текстового поля. Значение по умолчанию — `text`.

Допустимые значения: `text`, `email`, `tel`, `password`, `number`.

Способ установки: `BEMJSON`.

```js
[
    (function() {
      var textinputs = [
          { type: 'text', text: 'текст' },
          { type: 'email', text: 'lego@yandex-team.ru' },
          { type: 'tel', text: '725-12-13' },
          { type: 'password', text: '123456' },
          { type: 'number', text: 10 }
      ];

      return {
          block: 'x-table',
          head: ['text', 'email', 'tel', 'password', 'number'],
          body: textinputs.map(function(obj) {
              return {
                  block: 'textinput',
                  mods: { theme: 'normal', size: 'm', type: obj.type },
                  text: obj.text
              };
          })
      }
  })()
]
```

> **Примечание.** Модификатор `type` в значении `number` не используется совместно с [модификатором `has-clear`](#mods-has-clear) и не отображает HTML-атрибут `placeholder`.

<a name="mods-pin"></a>

#### Модификатор `pin`

Определяет форму текстового поля. Используется при группировке текстового поля с другими блоками (например, с кнопками).

Допустимые значения: `brick-brick`, `brick-clear`, `clear-brick`, `round-clear`, `clear-round`, `round-brick`, `brick-round`, `clear-clear`, `round-round`.

Допустимыми значениями модификатора являются комбинации из двух ключевых слов указанных через дефис (например, `brick-clear`). Комбинация определяет форму и границы текстового поля слева направо.

Ключевые слова:
* `clear` — нет боковой границы;
* `brick` — прямоугольная граница;
* `round` — граница со скругленными уголками.

Способ установки: `BEMJSON`, `JS`.

**Поля со скругленными уголками**

```js
[
    (function() {
        var pins = ['round-round', 'round-clear', 'clear-round', 'round-brick', 'brick-round'];

        return {
            block: 'x-table',
            head: pins,
            body: pins.map(function(pin) {
                return {
                    block: 'textinput',
                    mods: { theme: 'normal', size: 'm', pin: pin },
                    text: 'Текстовое поле'
                };
            })
        };
    })()
]
```

**Поля с прямоугольными уголками**

```js
[
    (function() {
        var pins = ['brick-brick', 'brick-clear', 'clear-brick'];

        return {
            block: 'x-table',
            head: pins,
            body: pins.map(function(pin) {
                return {
                    block: 'textinput',
                    mods: { theme: 'normal', size: 'm', pin: pin },
                    text: 'Текстовое поле'
                };
            })
        };
    })()
]
```

**Поле без боковых границ**

```js
[
    (function() {
        var pins = ['clear-clear'];

        return {
            block: 'x-table',
            head: pins,
            body: pins.map(function(pin) {
                return {
                    block: 'textinput',
                    mods: { theme: 'normal', size: 'm', pin: pin },
                    text: 'Текстовое поле'
                };
            })
        };
    })()
]
```

**Примеры группировок**

> **Примечание.** При группировке блоки должны иметь одинаковые размеры (модификатор `size`).

```js
[
    { block: 'x-title', tag: 'h3', text: 'Группировка с блоком button2' },
    [
        {
            block: 'textinput',
            mods: { theme: 'normal', size: 'm', pin: 'round-clear' },
            attrs: { style: 'width: 200px;' },
            text: 'Текстовое поле'
        },
        {
            block: 'button2',
            mods: { theme: 'action', size: 'm', pin: 'clear-round' },
            text: 'Найти'
        }
    ]
]
```

<a name="mods-poll"></a>

#### Модификатор `poll`

Отвечает за работу блока в режиме частых опросов, т.е периодические запросы: «эй, я тут, изменилось ли что-нибудь?».

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

> **Примечание.** Создает дополнительный трафик.

```js
[
    {
        block: 'x-table',
        head: ['_poll'],
        body: [
            {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', poll: 'yes' },
                text: 'Текстовое поле'
            },
            {
                block: 'x-deps',
                content: [
                    { block: 'textinput', mods: { poll: 'yes' } }
                ]
            }
        ]
    }
]
```

<a name="mods-has-clear"></a>

#### Модификатор `has-clear`

Добавляет крестик для очистки текстового поля.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['_has-clear'],
        body: [
            {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', 'has-clear': 'yes' },
                text: 'Текстовое поле с крестиком'
            },
            {
                block: 'x-deps',
                content: [
                  { block: 'textinput', elem: 'clear', mods: { theme: 'normal' } }
              ]
            }
        ]
    }
]
```

<a name="mods-has-icon"></a>

#### Модификатор `has-icon`

Позволяет использовать иконки в текстовое поле.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

> **Примечание.** Используется с полями: [icon](#field-icon), [iconLeft](#field-iconleft), [iconRight](#field-iconright).

```js
[
    {
        block: 'x-table',
        head: ['icon', 'iconLeft', 'iconRight'],
        body: [
            {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', 'has-icon': 'yes' },
                icon: { mods: { type: 'lock' } },
                text: 'Текстовое поле'
            },
            {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', 'has-icon': 'yes' },
                iconLeft: { mods: { type: 'lock' } },
                text: 'Текстовое поле'
            },
            {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', 'has-icon': 'yes' },
                iconRight: { mods: { type: 'lock' } },
                text: 'Текстовое поле'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'textinput', mods: { 'has-icon': 'yes' } },
            { block: 'icon', mods: { type: 'lock' } }
        ]
    }
]
```

<a name="mods-has-nameplate"></a>

#### Модификатор `has-nameplate`

Позволяет использовать метку сервиса рядом с текстовым полем. **Устаревший**.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

> **Примечание.** Необходимо использовать с блоком [nameplate](../nameplate/nameplate.ru.md).

```js
[
    {
        block: 'nameplate',
        name: 'market',
        url: 'http://market.yandex.ru'
    },
    {
        block: 'textinput',
        id: 'market',
        mods: { theme: 'normal', size: 'm', 'has-nameplate': 'yes' },
        text: 'Текстовое поле'
    },
    {
        block: 'x-deps',
        content: [
            { block: 'textinput', mods: { 'has-nameplate': 'yes' } },
            { block: 'nameplate' }
        ]
    }
]
```

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Определяет неактивное состояние, при котором текстовое поле становится недоступно для действий пользователя.

С включенным модификатором `disabled` невозможно:

* установить модификаторы `focused`, `pressed` и `hovered` (существующие удаляются);
* вызвать БЭМ-события.

> **Примечание.** Неактивное состояние блока возможно менять программно.

Допустимое значение: `yes`.

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['_disabled'],
    body: [
        {
            block: 'textinput',
            mods: { theme: 'normal', size: 'm', disabled: 'yes' },
            text: 'Текстовое поле'
        }
    ]
}
```

<a name="mods-focused"></a>

#### Модификатор `focused`

Устанавливает фокус на блоке. Если блок получил фокус, то выставляется автоматически.

Допустимое значение: `yes`.

Способы установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['_focused'],
        body: [
            {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', focused: 'yes'  },
                text: 'Текстовое поле в фокусе'
            }
        ]
    }
]
```

<a name="mods-hovered"></a>

#### Модификатор `hovered`

Определяет действие блока при наведении на него курсором. Выставляется автоматически.

Допустимое значение: `yes`.

Способы установки: `—`.

<a name="mods-baseline"></a>

#### Модификатор `baseline`

Выравнивает текстовое поле по базовой линии.

Допустимое значение: `yes`.

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['_baseline'],
    body: [
        {
            block: 'textinput',
            mods: { theme: 'normal', size: 'm', baseline: 'yes', view: 'classic' },
            text: 'Текстовое поле'
        }
    ]
}
```

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
            block: 'textinput',
            mods: { theme: 'normal', size: 'm' },
            text: 'Текстовое поле' // Переданное значение экранируется автоматически
        }
    ]
}
```

<a name="field-icon"></a>

#### Поле `icon`

Определяет иконку, которая отображается в текстовом поле. Иконка задается с помощью блока [icon](../icon/icon.ru.md).

Тип: `BEMJSON`.

> **Важно!** Необходимо использовать с модификатором [has-icon](#mods-has-icon).

```js
[
    {
        block: 'x-table',
        head: ['Поле icon'],
        body: [
            {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', 'has-icon': 'yes' },
                icon: {
                    // block: 'icon' можно не указывать
                    mods: { type: 'lock' }
                },
                text: 'Текстовое поле'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'textinput', mods: { 'has-icon': 'yes' } },
            { block: 'icon', mods: { type: 'lock' } }
        ]
    }
]
```

<a name="field-iconleft"></a>

#### Поле `iconLeft`

Определяет иконку, которая отображается слева от содержимого текстового поля. Иконка задается с помощью блока [icon](../icon/icon.ru.md).

Тип: `BEMJSON`.

> **Важно!** Необходимо использовать с модификатором [has-icon](#mods-has-icon).

```js
[
    {
        block: 'x-table',
        head: ['Поле iconLeft'],
        body: [
            {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', 'has-icon': 'yes' },
                iconLeft: {
                    // block: 'icon' указывать не нужно
                    mods: { type: 'lock' }
                },
                text: 'Текстовое поле'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'textinput', mods: { 'has-icon': 'yes' } },
            { block: 'icon', mods: { type: 'lock' } }
        ]
    }
]
```

<a name="field-iconright"></a>

#### Поле `iconRight`

Определяет иконку, которая отображается справа от содержимого текстового поля. Иконка задается с помощью блока [icon](../icon/icon.ru.md).

Тип: `BEMJSON`.

> **Важно!** Необходимо использовать с модификатором [has-icon](#mods-has-icon).

```js
[
    {
        block: 'x-table',
        head: ['Поле iconRight'],
        body: [
            {
                block: 'textinput',
                mods: { theme: 'normal', size: 'm', 'has-icon': 'yes' },
                iconRight: {
                    // block: 'icon' указывать не нужно
                    mods: { type: 'lock' }
                },
                text: 'Текстовое поле'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'textinput', mods: { 'has-icon': 'yes' } },
            { block: 'icon', mods: { type: 'lock' } }
        ]
    }
]
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
            block: 'textinput',
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
            block: 'textinput',
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
            block: 'textinput',
            mods: { theme: 'normal', size: 'm' },
            autocomplete: false,
            text: 'Текстовое поле'
        }
    ]
}
```

<a name="field-id"></a>

#### Поле `id`

Определяет уникальный идентификатор текстового поля, выставляется элементу `control`.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле id'],
    body: [
        {
            block: 'textinput',
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
            block: 'textinput',
            mods: { theme: 'normal', size: 'm' },
            tabindex: 2,
            text: 'tabindex: 2'
        },
        {
            block: 'textinput',
            mods: { theme: 'normal', size: 'm' },
            tabindex: 1,
            text: 'tabindex: 1'
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
            block: 'textinput',
            mods: { theme: 'normal', size: 'm' },
            controlAttrs: { autofocus: true },
            text: 'Текстовое поле c автофокусом'
        }
    ]
}
```
