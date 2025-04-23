## Описание

**Статус блока**: **deprecated**

Рекомендуется перейти на использование блоков `dropdown2` или `popup2` совместно с `menu`.

Блок `dropdown-menu` – выпадающее меню. Составной блок, реализованный на основе блоков [dropdown](../dropdown/dropdown.ru.md) и [b-menu-vert](../b-menu-vert/b-menu-vert.ru.md)/[b-menu-horiz](../../desktop.blocks/b-menu-horiz/b-menu-horiz.ru.md). Является сокращенной формой, которая служит для более удобного использования блоков [dropdown](../dropdown/dropdown.ru.md) и [b-menu](../b-menu/b-menu.ru.md).

Элементом, относительно которого открывается меню, могут быть кнопки, ссылки или другие элементы-триггеры.

### Элементы блока

  * `switcher` – блок-переключатель. Элемент, относительно которого открывается меню. Должен обладать следующими характеристиками:
    *  уметь вызывать BEM-событие `click`;
    *  уметь корректно реагировать на установку модификатора `disabled` в значение `yes` и на его снятие.

  * `popup` – выпадающее окно меню с элементом `tail` (хвост попапа), указывающим на блок, вызвавший меню. Базируется на блоке [popup](../popup/popup.ru.md).

  * `menu` – меню с пунктами `item`, построено на основе блока [b-menu-vert](../b-menu-vert/b-menu-vert.ru.md)/[b-menu-horiz](../../desktop.blocks/b-menu-horiz/b-menu-horiz.ru.md) (блок, создающий разметку для меню). Меню может быть вертикальным и горизонтальным. По умолчанию – вертикальное. Тип меню определяется в поле блока `type`.
Допустимые значения для него: `vert`(вертикальное меню), `horiz`(горизонтальное меню).

Направление раскрытия окна с меню выполняется в порядке, установленном в блоке [popup](../popup/popup.ru.md).


### Объявление блока на странице

Для создания выпадающего меню нужно в контенте блока задать элемент `switcher` и перечислить в контенте элемента `popup` все элементы меню `item`. В качестве содержимого `item` используются псевдоссылки (блок [link](../link/link.ru.md)).

```javascript
{
    block: 'dropdown-menu', // имя блока
    content: [
        { // блок-переключатель
            elem: 'switcher',
            content: {
                block: 'button',
                mods: {size: 'm', arrow: 'down', theme: 'normal'},
                content: 'Меню, пожалуйста'
            }
        },
        { // выпадающее окно с меню
            elem: 'popup',
            content: [ // массив элементов item
                {
                    elem: 'item', // элемент меню - псевдоссылка
                    content: {
                        block: 'link',
                        mods: {pseudo: 'yes'},
                        content: 'Пункт1'
                    }
                },
                {
                    elem: 'item',
                    content: {
                        block: 'link',
                        mods: {pseudo: 'yes'},
                        content: 'Пункт2'
                    }
                },
                ...
            ]
        }
    ]
}
```

```js
{
    block: 'dropdown-menu',
    content: [
        {
            elem: 'switcher',
            content: {
                block: 'button',
                mods: {size: 'm', arrow: 'down', theme: 'normal'},
                content: 'Меню, пожалуйста'
            }
        },
        {
            elem: 'popup',
            content: [
                {
                    elem: 'item',
                    content: {
                        block: 'link',
                        mods: {pseudo: 'yes'},
                        content: 'Поиск'
                    }
                },
                {
                    elem: 'item',
                    content: {
                        block: 'link',
                        mods: {pseudo: 'yes'},
                        content: 'Карты'
                    }
                }
            ]
        }
    ]
}
```

### Параметры шаблона

`{Object} menuMods` – поле модификаторов выпадающего меню. Располагается в элементе `popup`. Необязательное.
Модификатор `{type: 'hovered'}` также не является обязательным и, при необходимости, зависимость должна быть доопределена.

```javascript
{
    block: 'dropdown-menu',
    content: [
        {
            elem: 'switcher',
            content: {<блок-переключатель>}
        },
        {
            elem: 'popup',
            menuMods: {type: 'hovered'}, // модификаторы меню
            content: [<массив из элементов item>]
        }
    ]
}
```

`{Object} menuTitle` – поле, формирующее заголовок выпадающего меню. Располагается в элементе `popup`. Соответствует полю `title` блока [b-menu-vert](../b-menu-vert/b-menu-vert.ru.md). Необязательное.

```javascript
{
    block: 'dropdown-menu',
    content: [
        {
            elem: 'switcher',
            content: { <блок-переключатель> }
        },
        {
            elem: 'popup',
            menuTitle: { elem: 'title', content: 'Некоторый заголовок' }, // заголовок меню
            content: [ <массив из элементов item> ]
        }
    ]
}
```

### Модификаторы

#### Модификатор `theme`

Задает стилевое оформление блока. Внешнее оформление наследуется от блока `popup`.

Допустимое значение: `ffffff`. Используется по умолчанию.

_**Примечание**: Размер шрифта и высота строки для пункта меню соответствуют размеру `m` и включены в тему оформления по умолчанию. Отдельный модификатор размера со значением `m` не реализован в данной версии._

#### Модификатор `size`
Устанавливает размер для пункта меню. Необязательный.

Допустимое значение: `s`.

По умолчанию пункты выпадающего меню (псевдоссылки) при наведении курсора мыши меняют цвет.
Модификатор элемента `menu`: `type` со значением `hovered` изменит цвет шрифта на черный, и при наведении пункт меню будет выделяться желтой подсветкой.

```js
{
    block: 'dropdown-menu',
    content: [
        {
            elem: 'switcher',
            content: {
                block: 'button',
                mods: {size: 's', arrow: 'down', theme: 'normal'},
                content: 'Меню, пожалуйста'
            }
        },
        {
            elem: 'popup',
            menuMods: {type: 'hovered'},
            content: [
                {
                    elem: 'item',
                    content: {
                        block: 'link',
                        mods: {pseudo: 'yes'},
                        content: 'Поиск'
                    }
                },
                {
                    elem: 'item',
                    content: {
                        block: 'link',
                        mods: {pseudo: 'yes'},
                        content: 'Карты'
                    }
                }
            ]
        }
    ]
}
```
