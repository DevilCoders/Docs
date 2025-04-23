# radio-button

Используется для создания группы радиопереключателей в виде кнопок.

> **Примечание.** Для MSIE < 8 радиопереключатели деградируют до нативных переключателей `<input name="имя" type="radio" атрибуты>`.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [theme](#mods-theme) (req)| `normal`, `pseudo` | `BEMJSON`, `JS` | Стилевое оформление. |
| [size](#mods-size) (req) | `xs`, `s`, `m`, `n`, `l`, `head` | `BEMJSON`, `JS` | Размер радиопереключателей. |
| [view](#mods-view) | `classic`, `default` | `BEMJSON`, `JS` | Вид радиогруппы. |
| [tone](#mods-tone) | `default`, `dark`, `grey`, `red` | `BEMJSON`, `JS` | Цветовой тон кнопочной радиогруппы. |
| [side](#mods-side) | `left`, `right`, `both` | `BEMJSON`, `JS` | Скругление углов радиогруппы. |
| [disabled](#mods-disabled) |`yes` |`BEMJSON`, `JS` | Неактивное состояние радиогруппы. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [name](#field-name) | `BEMJSON`, `JS` | Уникальное имя радиогруппы. |
| [value](#field-value) | `BEMJSON`, `JS` | Значение заранее выбранного радиопереключателя. |
| [freeWidth](#field-freewidth) | `BEMJSON`, `JS` | Разрешить разную ширину радиопереключателям, у которых модификатор `view` в значении `default`. |

## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Отвечает за стилевое оформление кнопки. **Обязательный**.

Допустимое значение: `normal`, `pseudo`.

Способ установки: `BEMJSON`.

```js
{
    block: 'x-area',
    attrs: { style: 'background: #C9DCF6;' },
    content: [
        {
            block: 'x-table',
            head: ['normal', 'pseudo'],
            body: [
                ['normal', 'pseudo'].map((theme) => {
                    return {
                        block: 'radio-button',
                        mods: { theme: theme, size: 'm', view: 'classic' },
                        value: 'yes',
                        content: [
                            {
                                elem: 'radio',
                                controlAttrs: { value: 'yes' },
                                content: 'Да'
                            },
                            {
                                elem: 'radio',
                                controlAttrs: { value: 'no' },
                                content: 'Нет'
                            }
                        ]
                    };
                })
            ]
        }
    ]
}
```

<a name="mods-size"></a>

#### Модификатора `size`

Определяет размер радиопереключателей. **Обязательный**.

Способ установки: `BEMJSON`.

Допустимые значения: `хs`, `s`, `m`, `n`, `l`, `head`.

> **Примечание.** Размер `head` экспериментальный, доступен на уровне `desktop`. Используется в шапке.

```js
{
    block: 'x-table',
    head: ['xs', 's', 'm', 'n', 'l', 'head'],
    body: [
        ['xs', 's', 'm', 'n', 'l', 'head'].map((size) => {
            return {
                block: 'radio-button',
                mods: { theme: 'normal', size: size, view: 'classic' },
                value: 'yes',
                content: [
                    {
                        elem: 'radio',
                        controlAttrs: { value: 'yes' },
                        content: 'Да'
                    },
                    {
                        elem: 'radio',
                        controlAttrs: { value: 'no' },
                        content: 'Нет'
                    }
                ]
            };
        })
    ]
}
```

<a name="mods-tone"></a>

#### Модификатор `tone`

Определяет цветовой тон радиогруппы.

Допустимое значение: `default`, `dark`, `grey`, `red`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['default', 'dark', 'grey', 'red'],
    body: [
        ['default', 'dark', 'grey', 'red'].map((tone) => {
            return {
                block: 'radio-button',
                mods: { theme: 'normal', size: 'm', view: 'default', tone: tone },
                value: 'yes',
                content: [
                    {
                        elem: 'radio',
                        controlAttrs: { value: 'yes' },
                        content: 'Да'
                    },
                    {
                        elem: 'radio',
                        controlAttrs: { value: 'no' },
                        content: 'Нет'
                    }
                ]
            };
        })
    ]
}
```

<a name="mods-view"></a>

#### Модификатор `view`

Определяет внешний вид радиогруппы.

Допустимое значение: `classic`, `default`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['classic', 'default'],
    body: [
        ['classic', 'default'].map((view) => {
            return {
                block: 'radio-button',
                mods: { theme: 'normal', size: 'm', view: view, tone: 'default' },
                value: 'yes',
                content: [
                    {
                        elem: 'radio',
                        controlAttrs: { value: 'yes' },
                        content: 'Да'
                    },
                    {
                        elem: 'radio',
                        controlAttrs: { value: 'no' },
                        content: 'Нет'
                    }
                ]
            };
        })
    ]
}
```

<a name="mods-side"></a>

#### Модификатор `side`

Определяет скругление углов радиогруппы.

Допустимые значения | Описание
--- | ---
`left` | Скругляет левый угол крайней левой радиокнопки.
`right` | Скругляет правый угол крайней правой радиокнопки.
`both` |  Скругляет углы всех радиокнопок с двух сторон.

Способ установки:  `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['left', 'right', 'both'],
    body: [
        ['left', 'right', 'both'].map((side) => {
            return {
                block: 'radio-button',
                mods: { theme: 'normal', size: 'm' },
                value: 'yes',
                content: [
                    {
                        elem: 'radio',
                        side: side,
                        controlAttrs: { value: 'yes' },
                        content: 'Да'
                    },
                    {
                        elem: 'radio',
                        side: side ,
                        controlAttrs: { value: 'no' },
                        content: 'Нет'
                    },
                    {
                        elem: 'radio',
                        side: side ,
                        controlAttrs: { value: 'probably' },
                        content: 'Наверное'
                    }
                ]
            };
        })
    ]
}
```

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Определяет неактивное состояние радиогруппы.

Допустимое значение: `yes`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['_disabled'],
    body: [
        {
            block: 'radio-button',
            mods: { theme: 'normal', size: 'm', view: 'classic', disabled: 'yes' },
            value: 'yes',
            content: [
                {
                    elem: 'radio',
                    controlAttrs: { value: 'yes' },
                    content: 'Да'
                },
                {
                    elem: 'radio',
                    controlAttrs: { value: 'no' },
                    content: 'Нет'
                }
            ]
        }
    ]
}
```

### Поля блока

<a name="field-name"></a>

#### Поле `name`

Определяет уникальное имя радиогруппы. По умолчанию устанавливает такое же имя всем радиопереключателям в группе.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле name'],
    body: [
        {
            block: 'radio-button',
            mods: { theme: 'normal', size: 'm', view: 'classic' },
            value: 'yes',
            name: 'my-radio-button',
            content: [
                {
                    elem: 'radio',
                    controlAttrs: { value: 'yes' },
                    content: 'Да'
                },
                {
                    elem: 'radio',
                    controlAttrs: { value: 'no' },
                    content: 'Нет'
                }
            ]
        }
    ]
}
```

<a name="field-value"></a>

#### Поле `value`

Определяет значение радиопереключателя, который будет заранее выбран в группе. Должно совпадать со значением `value` поля `controlAttrs` этого радиопереключателя.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле value: yes', 'Поле value: no'],
    body: [
        ['yes', 'no'].map((value) => {
            return {
                block: 'radio-button',
                mods: { theme: 'normal', size: 'm', view: 'classic' },
                value: value,
                content: [
                    {
                        elem: 'radio',
                        controlAttrs: { value: 'yes' },
                        content: 'Да'
                    },
                    {
                        elem: 'radio',
                        controlAttrs: { value: 'no' },
                        content: 'Нет'
                    }
                ]
            };
        })
    ]
}
```

<a name="field-freewidth"></a>

#### Поле `freeWidth`

Разрешает задать разную ширину радиопереключателям, у которых модификатор `view` в значении `default`.

Тип: `BEMJSON`.

```js
{
    block: 'x-table',
    head: ['Поле freeWidth'],
    body: [
        {
            block: 'radio-button',
            mods: { theme: 'normal', size: 'm', view: 'default', tone: 'default' },
            value: 'yes',
            freeWidth: true,
            content: [
                {
                    elem: 'radio',
                    controlAttrs: { value: 'yes' },
                    content: 'Да'
                },
                {
                    elem: 'radio',
                    controlAttrs: { value: 'no' },
                    content: 'Нет'
                }
            ]
        }
    ]
}
```
