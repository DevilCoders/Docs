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
[autoclosable](#mods-autoclosable) | `true`                                 | BEMJSON           | Автоматическое закрытие подсказки.
[shown](#mods-shown)               | `true`                                 | —                 | Видимость подсказки.
[hovered](#mods-hovered)           | `true`                                 | —                 | Прозрачность подсказки при наведении курсора.  Используется по умолчанию.

## JS-параметры блока

Параметр                         | Тип           | Значение по умолчанию | Описание
-------------------------------- | ------------- | --------------------- | -----------------------------------------------
[mainOffset](#params-mainOffset) | Number        | —                     | Отступ подсказки от вызывающего элемента.
[to](#params-to)                 | String, Array | —                     | Сторона открытия подсказки относительно вызывающего элемента.


## Подробнее

<a name="js-owner"></a>
### Использование в JavaScript

> **NB** Перед [показом](#mods-shown) `tooltip` необходимо в JS-коде блока задать вызывающий блок `owner` — элемент страницы, на который указывает подсказка. Иначе, появится сообщение об ошибке `Owner is unset`.

Взаимосвязь вызывающего блока и подсказки устанавливается в JavaScript через метод блока`tooltip` — `setOwner()` (на уровне переопределения проекта).

Динамически изменять содержимое подсказки можно с помощью метода блока `setContent`.

Пример установки взаимосвязи подсказки и вызывающего блока:

```javascript
modules.define('example', [
    'i-bem-dom', 'button', 'tooltip'
], function(provide, bemDom, Button, Tooltip) {

    const Example = bemDom.declBlock(this.name, {
        onSetMod: {
            js: {
                inited() {
                    const button = this.findChildBlock(Button);   // блок вызывающий подсказку
                    const tooltip = this.findChildBlock(Tooltip); // блок подсказки
    
                    tooltip
                        .setOwner(button) // объект на который будет указывать подсказка
                        .setContent('Success!') // динамически поменять содержимое подсказки
                        .setMod('shown'); // показать подсказку
    
                    this._events(button).on('click', function() {
                        tooltip.toggleMod('shown', true);
                    });
                }
            }
        }
    });
    
    provide(Example);
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
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'owner'
        },
        {
            block: 'tooltip',
            mods: {size: 'm', theme: 'normal'},
            content: 'normal'
        }
    ]
}
```

```js
{
    block: 'example',
    content: [
        {
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'owner'
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
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'owner'
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
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'owner'
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
            block: 'button',
            mods: {size: 'xs', theme: 'islands'},
            content: 'owner'
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
            block: 'button',
            mods: {size: 's', theme: 'islands'},
            content: 'owner'
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
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'owner'
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
            block: 'button',
            mods: {size: 'l', theme: 'islands'},
            content: 'owner'
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
Допустимое значение: `true`.

```js
{
    block: 'example',
    content: [
        {
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'Owner'
        },
        {
            block: 'tooltip',
            mods: {
                size: 'm',
                theme: 'success',
                autoclosable: true
            },
            content: 'Hello'
        }
    ]
}
```

<a name="mods-shown"></a>
#### Модификатор `shown`

Отвечает за отображение подсказки на странице. При установке модификатора подсказка появляется, при снятии модификатора — скрывается.

Допустимое значение: `true`.

<a name="mods-hovered"></a>
#### Модификатор `hovered`

Отвечает за изменение прозрачности подсказки. Выставляется автоматически при наведении курсора мыши на блок.

Допустимое значение: `true`.

### JS-параметры блока

Обратите внимание, что JS-параметры блока `tooltip` передаются в соответствующие JS-параметры блока `popup`.

<a name="params-mainOffset"></a>
#### Параметр `mainOffset`

Определяет отступ подсказки от вызывающего элемента на странице в пикселях, с учетом размера хвостика (элемент `tail`).

Тип: Number.

Подсказка с отступом от вызывающего элемента:

```js
{
    block: 'example',
    content: [
        {
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'Owner'
        },
        {
            block: 'tooltip',
            mods: {size: 'm', theme: 'success', autoclosable: true},
            js: {mainOffset: 42}, // отступ подсказки
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
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'owner'
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
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'owner'
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
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'owner'
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
            block: 'button',
            mods: {size: 'm', theme: 'islands'},
            content: 'owner'
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
