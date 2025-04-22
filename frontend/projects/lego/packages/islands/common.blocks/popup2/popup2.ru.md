# popup2

Используется для создания всплывающих окон.

## Обзор

### Модификаторы блока

|Модификатор | Допустимые значения | Способы установки | Описание |
| -----------| --------------------| ------------------| ---------|
| [theme](#mods-teme) | `normal`, `clear` | BEMJSON | Стилевое оформление блока. |
| [tone](#mods-tone)| `default`, `dark`, `grey`, `red`, `market` | BEMJSON | Цветовой тон блока. |
| [view](#mods-view)| `default`, `classic` | BEMJSON | Внешний вид блока. |
| [target](#mods-target)| `anchor`, `position` | BEMJSON | Точка открытия всплывающего окна. |
| [hiding](#mods-hiding)| `yes`, `false` | BEMJSON | Логика поведения блока внутри родительского контейнера со свойством `overflow: auto` или `overflow: scroll`. |
| [autoclosable](#mods-autoclosable)| `yes` | BEMJSON | Закрытие всплывающего окна при нажатии за его пределами или по клавише **Escape**. |
| [motionless](#mods-motionless)| `yes` | BEMJSON | Закрепить положение всплывающего окна после открытия. |
| [nonvisual](#mods-nonvisual)| `yes` | BEMJSON | Отключает визуальные стили блока. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание  |
| ---- | --- | --------- |
| [directions](#field-direction) | `String` | Задает направление относительно объекта открытия (цели), по которому раскрывается всплывающее окно. |
| [mainOffset](#field-mainoffset) | `Number` | Смещение в пикселях всплывающего окна относительно основного направления. Используется только с модификатором `target`. |
| [secondaryOffset](#field-secondaryoffset) | `Number` | Смещение всплывающего окна относительно [второстепенного направления](#sub-directions). Используется только с модификатором `target`. |
| [viewportOffset](#field-viewportoffset) | `Number` | Отступ блока от края окна браузера. Используется только с модификатором `target`.|
| [hasTail](#field-hastail) | `Boolean` | Наличие «хвостика». |
| [tailSize](#field-tailsize) | `Number` | Размер «хвостика». |
| [tailOffset](#field-tailoffset) | `Number` | Отступ «хвостика» от края всплывающего окна. |
| [zIndexGroupLevel](#z-index) | `Number` | Задает уровень слоев `z-index` для открывающихся всплывающих окон. |

## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Отвечает за стилевое оформление блока.

Способы установки: `BEMJSON`.

| Допустимые значения | Описание |
| ------------------- | -------- |
| `normal` | Стандартное оформление блока в стиле «Острова». Содержит анимацию открытия/закрытия и добавляет параметры `mainOffset=5` и `viewportOffset=5`.|
| `clear` | Блок без рамки. Выставляет для открытого блока `popup2` свойство `display: block`. Отсутствует анимация открытия/закрытия. На основе этой темы можно реализовать собственный стиль оформления.  |

```js
[
    {
        block: 'popup-open',
        content: [
            {
                block: 'button2',
                mods: {theme: 'normal', size: 's'},
                text: 'Открыть (normal)'
            },
            {
                block: 'popup2',
                mods: {target: 'anchor', theme: 'normal', autoclosable: 'yes'},
                content: 'Попап с темой normal'
            }
        ]
    },
    {
        block: 'popup-open',
        content: [
            {
                block: 'button2',
                mods: {theme: 'normal', size: 's'},
                text: 'Открыть (clear)'
            },
            {
                block: 'popup2',
                mods: {target: 'anchor', theme: 'clear', autoclosable: 'yes'},
                content: 'Попап с темой clear'
            }
        ]
    }
]
```

<a name="mods-tone"></a>

#### Модификатор `tone`

Задает цветовой тон блока.

Допустимые значения: `default`, `red`, `grey`, `dark`, `market`.

Способ установки: `BEMJSON`.

```js
{
    block: 'x-table',
    head: ['default', 'red', 'grey', 'dark', 'market'],
    body: [
        ['default', 'red', 'grey', 'dark', 'market'].map((tone) => {
            return {
                block: 'popup-open',
                content: [
                    {
                        block: 'button2',
                        mods: { theme: 'normal', size: 'm', view: 'default', tone: tone },
                        text: 'Открыть'
                    },
                    {
                        block: 'popup2',
                        mods: { target: 'anchor', theme: 'normal', autoclosable: 'yes', view: 'default', tone: tone },
                        content: 'Попап с _tone_' + tone + '.'
                    }
                ]
            };
        })
    ]
}
```

<a name="mods-view"></a>

#### Модификатор `view`

Задает внешний вид блока.

Допустимые значения: `default`, `classic`.

Способ установки: `BEMJSON`.

```js
{
    block: 'x-table',
    head: ['default', 'classic'],
    body: [
        ['default', 'classic'].map((view) => {
            return {
                block: 'popup-open',
                content: [
                    {
                        block: 'button2',
                        mods: { theme: 'normal', size: 'm', view: view, tone: 'default' },
                        text: 'Открыть'
                    },
                    {
                        block: 'popup2',
                        mods: { target: 'anchor', theme: 'normal', autoclosable: 'yes', view: view, tone: 'default' },
                        content: 'Попап с _view_' + view + '.'
                    }
                ]
            };
        })
    ]
}
```

<a name="mods-target"></a>

#### Модификатор `target`

Определяет на странице объект (цель) в качестве точки открытия всплывающего окна.

| Допустимые значения | Описание |
| ------------------- | -------- |
| `anchor` | Позиционирование блока относительно DOM-элемента. Цель задается с помощью метода `setAnchor()`, который принимает в качестве аргумента DOM-элемент или БЭМ-блок.
| `position` | Позиционирование блока относительно координат страницы. Цель задается с помощью метода `setPosition()`, который принимает в качестве аргументов горизонтальную и вертикальную координаты.|

Способы установки: `BEMJSON`.

```js
var anchoredPopup = this.findBlockInside({block: 'popup2', modName: 'target', modVal: 'anchor'});
anchoredPopup.setAnchor(domElem);
anchoredPopup.setMod('visible', 'yes'); // откроет попап относительно domElem
anchoredPopup.delMod('visible'); // закроет попап

var positionedPopup = this.findBlockInside({block: 'popup2', modName: 'target', modVal: 'position'});
positionedPopup.setPosition(10, 20);
positionedPopup.setMod('visible', 'yes'); // откроет попап в координатах (10, 20)
positionedPopup.delMod('visible'); // закроет попап
```

```js
[
    {
        block: 'popup-open',
        content: [
            {
                block: 'button2',
                mods: {theme: 'normal', size: 's'},
                text: 'Открыть (anchor)'
            },
            {
                block: 'popup2',
                mods: {target: 'anchor', theme: 'normal', autoclosable: 'yes'},
                content: 'Попап привязан к кнопке'
            }
        ]
    },
    {
        block: 'popup-open',
        js: {position: [120, 60]},
        content: [
            {
                block: 'button2',
                mods: {theme: 'normal', size: 's'},
                text: 'Открыть (position)'
            },
            {
                block: 'popup2',
                mods: {target: 'position', theme: 'normal', autoclosable: 'yes'},
                content: 'Попап спозиционирован в точке (120;60). Однако по вертикали<br> ' +
                'он имеет координату 65px вместо 60px, это происходит т.к. по умолчанию для<br>' +
                'темы normal mainOffset=5. Если этот эффект нежелателен, просто обнулите <br>смещение в памаретрах.'
            }
        ]
    }
]
```

<a name="mods-hiding"></a>

#### Модификатор `hiding`

Отвечает за поведение блока внутри родительского контейнера со свойством `overflow: auto|scroll`. В значении `yes` должен использоваться с модификатором `target: anchor`. Во включенном состоянии добавляет для блока логику, при которой он отслеживает

Допустимые значения: `yes`, `false`.

Способ установки: `BEMJSON`.

В значении `yes` добавляет блоку логику, позволяющую следить за поведением скроллящегося родителя, в том числе в случае вложенных попапов.

```js
[
    {
        block: 'example',
        mods: {scrollable: 'yes'},
        attrs: {style: 'height: 300px; overflow-y: auto; border:1px solid #000;'},
        content: {
            block: 'example',
            attrs: {style: 'height: 500px;'},
            content:     {
                block: 'popup-open',
                content: [
                    {
                        block: 'button2',
                        mods: {theme: 'normal', size: 's'},
                        text: 'Открыть попап'
                    },
                    {
                        block: 'popup2',
                        mods: {
                            hiding: 'yes',
                            theme: 'normal',
                            target: 'anchor',
                            autoclosable: 'yes'
                        },
                        content: 'Попап'
                    }
                ]
            }
        }
    }
]
```

<a name="mods-autoclosable"></a>

#### Модификатор `autoclosable`

Отвечает за закрытие всплывающего окна при нажатии за его пределами или по клавише **Escape**. По клавише **Escape** блоки закрываются в порядке, обратном порядку открытия.

Допустимое значение: `yes`.

Способы установки: `BEMJSON`.

```js
{
    block: 'popup-open',
    content: [
        {
            block: 'button2',
            mods: {theme: 'normal', size: 's'},
            text: 'Открыть'
        },
        {
            block: 'popup2',
            mods: {target: 'anchor', theme: 'normal', autoclosable: 'yes'},
            content: {
                block: 'popup-open',
                attrs: {style: 'padding: 16px'},
                content: [
                    {
                        block: 'button2',
                        mods: {theme: 'normal', size: 's'},
                        text: 'Еще Открыть'
                    },
                    {
                        block: 'popup2',
                        mods: {target: 'anchor', theme: 'normal', autoclosable: 'yes'},
                        content: 'Привет! Нажми ESC'
                    }
                ]
            }
        }
    ]
}
```

<a name="mods-motionless"></a>

#### Модификатор `motionless`

Закрепить положение всплывающего окна после открытия. Открыв окно в одном из направлений, направление закрепится и не будет меняться при прокрутке страницы. Чтобы изменить положение всплывающего окна, его необходимо закрыть и открыть заново.

Допустимое значение: `yes`.

Способы установки: `BEMJSON`.

```js
{
    block: 'popup-open',
    content: [
        {
            block: 'button2',
            mods: {theme: 'normal', size: 's'},
            text: 'Открыть'
        },
        {
            block: 'popup2',
            mods: {target: 'anchor', theme: 'normal', motionless: 'yes'},
            content: 'Привет'
        }
    ]
}
```

<a name="mods-nonvisual"></a>

#### Модификатор `nonvisual`

Отключает визуальные стили всплывающего окна (например, границы и тень).

Допустимое значение: `yes`.

Способы установки: `BEMJSON`.

```js
{
    block: 'popup-open',
    content: [
        {
            block: 'button2',
            mods: {theme: 'normal', size: 's'},
            text: 'Открыть'
        },
        {
            block: 'popup2',
            mods: {target: 'anchor', theme: 'normal', nonvisual: 'yes'},
            content: 'Привет'
        }
    ]
}
```

### Поля блока

<a name="field-direction"></a>

#### Поле `directions`

Задает направление относительно объекта открытия (цели), по которому раскрывается всплывающее окно. По умолчанию содержит все 12 допустимых направлений. Используется только для всплывающих окон с модификатором `target`.

Расположение блока определяется автоматически, исходя из массива допустимых направлений (в порядке приоритета) и положения точки открытия на странице. У всех допустимых направлений есть основной и второстепенный параметры. Например, для направления `bottom-left` параметр `bottom` является основным, а `left` — второстепенным.

Для управления расположением всплывающего окна необходимо указать массив направлений открытия. При этом из значений массива будет выбрано наиболее подходящее, исходя из положения точки открытия на странице.

<a name="sub-directions"></a>

Допустимые значения (в порядке приоритета):

* bottom-left;
* bottom-center;
* bottom-right;
* top-left;
* top-center;
* top-right;
* right-top;
* right-center;
* right-bottom;
* left-top;
* left-center;
* left-bottom.

Тип: `String`.


```js
{
    block: 'x-table',
    head: ['right-top', 'bottom-left', 'bottom-center', 'bottom-right', 'left-top', 'right-center', 'left-center', 'right-bottom', 'top-left', 'top-center', 'top-center', 'top-center' ],
    body: [
        ['right-top', 'bottom-left', 'bottom-center', 'bottom-right', 'left-top', 'right-center', 'left-center', 'right-bottom', 'top-left', 'top-center', 'top-center', 'top-center'].map((direction) => {
            return {
                block: 'popup-open',
                content: [
                    {
                        block: 'button2',
                        mods: { theme: 'normal', size: 'm' },
                        text: 'Открыть'
                    },
                    {
                        block: 'popup2',
                        mods: { target: 'anchor', theme: 'normal', autoclosable: 'yes' },
                        directions: [direction],
                        content: 'Попап'
                    }
                ]
            };
        })
    ]
}
```

Схематически:

<img width="433" height="168" src="https://jing.yandex-team.ru/files/tenorok/popup2-directions.png" />

<a name="field-mainoffset"></a>

#### Поле `mainOffset`

Определяет смещение блока в пикселях относительно [основного направления](#sub-directions). Значение по умолчанию: `0`, для темы `normal`:`5`. Используется только с модификатором `target`.

Тип: `Number`.

```js
{
    block: 'popup-open',
    content: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm' },
            text: 'Открыть'
        },
        {
            block: 'popup2',
            mods: { target: 'anchor', theme: 'normal', autoclosable: 'yes' },
            mainOffset: 40,
            content: 'Попап'
        }
    ]
}
```

<a name="field-secondaryoffset"></a>

#### Поле `secondaryOffset`

Определяет смещение блока в пикселях относительно [второстепенного направления](#sub-directions). Используется только с модификатором `target`.

Тип: `Number`.

```js
{
    block: 'popup-open',
    content: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm' },
            text: 'Открыть'
        },
        {
            block: 'popup2',
            mods: { target: 'anchor', theme: 'normal', autoclosable: 'yes' },
            secondaryOffset: 40,
            content: 'Попап'
        }
    ]
}
```

<a name="field-viewportoffset"></a>

#### Поле `viewportOffset`

Определяет минимально допустимое смещение в пикселях всплывающего окна от края окна браузера. Используется только с модификатором `target`.

Тип: `Number`.

```js
{
    block: 'popup-open',
    content: [
        {
            block: 'button2',
            mods: { theme: 'normal', size: 'm' },
            text: 'Открыть'
        },
        {
            block: 'popup2',
            mods: { target: 'anchor', theme: 'normal', autoclosable: 'yes' },
            viewportOffset: 20,
            content: 'Попап'
        }
    ]
}
```

<a name="field-hastail"></a>

#### Поле `hasTail`

Определяет наличие «хвостика» у всплывающего окна. По умолчанию «хвостик» отключен — `false`.

Допустимые значения: `true`, `false`.

Тип: `Boolean`.

```js
[
    {
        block: 'x-table',
        head: ['false', 'true'],
        body: [
            [false, true].map((hastail) => {
                return {
                    block: 'popup-open',
                    content: [
                        {
                            block: 'button2',
                            mods: { theme: 'normal', size: 'm', view: 'default', tone: 'default' },
                            text: 'Открыть'
                        },
                        {
                            block: 'popup2',
                            mods: { target: 'anchor', theme: 'normal', autoclosable: 'yes', view: 'default', tone: 'default' },
                            hasTail: hastail,
                            content: 'Попап'
                        }
                    ]
                };
            })
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'popup2', elem: 'tail' },
            { block: 'popup2', mods: { view: 'default' } }
        ].concat(['default', 'red', 'dark', 'grey'].map(tone => ({ block: 'popup2', mods: { tone } })))
    }
]
```

<a name="field-tailsize"></a>

#### Поле `tailSize`

Определяет размер «хвостика» всплывающего окна в пикселях. Значение по умолчанию: `10px`.

Тип: `Number`.

```js
[
    {
        block: 'popup-open',
        content: [
            {
                block: 'button2',
                mods: { theme: 'normal', size: 'm', view: 'default', tone: 'default' },
                text: 'Открыть'
            },
            {
                block: 'popup2',
                mods: { target: 'anchor', theme: 'normal', autoclosable: 'yes',  view: 'default', tone: 'default' },
                hasTail: true,
                tailSize: 12,
                content: 'Попап'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'popup2', elem: 'tail' },
            { block: 'popup2', mods: { view: 'default' } }
        ].concat(['default', 'red', 'dark', 'grey'].map(tone => ({ block: 'popup2', mods: { tone } })))
    }
]
```

<a name="field-tailoffset"></a>

#### Поле `tailOffset`

Определяет отступ «хвостика» от края всплывающего окна в пикселях. Значение по умолчанию: `0`.

Тип: `Number`.

```js
[
    {
        block: 'popup-open',
        content: [
            {
                block: 'button2',
                mods: { theme: 'normal', size: 'm', view: 'classic', tone: 'default' },
                text: 'Открыть'
            },
            {
                block: 'popup2',
                mods: { target: 'anchor', theme: 'normal', autoclosable: 'yes', view: 'classic' },
                hasTail: true,
                tailOffset: 12,
                content: 'Попап'
            }
        ]
    },
    {
        block: 'x-deps',
        content: [
            { block: 'popup2', elem: 'tail' },
            { block: 'popup2', mods: { view: 'default' } }
        ].concat(['default', 'red', 'dark', 'grey'].map(tone => ({ block: 'popup2', mods: { tone } })))
    }
]
```

<a name="z-index"></a>

#### Поле `zIndexGroupLevel`

Задает уровень слоя `z-index` для всплывающего окна. Значение по умолчанию: `0`.

Тип: `Number`.

В блоке поддерживается несколько способов влиять на устанавливаемый уровень слоя `z-index`. В общем случае, он рассчитывается по формуле `(level + 1) * 1000 + stackIndex`, где:

- `level` — вычисляется, как `zIndexGroupLevel` (собственный) + `zIndexGroupLevel` (родительского попапа) + сумма значений модификаторов `level` всех блоков [z-index-group](../z-index-group/z-index-group.ru.md), в которые вложена цель (anchor) попапа;
- `stackIndex` — это порядковый номер `z-index` в стеке слоев `z-index`. Нумерация начинается с `1`. Для каждого уровня создается свой стек, все стеки хранятся в объекте вида:

  ```js
  {
      0: [1000, 1001, 1002], // ключ - это level, значения в массиве - это и есть занятые z-index-ы
      9: [10000, 10001],
      // ..
  }
  ```

При каждом открытии попап занимает наименьший свободный слой `z-index` в стеке для своего уровня. А после закрытия — освобождает его. Попап может изменить свой `z-index` при вызове метода `setAnchor()`, чтобы пересчитать его относительно новой цели.

Служебный блок `z-index-group` создан специально для возможности влиять на `z-index` всех попапов в некотором контейнере. Например, шапка должна всегда иметь `z-index` больший, чем все попапы на странице, а попапы в шапке должны иметь `z-index` больший, чем у шапки. Для этого можно примешать, например, блок `z-index-group_level_9` к шапке, и она будет иметь `z-index=10000`, а попапы в ней — большие значения.

Примеры расчета `z-index`:

№ Шага | Действие | z-index
--- |--- | ---
1 | Открываем первый на странице попап (без `zIndexGroupLevel`) | `1001`
2 | Открываем второй на странице попап (без `zIndexGroupLevel`) | `1002`
3 | Открываем попап с `zIndexGroupLevel=1` | `2001`
4 | Открываем попап (без `zIndexGroupLevel`) с целью, вложенной в предыдущий попап | `2002`
5 | Открываем попап (без `zIndexGroupLevel`) с целью, вложенной в `z-index-group_level_1` | `2003`
6 | Открываем попап (c `zIndexGroupLevel=1`) с целью, вложенной в `z-index-group_level_9` | `11001`
7 | Открываем попап (без `zIndexGroupLevel`) с целью, вложенной в предыдущий попап | `11002`

Пример, иллюстрирующий эти шаги (для удобства все попапы показывают свой `z-index`):

```js
[
    {
        block: 'popup-open',
        content: [
            {
                block: 'button2',
                mods: {theme: 'normal', size: 's'},
                text: 'Открыть (1)'
            },
            {
                block: 'popup2',
                mods: {target: 'anchor', theme: 'normal', 'show-z-index': 'yes'},
                content: 'Привет!'
            }
        ]
    },

    {
        block: 'popup-open',
        content: [
            {
                block: 'button2',
                mods: {theme: 'normal', size: 's'},
                text: 'Открыть (2)'
            },
            {
                block: 'popup2',
                mods: {target: 'anchor', theme: 'normal', 'show-z-index': 'yes'},
                content: 'Привет!'
            }
        ]
    },

    {
        block: 'popup-open',
        content: [
            {
                block: 'button2',
                mods: {theme: 'normal', size: 's'},
                text: 'Открыть (3)'
            },
            {
                block: 'popup2',
                zIndexGroupLevel: 1,
                mods: {target: 'anchor', theme: 'normal', 'show-z-index': 'yes'},
                content: [
                   'Привет! У меня параметр zIndexGroupLevel=1<br>',
                   {
                       block: 'popup-open',
                       content: [
                           {
                               block: 'button2',
                               mods: {theme: 'normal', size: 's'},
                               text: 'Открыть (4)'
                           },
                           {
                               block: 'popup2',
                               mods: {target: 'anchor', theme: 'normal', 'show-z-index': 'yes'},
                               content: [
                                  'Привет! Я наследую уровень моего родителя.',
                               ]
                           }
                       ]
                   }
                ]
            }
        ]
    },

    '<br><br><br><br><br><br>',

    {
        block: 'x-area',
        mods: {bordered: 'yes', bg: 'squares'},
        mix: {block: 'z-index-group', mods: {level: 1}},
        content: [
            'Контейнер с z-index-group_level_1<br>',
            {
                block: 'popup-open',
                content: [
                    {
                        block: 'button2',
                        mods: {theme: 'normal', size: 's'},
                        text: 'Открыть (5)'
                    },
                    {
                        block: 'popup2',
                        mods: {target: 'anchor', theme: 'normal', 'show-z-index': 'yes'},
                        content: 'Привет! Я наследую уровень моего контейнера.'
                    }
                ]
            }
        ]
    },

    '&nbsp;&nbsp;&nbsp;',

    {
        block: 'x-area',
        mods: {bordered: 'yes', bg: 'squares'},
        mix: {block: 'z-index-group', mods: {level: 9}},
        content: [
            'Контейнер с z-index-group_level_9<br>',
            {
                block: 'popup-open',
                content: [
                    {
                        block: 'button2',
                        mods: {theme: 'normal', size: 's'},
                        text: 'Открыть (6)'
                    },
                    {
                        block: 'popup2',
                        mods: {target: 'anchor', theme: 'normal', 'show-z-index': 'yes'},
                        content: [
                            'Привет! Я наследую уровень моего контейнера, а так же у меня параметр <br>zIndexGroupLevel=1, поэтому мой z-index не 10001, а 11001<br>',
                            {
                                block: 'popup-open',
                                content: [
                                    {
                                        block: 'button2',
                                        mods: {theme: 'normal', size: 's'},
                                        text: 'Открыть (7)'
                                    },
                                    {
                                        block: 'popup2',
                                        mods: {target: 'anchor', theme: 'normal', 'show-z-index': 'yes'},
                                        content: 'Привет! Ну а я наследую все, что могу.'
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
```