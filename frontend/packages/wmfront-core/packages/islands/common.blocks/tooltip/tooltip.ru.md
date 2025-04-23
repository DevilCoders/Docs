# tooltip

Блок `tooltip` используется для создания всплывающих подсказок. Подсказка указывает на элемент страницы (`owner`), который ее вызывает. Блок представляет собой обвязку блока [`popup`](../popup/popup.ru.md).

С помощью API блока можно:

* изменять оформление подсказки: [размер](#mods-size), [цвет](#mods-theme);
* задавать [сторону раскрытия подсказки](#params-to) относительно вызывающего элемента;
* [смещать](#move) хвостик (элемент `tail`) относительно центра стороны подсказки;
* управлять [состоянием подсказки](#mods-show): скрыть/показать;
* выполнять [автоматическое закрытие](#mods-autoclosable) подсказки (по умолчанию подсказка скрывается щелчком мыши по ней).


## Обзор

* [Использование в JavaScript](#js-owner)
* [Смещение хвостика подсказки](#move)

## Модификаторы блока

Модификатор	                       | Допустимые значения                    | Способы установки | Описание
---------------------------------- | -------------------------------------  | ----------------  | --------------------------------------
[theme](#mods-theme)               | `normal`, `error` , `success`, `white` | BEMJSON           | **Обязательный**. Стилевое оформление подсказки. Используется совместно с модификатором [size](#mods-size).
[size](#mods-size)                 | `xs`, `s`, `m` , `l`                   | BEMJSON           | **Обязательный**. Размер подсказки. Используется совместно с модификатором [theme](#mods-theme).
[autoclosable](#mods-autoclosable) | `yes`                                  | BEMJSON           | Автоматическое закрытие подсказки.
[shown](#mods-shown)                 | `yes`                                  | —                 | Видимость подсказки.
[hovered](#mods-hovered)           | `yes`                                  | —                 | Прозрачность подсказки при наведении курсора.  Используется по умолчанию. Уровень переопределения: `desktop`.

## BEMJSON-поля блока

|  Поле                | Тип     | Описание                                          |
| -------------------- | ------- | ------------------------------------------------- |
| [tail](#fields-tail) | Boolean | Выключает хвостик. Значение по умолчанию: `true`. |


## Элементы блока

 Элемент            | Описание
------------------- | -------------------------------------------------
[tail](#elems-tail) | «Хвостик» подсказки. Используется по умолчанию.

## JS-параметры блока

Параметр                                   | Тип           | Значение по умолчанию | Описание
------------------------------------------ | ------------- | --------------------- | -----------------------------------------------
[offset (Deprecated)](#params-offset)                   | Number        | —                     | Отступ подсказки от вызывающего элемента.
[mainOffset](#params-offset)                   | Number        | —                     | Отступ подсказки от вызывающего элемента.
[secondaryOffset](#params-secondaryOffset) | Number        | —                     | Отступ подсказки относительно вторичного направления раскрытия.
[tailOffset](#params-tailOffset)           | Number        | —                     | Отступ хвостика подсказки вдоль вторичного направления раскрытия.
[to](#params-to)                           | String, Array | —                     | Сторона открытия подсказки относительно вызывающего элемента.


## Подробнее

<a name="js-owner"></a>
### Использование в JavaScript

> **NB** Перед [показом](#mods-shown) `tooltip` необходимо в JS-коде блока задать вызывающий блок `owner` — элемент страницы, на который указывает подсказка. Иначе, появится сообщение об ошибке `Owner is unset`.

Взаимосвязь вызывающего блока и подсказки устанавливается в JavaScript через метод блока`tooltip` — `setOwner()` (на уровне переопределения проекта).

Динамически изменять содержимое подсказки можно с помощью метода блока `setContent`.

Пример установки взаимосвязи подсказки и вызывающего блока:

```javascript
BEM.DOM.decl('example', {
    onSetMod: {
        js: {
            inited: function() {
                var button = this.findBlockInside('button2'), // блок вызывающий подсказку
                    tooltip = this.findBlockInside('tooltip'); // блок подсказки

                tooltip
                    .setOwner(button) // объект на который будет указывать подсказка
                    .setContent('Success!') // динамически поменять содержимое подсказки
                    .setMod('shown', 'yes'); // показать подсказку

                button.on('click', function() {
                    tooltip.toggleMod('shown', 'yes', '');
                });
            }
        }
    }
});
```

### Модификаторы блока

<a name="mods-theme"></a>
#### Модификатор `theme`

**Обязательный**. <br>
Отвечает за стилевое оформление блока. Необходимо использовать совместно с [модификатором size](#mods-size).

Способ установки: BEMJSON. <br>
Допустимые значения:

Значение            | Описание
------------------- | ---------------------------------
`normal`            | Обычная подсказка с серым фоном.
`error`             | Подсказка с красным фоном.
`success`           | Подсказка с зеленым фоном.
`white`             | Подсказка с белым  фоном.

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {size: 'm', theme: 'normal'},
            text: 'normal'
        }
    ]
}
```

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {size: 'm', theme: 'error'},
            content: 'error'
        }
    ]
}
```

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {size: 'm', theme: 'success'},
            content: 'success'
        }
    ]
}
```

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {size: 'm', theme: 'white'},
            content: 'white'
        }
    ]
}
```

<a name="mods-size"></a>
####  Модификатор `size`

**Обязательный**.<br>
Отвечает за размер блока. Необходимо использовать совместно с [модификатором theme](#mods-theme).

Способ установки: BEMJSON. <br>
Допустимые значения: `xs`, `s`, `m`, `l`.

Размерная сетка для подсказок соответствует [размерам кнопки в версии v3.0.0](https://github.yandex-team.ru/lego/islands-components/blob/v3.3.1/common.blocks/button/button.ru.md).

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'xs', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {
                size: 'xs',
                theme: 'success'
            },
            content: 'xs'
        }
    ]
}
```

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 's', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {
                size: 's',
                theme: 'success'
            },
            content: 's'
        }
    ]
}
```

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {
                size: 'm',
                theme: 'success'
            },
            content: 'm'
        }
    ]
}
```

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'l', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {
                size: 'l',
                theme: 'success'
            },
            content: 'l'
        }
    ]
}
```

<a name="mods-autoclosable"></a>
#### Модификатор `autoclosable`

Отвечает за автоматическое закрытие подсказки щелчком мыши за пределами ее области или нажатием клавиши **Esc**.

По умолчанию подсказка закрывается нажатием мыши по ней.

Способ установки: BEMJSON. <br>
Допустимое значение: `yes`.

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'Owner'
        },
        {
            block: 'tooltip',
            mods: {
                size: 'm',
                theme: 'success',
                autoclosable: 'yes'
            },
            content: 'Hello'
        }
    ]
}
```

<a name="mods-shown"></a>
#### Модификатор `shown`

Отвечает за отображение подсказки на странице. При установке модификатора подсказка появляется, при снятии модификатора — скрывается.

Допустимое значение: `yes`.

<a name="mods-hovered"></a>
#### Модификатор `hovered`

Отвечает за изменение прозрачности подсказки. Выставляется автоматически при наведении курсора мыши на блок.

Допустимое значение: `yes`. <br>
Уровень переопределения: `desktop`.

### BEMJSON-поля блока

<a name="fields-tail"></a>
#### Поле `tail`

Тип: Boolean. <br>
Значение по умолчанию: `true`.

Отвечает за отключение хвостика.

```js
 {
    block: 'tooltip',
    mods: {size: 'm', theme: 'normal'},
    tail: `false`,
    content: 'Without tail'
}
```

<a name="elems-tail"></a>
### Элементы блока

<a name="elems-tail"></a>
#### Элемент `tail`

Задает «хвостик» для подсказки, который указывает на вызывающий элемент. Используется по умолчанию. Реализован в технологии CSS.

Допустимые размеры определены в значениях [модификатора size](#mods-size).

### JS-параметры блока

Обратите внимание, что JS-параметры блока `tooltip` передаются в соответствующие JS-параметры блока `popup`.

<a name="params-offset"></a>
#### Параметр `mainOffset`

Определяет отступ подсказки от вызывающего элемента на странице в пикселях, с учетом размера хвостика (элемент `tail`).

Тип: Number.

Подсказка с отступом от вызывающего элемента:

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'Owner'
        },
        {
            block: 'tooltip',
            mods: {size: 'm', theme: 'success', autoclosable: 'yes'},
            js: {mainOffset: 42}, // отступ подсказки
            content: 'Hello'
        }
    ]
}
```

<a name="params-secondaryOffset"></a>
#### Параметр `secondaryOffset`

Определяет отступ вторичного направления раскрытия подсказки в пикселях.

Тип: Number.

Подсказка со вторичным отступом:

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'Owner'
        },
        {
            block: 'tooltip',
            mods: {size: 'm', theme: 'success', autoclosable: 'yes'},
            js: {secondaryOffset: 18}, // вторичный отступ подсказки
            content: 'Hello'
        }
    ]
}
```

<a name="params-tailOffset"></a>
#### Параметр `tailOffset`

Определяет отступ хвостика вдоль вторичного направления раскрытия подсказки в пикселях.

Тип: Number.

Подсказка со отступом хвостика:

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'Owner'
        },
        {
            block: 'tooltip',
            mods: {size: 'm', theme: 'success', autoclosable: 'yes'},
            js: {tailOffset: 5}, // отступ хвостика подсказки
            content: 'Hello'
        }
    ]
}
```

<a name="params-to"></a>
#### Параметр `to`

Отвечает за определение стороны открытия подсказки относительно вызывающего элемента (на нее  указывает хвостик подсказки).

Если значение не задано во входном BEMJSON, то оно автоматически определится, исходя из положения вызывающего элемента на странице и массива допустимых значений по умолчанию (в порядке приоритета).

Тип: String, Array. <br>
Допустимые значения (в порядке приоритета): `right`, `bottom`, `top`, `left`.

**top**
```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {
                size: 'm',
                theme: 'success'
            },
            js: {to: ['top']},
            content: 'top'
        }
    ]
}
```

**bottom**

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {
                size: 'm',
                theme: 'success'
            },
            js: {to: ['bottom']},
            content: 'bottom'
        }
    ]
}
```

**left**

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {
                size: 'm',
                theme: 'success'
            },
            js: {to: ['left']},
            content: 'left'
        }
    ]
}
```
**right**

```js
{
    block: 'example',
    content: [
        {
            block: 'button2',
            mods: {size: 'm', theme: 'normal'},
            text: 'owner'
        },
        {
            block: 'tooltip',
            mods: {
                size: 'm',
                theme: 'success'
            },
            js: {to: ['right']},
            content: 'right'
        }
    ]
}
```
<a name="move"></a>
### Смещение хвостика подсказки
Чтобы управлять смещением хвостика (`элемент tail`) подсказки нужно:

* Примиксовать к блоку `tooltip` произвольной блок, например, `custom-tooltip`.
* В блоке `custom-tooltip` задать параметры (или способ вычисления параметров) для смещения хвостика.

По умолчанию хвостик располагается по центру границы блока `tooltip`.

```javascript
{
     block: 'tooltip',
     mix: [{block: 'custom-tooltip'}],
     mods: {size: 'xs', theme: 'success'},
     js: {to: ['top']},
     content: 'success success success!'
 }
```

`tooltip.examples/60-tail-offset.blocks/custom-tooltip/custom-tooltip.css`

```css
.custom-tooltip.tooltip
{
    margin-left: -50px;
}
.custom-tooltip.tooltip .tooltip__tail
{
    left: 80%;
}
```
