# suggest2-popup

Блок `suggest2-popup` — адаптер API для подключения к саджесту popup-блоков из разных библиотек (не только `islands-*`, но и библиотек сервисов). Popup-блок служит контейнером для подсказок саджеста.

По умолчанию в `suggest2-popup` реализованы [адаптеры API](#mods-for) для подключения блоков [popup](../popup/popup.ru.md) и [popup2](../popup2/popup2.ru.md) из `islands-*`.


## Обзор

<a name="mods"></a>
### Модификаторы блока

| Модификатор                | Допустимые значения | Способы установки | Описание |
| -------------------------- | ------------------- | ------------------| ---------|
| [disabled](#mods-disabled) |	`yes`              |	 JS	             | Неактивное состояние блока. |
| [for](#mods-for)           |`popup`, `popup2`    | BEMJSON           | Адаптер API для popup-блока.


## Подробнее

<a name="mods-disabled"></a>
### Модификатор `disabled`

Отвечает за неактивное состояние блока.

Выставляется автоматически при выставлении неактивного состояния блоку [suggest2-form](../suggest2-form/suggest2-form.ru.md#%D0%9C%D0%BE%D0%B4%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%82%D0%BE%D1%80-disabled).

Способы установки: JS.<br>
Допустимое значение: `yes`.

<a name="mods-for"></a>
### Модификатор `for`

Используется для выбора адаптера API (набор методов управления `popup` и событиями) и взаимодействия саджеста с определенным popup-блоком.

Способы установки: BEMJSON.<br>

Допустимые значения | Описание
------------------- | ----------------------
`popup`             | Адаптер API для блока [popup](https://github.yandex-team.ru/lego/islands/blob/dev/common.blocks/popup/popup.ru.md).
`popup2`            | Адаптер API для блока [popup2](https://github.yandex-team.ru/lego/islands/blob/dev/common.blocks/popup2/popup2.ru.md). <br> **NB** Для корректного поиска блока `popup2`, необходимо указать JS-параметр блоку [suggest2-form](../suggest2-form/suggest2-form.ru.md): ```js: {popupName: 'popup2'}```.

**NB** Обратите внимание, что при данном подходе у `suggest2-form` должны присутствовать popup-блоки одного типа, так как адаптер пробрасывается один для всех.

> **NB** Чтобы использовать модификатор, подключите его с нужным значением в зависимости блока на проектном уровне.

Саджест с блоком `popup`

```js
{
    block: 'form',
    tag: 'form',
    mix: [
        {block: 'normal'},
        {block: 'suggest2-form', js: true}
    ],
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 'm', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                attrs: {style: 'width: 50%'},
                content: {elem: 'control'}
            },
            {
                block: 'button2',
                mods: {size: 'm', theme: 'normal', pin: 'clear-round'},
                type: 'submit',
                mix: {block: 'suggest2-form', elem: 'button'},
                text: 'Найти'
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                js: {directions: 'bottom-left'},
                mix: [{
                    block: 'suggest2',
                    mods: {theme: 'normal', size: 'm', adaptive: 'yes'},
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```

Саджест с блоком `popup2`

```js
{
    block: 'form',
    tag: 'form',
    mix: [
        {
            block: 'suggest2-form',
            js: {popupName: 'popup2'} // JS-параметр для корректного поиска popup2
        }
    ],
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 'm', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                attrs: {style: 'width: 50%'},
                content: {
                    elem: 'control',
                    attrs: {name: 'text', tabindex: 1, autocomplete: 'off', maxlength: 400}
                }
            },
            {
                block: 'button2',
                mods: {size: 'm', theme: 'normal', pin: 'clear-round'},
                type: 'submit',
                mix: {block: 'suggest2-form', elem: 'button'},
                text: 'Найти'
            },
            {
                block: 'popup2',
                mods: {target: 'anchor', theme: 'clear', autoclosable: 'yes'},
                directions: ['bottom-left'],
                mix: [{
                    block: 'suggest2',
                    mods: {type: 'simple', theme: 'normal', size: 'm', adaptive: 'yes'},
                    js: {
                        url: '//suggest.yandex.ru/suggest-ya.cgi',
                        data: {
                            v: 4,
                            lr: 213,
                            wiz: 'TrWth',
                            fact: 1,
                            icon: 1,
                            hl: 1
                        }
                    }
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}  
```
