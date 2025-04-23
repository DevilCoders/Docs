# checkbox

Используется для создания различных типов переключателей.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [theme](#mods-theme) (req) | `'normal'`, `'pseudo'` | `BEMJSON`, `JS` | Стилевое оформление. |
| [size](#mods-size) (req) | `'s'`, `'m'` | `BEMJSON`, `JS` | Размер переключателя. |
| [checked](#mods-checked) | `'yes'` | `BEMJSON`, `JS` | Переключатель в значении «включен». |
| [disabled](#mods-disabled) | `'yes'` | `BEMJSON`, `JS` | Неактивное состояние. |
| [focused](#mods-focused) | `'yes'` | `BEMJSON`, `JS` | Фокус на блоке. |
| [pressed](#mods-pressed) | `'yes'` | — | Нажатие на переключатель. |
| [hovered](#mods-hovered) | `'yes'` | — | Наведение на переключатель курсором. |
| [lines](#mods-lines) | `'one'`, `'multi'`, `false` | — | Поддержка однострочных или многострочных подписей. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [text](#field-text) | `String`, `Number` | Текст подписи к переключателю. |
| [box](#field-box) | `BEMJSON` | Содержимое элемента [box](#elem-box). |
| [content](#field-content) | `BEMJSON` | Содержимое переключателя. Используется для формирования произвольной HTML-разметки, с помощью [элементов блока](#elems). Переопределяет значения заданные в полях `text`, `box`, `control`. |
| [control](#field-control) | `BEMJSON` | Содержимое элемента [control](#elem-control). |
| [tabindex](#field-tabindex) | `Number` | Последовательность перехода между контролами при нажатии на `Tab`. |
| [controlAttrs](#field-controlattrs) | `Object` | Произвольный набор HTML-атрибутов для элемента [control](#elem-control). |

<a name="elems"></a>

### Элементы блока

| Элемент | Описание |
| ------- | -------- |
| [box](#elem-box) | Контейнер для переключателя. Нативный элемент управления `INPUT type="checkbox"` скрыт. |
| [control](#elem-control) | Вспомогательный элемент, позволяющий использовать функциональность нативного элемента управления `INPUT type="checkbox"`. |
| [label](#elem-label) | Текст подписи к переключателю. |
| [tick](#elem-tick) | Галочка. |

## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Отвечает за стилевое оформление.

Допустимое значение: `'normal'`, `'pseudo'`.

Способ установки: `BEMJSON`, `JS`.

<a name="theme-normal"></a>

**Обычный переключатель (модификатор `theme` в значении `normal`)**

Используется в большинстве случаев.

```js
[
    {
        block: 'x-table',
        head: ['normal'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                text: 'checkbox'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

<a name="theme-pseudo"></a>

**Псевдопереключатель (модификатор `theme` в значении `pseudo`)**

Используется для изменения внешнего вида блока при необходимости сделать переключатель менее заметным на странице.

```js
[
    {
        block: 'x-area',
        attrs: { style: 'background: #ddd;' },
        content: [
            {
                block: 'x-table',
                head: ['normal', 'pseudo'],
                body: [
                    ['normal', 'pseudo'].map(function(theme) {
                        return {
                            block: 'checkbox',
                            mods: { theme: theme, size: 'm' },
                            text: 'checkbox'
                        };
                    })
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

<a name="mods-size"></a>

#### Модификатор `size`

Задает размер переключателю.

Допустимые значения: `'s'`, `'m'`.

Способ установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['s', 'm'],
        body: [
            ['s', 'm'].map(function(size) {
                return {
                    block: 'checkbox',
                    mods: { theme: 'normal', size: size },
                    text: 'Размер ' + size
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

<a name="mods-checked"></a>

#### Модификатор `checked`

Отвечает за состояние переключатель «включен».

Допустимые значения: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['_checked'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm', checked: 'yes' },
                text: 'checkbox'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Отвечает за неактивное состояние, при котором блок виден, но недоступен для действий пользователя.

Нельзя:

* установить модификаторы `focused`, `pressed` и `hovered` (существующие удаляются);
* вызвать БЭМ-события.

> **Примечание.** Блок может находится сразу в двух состояниях: `disabled` и `checked`. Неактивное состояние блока можно изменять программно.

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

```js
[
  (function() {
      var state = [
        { disabled: 'yes', checked: false },
        { disabled: 'yes', checked: 'yes' }
      ];

    return [
        {
            block: 'x-table',
            head: ['_disabled', '_disabled + _checked'],
            body: state.map(function(obj) {
                return {
                    block: 'checkbox',
                    mods: { theme: 'normal', size: 'm', disabled: obj.disabled,  checked: obj.checked },
                    text: 'checkbox'
                };
            })
        },
        {
          block: 'x-deps',
          content: [
              { block: 'checkbox', elem: 'label' }
          ]
        }
    ];

  })()
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
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm', focused: 'yes' },
                text: 'checkbox'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' },
            { block: 'checkbox', mods: { focused: 'yes' } }
        ]
    }
]
```

<a name="mods-pressed"></a>

#### Модификатор `pressed`

Определяет действие «нажатие на переключатель».

Допустимое значение: `yes`.

Способы установки: `—`.

Выставляется автоматически.

<a name="mods-hovered"></a>

#### Модификатор `hovered`

Определяет действие «наведение на блок курсором».

Допустимое значение: `yes`.

Способы установки: `—`.

Выставляется автоматически.

<a name="mods-lines"></a>

#### Модификатор `lines`

Задает тип подписи.

Допустимые значения: `'one'`, `'multi'`, `false`.

Способ установки: `BEMJSON`.

> **Примечание.** Значение по умолчанию: `multi`. Отключается по значению `false`.

**Модификатор `lines` в значении `one`.**

Используется для создания чекбокса с однострочной подписью, которая обрезается троеточием, если ее длина превышает длину родительского элемента.

```js
[
    {
        block: 'x-table',
        head: ['_lines_one'],
        body: [
            {
                block: 'x-area',
                mods: { resizable: 'yes', bordered: 'yes' },
                content:
                    {
                        block: 'checkbox',
                        mods: { theme: 'normal', size: 'm', lines: 'one' },
                        text: 'Длинный текст обрезается троеточием'
                    }

            }
        ]
    },
    {
      block: 'x-deps',
      content: [
          { block: 'checkbox', elem: 'label', mods: { lines: 'one' } },
      ]
    }
]
```

**Модификатор `lines` в значении `multi`.**

Используется для создания чекбокса с многострочной подписью. Устанавливает CSS-свойство `display: inline-table`.

```js
[
    {
        block: 'x-table',
        head: ['_lines_multi'],
        body: [
            {
                block: 'checkbox',
                attrs: {style: 'width: 220px'},
                mods: { theme: 'normal', size: 'm', lines: 'multi' },
                text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce in accumsan augue. Nullam tincidunt ullamcorper nisl, sed efficitur sem pellentesque mattis.'
            }
        ]
    },
    {
      block: 'x-deps',
      content: [
          { block: 'checkbox', elem: 'label' }
      ]
    }
]
```

**Модификатор `lines` в значении `false`.**

Используется для отключения модификатора `lines`. Устанавливает CSS-свойство `display: inline`.

```js
[
    {
        block: 'x-table',
        head: ['_lines_false'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm', lines: false },
                text: 'inline-чекбокс'
            },
            {
                block: 'icon',
                mods: { type: 'camera' }
            }
        ]
    },
    {
      block: 'x-deps',
      content: [
          { block: 'checkbox', elem: 'label' },
          { block: 'icon', mods: { type: 'camera' } }
      ]
    }
]
```

### Поля блока

<a name="field-text"></a>

#### Поле `text`

Определяет текст подписи к переключателю.

Тип: `String`, `Number`.

```js
[
    {
        block: 'x-table',
        head: ['Поле text'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                text: 'checkbox' // Переданное значение экранируется автоматически
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

> **Примечание.** Переданное значение экранируется автоматически.

<a name="field-box"></a>

#### Поле `box`

Определяет содержимое элемента [box](#elem-box). Используется для доопределения блока или для формирования произвольной HTML-разметки.

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле box'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                box: {
                      attrs: { name: 'the-box' },
                      content: [
                          {
                              elem: 'control'
                          },
                          {
                              elem: 'tick'
                          },
                          {
                              elem: 'tootsi-pootsi'
                          }
                      ]
                },
                text: 'checkbox'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

<a name="field-content"></a>

#### Поле `content`

Определяет содержимое переключателя. Используется для формирования произвольной HTML-разметки.

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле content'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                content:  [
                    {
                        elem: 'box',
                        attrs: { style: 'margin-top: 6px;' },
                        content: [
                            {
                                elem: 'control'
                            },
                            {
                                elem: 'tick'
                            }
                        ]
                    },
                    {
                        elem: 'label',
                        content: [
                            {
                                block: 'logo',
                                attrs: { style: 'display: table-cell;' },
                                mods: {
                                    name: 'ys-ru-64x27'
                                }
                            }
                        ]
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

> **Важно!** Переопределяет значения заданные в полях `text`, `box`, `control`.

<a name="field-control"></a>

#### Поле `control`

Определяет содержимое элемента [control](#elem-control). Используется для доопределения блока или для формирования произвольной HTML-разметки.

Тип: `BEMJSON`.

```js
[
    {
        block: 'x-table',
        head: ['Поле control'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                control: {
                    attrs: { name: 'the-control' }
                },
                text: 'checkbox'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

<a name="field-tabindex"></a>

#### Поле `tabIndex`

Определяет последовательность перехода между контролами при нажатии на `Tab`.

Тип: `Number`.

```js
[
    {
        block: 'x-table',
        head: ['Поле tabIndex'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                tabIndex: 1,
                text: 'checkbox'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

<a name="field-controlattrs"></a>

#### Поле `controlAttrs`

Определяет произвольный набор HTML-атрибутов для элемента [control](#elem-control).

Тип: `Object`.

```js
[
    {
        block: 'x-table',
        head: ['Поле controlAttrs'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                controlAttrs: { autofocus: true, id: 'the-id', name: 'the-name', value: 'the-value' },
                text: 'checkbox'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

### Элементы блока

<a name="elem-box"></a>

#### Элемент `box`

Контейнер для переключателя.

```js
[
    {
        block: 'x-table',
        head: ['__box'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                content:  [
                    {
                        elem: 'box',
                        content: [
                            {
                                elem: 'control'
                            },
                            {
                                elem: 'tick'
                            }
                        ]
                    },
                    {
                        elem: 'label',
                        content: 'checkbox'
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

> **Примечание.** Используется для самостоятельной настройки параметров блока.

<a name="elem-control"></a>

#### Элемент `control`

Вспомогательный элемент, позволяющий использовать функциональность нативного элемента управления `INPUT type="checkbox"`.

```js
[
    {
        block: 'x-table',
        head: ['__control'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                content:  [
                    {
                        elem: 'box',
                        content: [
                            {
                                elem: 'control'
                            },
                            {
                                elem: 'tick'
                            }
                        ]
                    },
                    {
                        elem: 'label',
                        content: 'checkbox'
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

> **Примечание.** Используется для самостоятельной настройки параметров блока.

<a name="elem-label"></a>

#### Элемент `label`

Текст подписи к переключателю.

```js
[
    {
        block: 'x-table',
        head: ['__label'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                content:  [
                    {
                        elem: 'box',
                        content: [
                            {
                                elem: 'control'
                            },
                            {
                                elem: 'tick'
                            }
                        ]
                    },
                    {
                        elem: 'label',
                        content: 'checkbox'
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

> **Примечание.** Используется для самостоятельной настройки параметров блока.

<a name="elem-tick"></a>

#### Элемент `tick`

Галочка переключателя.

```js
[
    {
        block: 'x-table',
        head: ['__tick'],
        body: [
            {
                block: 'checkbox',
                mods: { theme: 'normal', size: 'm' },
                content:  [
                    {
                        elem: 'box',
                        content: [
                            {
                                elem: 'control'
                            },
                            {
                                elem: 'tick'
                            }
                        ]
                    },
                    {
                        elem: 'label',
                        content: 'checkbox'
                    }
                ]
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'checkbox', elem: 'label' }
        ]
    }
]
```

> **Примечание.** Используется для самостоятельной настройки параметров блока.
