# search2

Блок `search2` используется для создания поисковой формы.

## Обзор
### Примеры форм
Поисковая стрелка с произвольным контентом:

```js
{
    block: 'search2',
    url: 'http://yandex.com.tr/yandsearch',
    input: {
        block: 'input',
        mods: {size: 'ws-head', theme: 'websearch'},
        value: 'moskova',
        content: [
            {elem: 'found', content: ' — 8 milyon sonuç'},
            {
                elem: 'control',
                attrs: {
                    name: 'text',
                    autocomplete: 'off',
                    maxlength: 400
                }
            }
        ]
    },
    button: {
        block: 'button2',
        mods: {size: 'ws-head', theme: 'websearch', type: 'submit'},
        attrs: {tabindex: -1},
        text: 'Bul'
    }
}
```

Форма поиска по сервису:

```js
{
    block: 'search2',
    url: 'https://search.yandex-team.ru/search',
    input: {
        block: 'input',
        mods: {size: 'm', theme: 'normal', pin: 'round-clear'},
        value: 'islands',
        content: {elem: 'control', attrs: {name: 'text'}}
    },
    button: {
        block: 'button2',
        mods: {size: 'm', theme: 'action', type: 'submit', pin: 'brick-round'},
        attrs: {tabindex: -1},
        text: 'Найти'
    }
}
```


### Модификаторы блока

| Модификатор        | Допустимые значения  | Способы установки | Описание
| ------------------ | -------------------- | ----------------- | ------------------
| [template](#mods-template) | `websearch` | BEMJSON | Поисковая стрелка с содержимым по умолчанию. Рекомендуется использовать в ознакомительных целях или когда кастомизация стрелки не нужна. |
| [theme](#mods-theme) | `websearch` | BEMJSON | Стилевое оформление поисковой стрелки. |


### BEMJSON-поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [input](#fields-input)| BEMJSON | Содержимое [элемента input](#elems-short). |
| [button](#fields-button)| BEMJSON | Содержимое [элемента button](#elems-short). |
| [hidden](#add-hidden) | Object | Ключи и значения скрытых полей формы. |
| `content` | BEMJSON | Содержимое поисковой формы. Используется для самостоятельного формирования содержимого формы, с помощью [элементов блока](#elems-short). Не применяется совместно с полями `input`, `button`, `hidden`, так как их значения будут переопределены. |
| [label](#fields-label)| String | Значение атрибута `aria-label`. Прочитывается программами экранного доступа. |
| [url](#fields-url)| String | Значение атрибута `action`. |

<a name="elems-short"></a>
### Элементы блока

| Элемент | Описание |
| --------| -------- |
| [input](#elems-input) | **Обязательный**. Контейнер для поля ввода поисковой формы. |
| [button](#elems-button) | **Обязательный**. Контейнер для кнопки поисковой формы. |
| [hidden](#add-hidden) | Скрытое поле `<input type="hidden">`. |


## Подробнее

<a name="add-hidden"></a>
### Добавление скрытого поля

Способы добавления скрытого поля в поисковую форму:

* C помощью элемента `hidden`, размещенного в поле `content`. <br> Элемент реализует скрытое поле.
> Чтобы использовать опциональный элемент, укажите его в зависимостях блока на проектном уровне.

* C помощью поля `hidden` (шорткат). Поле содержит набор пар вида «name:value».

```javascript
{
    block: 'search2',
    ...
    hidden: {
        name: 'Finn',
        kind: 'Human'
    }
}
// эквивалентно
{
    block: 'search2',
    content: [
        ...
        {elem: 'hidden', attrs: {name: 'name', value: 'Finn'}},
        {elem: 'hidden', attrs: {name: 'kind', value: 'Human'}}
    ]
}
```

<a name="mods"></a>
### Модификаторы блока

<a name="mods-template"></a>
#### Модификатор `template`

Задает шаблон с контентом по умолчанию для желтой поисковой стрелки. Значения полей определены в шаблоне ([BEMHTML](../../common.blocks/search2/_template/search2_template_websearch.bemhtml.js)/[BH](../../common.blocks/search2/_template/search2_template_websearch.bh.js)).

> Чтобы использовать опциональный модификатор `template`, укажите его в зависимостях блока на проектном уровне.

Способ установки: BEMJSON.<br>
Допустимое значение: `websearch`.

Стрелка с контентом по умолчанию:

```js
{
    block: 'search2',
    url: 'https://yandex.ru/yandsearch',
    mods: {
        template: 'websearch'
    }
}
```

<a name="mods-theme"></a>
#### Модификатор `theme`

Задает стилевое оформление для желтой поисковой стрелки. Сейчас стили содержат только максимальную ширину поля ввода (`550px`).
Оформление стрелки определяется модификатором `theme` со значением `websearch` блоков [`input`](../input/input.ru.md#mods-theme-websearch),
[`button`](../button/button.ru.md#mods-theme-websearch), [`button2`](../button2/button2.ru.md#mods-theme)

<a name="fields"></a>
### BEMJSON-поля блока

<a name="fields-input"></a>
#### Поле `input`

Тип: BEMJSON.

Определяет содержимое элемента `input`, который является контейнером для поля ввода поисковой формы.

<a name="fields-button"></a>
#### Поле `button`

Тип: BEMJSON.

Определяет содержимое элемента `button`, который является контейнером для кнопки поисковой формы.

<a name="fields-label"></a>
#### Поле `label`
Тип: String.

Определяет значение атрибута `aria-label`, который используется в качестве ярлыка для программ экранного доступа.

Пример:

```js
{
    block: 'search2',
    url: 'https://yandex.ru/search',
    label: 'Искать в Яндексе',
    input: {tag: 'input', attrs: {style: 'width: 100%;'}},
    button: {tag: 'button', attrs: {type: 'submit'}, content: 'Найти'}
}
```
