# popup2

Блок `popup2` (далее «попап») используется для создания различных выпадающих элементов. Новая версия блока [popup](../popup/popup.ru.md).

## Обзор
* [Автоматическое уничтожение](#destroy)
* [Взаимосвязи между блоками popup](#p2p)
* [Работа со слоями z-index](#z-index)
* [Отличия от блока popup](#diff)
* [Известные проблемы и их решения](#trouble)

### Модификаторы блока

|Модификатор | Допустимые значения | Способы установки | Описание |
| -----------| --------------------| ------------------| ---------|
| [target](#mods-target)| `anchor`, `position` | BEMJSON | Способ позиционирования блока. |
| [theme](#mods-teme) | `normal`, `clear` | BEMJSON | Стилевое оформление блока.|
| [visible](#mods-visible) | `yes` | JS | Видимость блока. |
| [autoclosable](#mods-autoclosable)| `yes` | BEMJSON | Автоматическое закрытие блока. |
| [motionless](#mods-motionless)| `yes` | BEMJSON | Закрепляет положение всплывающего окна после открытия. |


### BEMJSON-поля блока

| Поле | Тип | Описание  |
| ---- | --- | --------- |
| [directions](#field-direction) | `String[]` | Направления раскрытия блока. По умолчанию содержит все 12 допустимых направлений.
| [mainOffset](#field-mainOffset) | `Number` | Смещение блока относительно [основного направления](#sub-directions). Значение по умолчанию: `0`, для темы `normal`:`5`.
| `secondaryOffset` | `Number` | Задает смещение попапа относительно [второстепенного направления](#sub-directions). Значение по умолчанию:  `0`.
| `viewportOffset` | `Number` | Задает обязательный отступ от края окна браузера. Значение по умолчанию: `0`, для темы `normal`:`5`.
| `tailOffset` | `Number` | Задает отступ хвостика от края всплывающего окошка. Значение по умолчанию: `0`.
| [zIndexGroupLevel](#z-index) | `Number` | Позволяет задать уровень слоев `z-index` для открывающихся попапов. Значение по умолчанию: `0`.

### Элементы блока

Элемент | Описание
---| ---
[tail](#elems-tail) | Хвостик. Может использоваться только для блока с модификатором `target` в значении `anchor`.

## Подробнее

### Модификаторы блока

<a name="mods-target"></a>
#### Модификатор `target`

Определяет объект (цель) на странице относительно которого позиционируется блок.

Способы установки: BEMJSON.

| Допустимые значения | Описание |
| ------------------- | -------- |
| `anchor` | Позиционирование блока относительно DOM-элемента. Цель задается с помощью метода `setAnchor()`, который принимает в качестве аргумента DOM-элемент или БЭМ-блок.
| `position` | Позиционирование блока относительно координат страницы. Цель задается с помощью метода `setPosition()`, который принимает в качестве аргументов горизонтальную и вертикальную координаты.|

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
        js: {position: [20, 60]},
        content: [
            {
                block: 'button2',
                mods: {theme: 'normal', size: 's'},
                text: 'Открыть (position)'
            },
            {
                block: 'popup2',
                mods: {target: 'position', theme: 'normal', autoclosable: 'yes'},
                content: 'Попап спозиционирован в точке (20;60). Однако по вертикали<br> ' +
                'он имеет координату 65px вместо 60px, это происходит т.к. по умолчанию для<br>' +
                'темы normal mainOffset=5. Если этот эффект нежелателен, просто обнулите <br>смещение в памаретрах.'
            }
        ]
    }
]
```

<a name="mods-theme"></a>
#### Модификатор `theme`

Отвечает за стилевое оформление блока.

Способы установки: BEMJSON.

| Допустимые значения | Описание |
| ------------------- | -------- |
| `normal` | Стандартное оформление в стиле «Острова» . Содержит анимацию открытия/закрытия и добавляет параметры `mainOffset=5` и `viewportOffset=5`.|
| `clear` | Блок без рамки. Выставляет только `display: block` для открытого блока `popup2`. Отсутствует анимация открытия/закрытия. На основе этой темы можно реализовать собственный стиль оформления.  |

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

<a name="mods-visible"></a>
#### Модификатор `visible`

Отвечает за видимость блока на странице.

Чтобы открыть попап, необходимо выставить ему модификатор `visible` со значением `yes`, чтобы скрыть — удалить модификатор.

При первом открытии блока его DOM-элемент перемещается в конец `<body>`.

Способы установки: JS.<br>
Допустимое значение: `yes`.


<a name="mods-autoclosable"></a>
#### Модификатор `autoclosable`

Отвечает за скрытие блока кликом за его пределами или нажатием  **ESC**.
В последнем случае попапы закрываются в порядке, обратном порядку открытия при каждом следующем нажатии.

Способы установки: BEMJSON. <br>
Допустимое значение: `yes`.

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

Закрепляет положение всплывающего окна блока `popup2` после открытия. Открыв окно в одном из направлений, направление
закрепляется и не изменяется при прокрутке страницы. Чтобы изменить положение, необходимо заново закрыть и открыть
всплывающее окно.

Способы установки: BEMJSON.

Допустимое значение: `yes`.

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
            content: 'Привет!'
        }
    ]
}
```


### BEMJSON-поля блока

<a name="field-direction"></a>
#### Поле `directions`

Задает направление раскрытия блока относительно объекта открытия (цели).

Для управления расположением блока необходимо указать массив направлений раскрытия. При этом из значений массива будет выбрано наиболее подходящее, исходя из положения объекта открытия на странице.

Тип: `String[]`.

Допустимые значения (в порядке приоритета):

* bottom-left
* bottom-center
* bottom-right
* top-left
* top-center
* top-right
* right-top
* right-center
* right-bottom
* left-top
* left-center
* left-bottom

Допустимые направления представлены комбинацией основного и второстепенного направлений, где:
<a name="sub-directions"></a>

* основное (часть до `-`) — позиционирует попап относительно цели.
* второстепенное (часть после `-`) — задает выравнивание.

Схематически:

<img width="433" height="168" src="https://jing.yandex-team.ru/files/tenorok/popup2-directions.png" />

<a name="field-mainOffset"></a>
#### Поле `mainOffset`

Определяет смещение блока в пикселях относительно [основного направления](#sub-directions).

Тип: `Number`. <br>
Значение по умолчанию: `0`, c темой `normal`: `5`.

<a name="z-index"></a>
#### Поле `zIndexGroupLevel`

Задает уровень слоев `z-index` для открывающихся попапов.

Тип:`Number`.
Значение по умолчанию: `0`.

В блоке поддерживается несколько способов влиять на устанавливаемый попапу `z-index`. В общем случае, он рассчитывается по формуле `(level + 1) * 1000 + stackIndex`, где:

* `level` — вычисляется, как `zIndexGroupLevel` (собственный) + `zIndexGroupLevel` (родительского попапа) + сумма значений модификаторов `level` всех блоков [z-index-group](../z-index-group/z-index-group.ru.md), в которые вложена цель (anchor) попапа;
* `stackIndex` — это порядковый номер `z-index` в стеке слоев `z-index`. Нумерация начинается с `1`. Для каждого уровня создается свой стек, все стеки хранятся в объекте вида:

  ```javascript
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

### Элементы блока

<a name="elems-tail"></a>
#### Элемент `tail`

Хвостик для блока, который позиционируется относительно DOM-элемента. Может использоваться только для блока с модификатором `target` в значении `anchor`.

Отображается в любом из направлений раскрытия и всегда указывает на середину цели попапа.

> **NB** Хвостик работает во всех браузерах, кроме IE8 и IE9, так как они не поддерживают CSS-трансформации и CSS-градиенты,
которые нужны для гибкой и простой реализации. В качестве деградации, в этих браузерах попап отображается без
хвостика, даже если он добавлен.

По умолчанию размер хвостика равен `10px`, но его можно легко изменить через `CSS`. Единственное ограничение:
высота и ширина должны совпадать и иметь значение кратное `2px`.

```css
.popup2__tail
{
    width: 16px;
    height: 16px;
}
```

Чтобы включить отображение хвостика, нужно подключить элемент `tail` в зависимости и разместить его в `content` попапа:

```js
[
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
                content: [
                    {elem: 'tail'},
                    'Попап  с хвостиком'
                ]
            }
        ]
    },

    {
        block: 'popup-open',
        content: [
            {
                block: 'button2',
                mods: {theme: 'normal', size: 's'},
                text: 'Открыть попап с увеличенным хвостиком'
            },
            {
                block: 'popup2',
                mods: {target: 'anchor', theme: 'normal', autoclosable: 'yes'},
                content: [
                    {elem: 'tail', attrs: {style: 'width: 16px; height: 16px'}},
                    'Попап  с увеличенным хвостиком'
                ]
            }
        ]
    }
]
```

> **NB** При использовании хвостика смещение попапа по основному направлению раскрытия (`mainOffset`) автоматически
увеличивается, чтобы хвостик помещался между попапом и его целью.


<a name="destroy"></a>
### Автоматическое уничтожение

Блок `popup2` с  модификатором `target` в  значении `anchor` автоматически самоуничтожится, если его цель (DOM-элемент или БЭМ-блок, относительно которой он позиционируется) уничтожена c помощью `BEM.DOM.destruct()`.

<a name="p2p"></a>
### Взаимосвязи между блоками popup

Блоки `popup2` можно вкладывать друг в друга без использования дополнительных методов. Блок считается вложенным, если его цель (`anchor`) находится в другом попапе. Дочерним может быть только попап с модификатором `target` в значении `anchor`.

Особенности поведения вложенных попапов:

* Если закрывается родительский попап, то дочерний закрывается автоматически.
* Если уничтожается родительский попап, то дочерний уничтожается автоматически. Подробнее об [автоматическом уничтожении](#destroy).
* Дочерний попап рассчитывает свой `z-index` с учетом родительского. Подробнее о [работе с z-index](#z-index).
* Клик по дочерним попапам не вызывает закрытие родительских попапов. Подробнее о [модификаторе autoclosable](#mods-autoclosable).

<a name="diff"></a>
## Отличия от блока `popup`

В блоке `popup2`:

1. Не содержится модальное окно. Теперь оно реализовано в виде отдельного блока [modal](../modal/modal.ru.md).
1. Отсутствует закрывающий крестик.
1. Не используется `iframe` для перекрытия Flash в старых версиях браузеров.
1. `popup2` всегда выносит себя в конец `<body>`, даже если он находится в другом попапе или модальном окне.

<a name="#trouble"></a>
## Известные проблемы и их решения

1. Во всех версиях браузера IE и некоторых Safari блок `popup2`, расположенный относительно цели с `position: fixed`, подергивается при прокрутке страницы. Для попапов небольших размеров (`dropdown`, `select`) это выглядит приемлемо, а для больших (`suggest` на всю страницу), в качестве решения, можно скрывать попап при прокрутке.
1. При ненулевом значении свойства `margin` у `<body>`, блок `popup2` позиционируется неправильно. Чтобы решить проблему, не используйте это свойство для `<body>`.
