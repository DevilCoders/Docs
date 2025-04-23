# radiobox
Блок `radiobox` используется для создания радиогруппы — группы зависимых радиопереключателей ([элементы radio](#elems-radio)). Позволяет выбрать только один элемент из предложенного списка.

## Обзор

* [Объединение радиогрупп](#marge-radiobox)
* [Отложенная инициализация блока](#live)

### Модификаторы блока

| Модификатор        | Допустимые значения  | Способы установки | Описание
| ------------------ | -------------------- | ----------------- | ------------------
| [theme](#mods-theme) |`normal`, `pseudo`| BEMJSON, JS | **Обязательный**. Стилевое оформление блока. |
| [size](#mods-size) |	`s`, `m` | BEMJSON, JS | **Обязательный**. Размер блока. |
| [disabled](#mods-disabled) |`yes` | BEMJSON, JS | Неактивное состояние блока. |


### BEMJSON-поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [name](#fields-value)| String| **Обязательное**. Уникальное имя радиогруппы. По умолчанию устанавливается в значение HTML-атрибута `name` всех радиопереключателей ([элементы radio](#elems-radio)). |
| [value](#fields-value)| String| Значение `value`, предварительно выбранного радиопереключателя. Устанавливается на этапе инициализации блока. По умолчанию выбран первый радиопереключатель группы.|


<a name="elems-short"></a>
### Элементы блока

| Элемент | Описание |
| --------| -------- |
| [radio](#elems-radio) | Радиопереключатель. |


## Подробнее

### Модификаторы блока

<a name="mods-theme"></a>
#### Модификатор `theme`

Задает стилевое оформление всем радиопереключателям в группе.

Способы установки: BEMJSON, JS.

Допустимые значения| Описание
--- | ---
`normal` | Типовая тема оформления.
`pseudo` | Радиопереключатели с прозрачным фоном. Используется для размещения на цветном фоне страницы.

**normal**

```js
{
    block: 'radiobox',
    mods: {theme: 'normal', size: 'm' },
    name: 'bla',
    value: 'val-1',
    content: [
        {
            elem: 'radio',
            content: 'Радио 1',
            controlAttrs: {value: 'val-1'}
        },'&nbsp;&nbsp;',
        {
            elem: 'radio',
            content: 'Радио 2',
            controlAttrs: {value: 'val-2'}
        },'&nbsp;&nbsp;',
        {
            elem: 'radio',
            content: 'Радио 3',
            controlAttrs: {value: 'val-3'}
        }
    ]
}
```
**pseudo**

```js
{
    block: 'radiobox',
    mods: {theme: 'pseudo', size: 'm' },
    name: 'bla',
    value: 'val-1',
    content: [
        {
            elem: 'radio',
            content: 'Радио 1',
            controlAttrs: {value: 'val-1'}
        },'&nbsp;&nbsp;',
        {
            elem: 'radio',
            content: 'Радио 2',
            controlAttrs: {value: 'val-2'}
        },'&nbsp;&nbsp;',
        {
            elem: 'radio',
            content: 'Радио 3',
            controlAttrs: {value: 'val-3'}
        }
    ]
}
```

<a name="mods-size"></a>
#### Модификатор `size`

Задает размер всем радиопереключателям в группе.

Способы установки: BEMJSON, JS.<br>
Допустимые значения: `s`, `m`.

**s**

```js
{
    block: 'radiobox',
    mods: {theme: 'normal', size: 's' },
    name: 'bla',
    value: 'val-1',
    content: [
        {
            elem: 'radio',
            content: 'Радио 1',
            controlAttrs: {value: 'val-1'}
        },'&nbsp;&nbsp;',
        {
            elem: 'radio',
            content: 'Радио 2',
            controlAttrs: {value: 'val-2'}
        },'&nbsp;&nbsp;',
        {
            elem: 'radio',
            content: 'Радио 3',
            controlAttrs: {value: 'val-3'}
        }
    ]
}
```

**m**

```js
{
    block: 'radiobox',
    mods: {theme: 'normal', size: 'm' },
    name: 'bla',
    value: 'val-1',
    content: [
        {
            elem: 'radio',
            content: 'Радио 1',
            controlAttrs: {value: 'val-1'}
        },'&nbsp;&nbsp;',
        {
            elem: 'radio',
            content: 'Радио 2',
            controlAttrs: {value: 'val-2'}
        },'&nbsp;&nbsp;',
        {
            elem: 'radio',
            content: 'Радио 3',
            controlAttrs: {value: 'val-3'}
        }
    ]
}
```

<a name="mods-disabled"></a>
#### Модификатор `disabled`

Все радиопереключатели (элементы `radio`) в группе и их метки недоступны пользователю. Каждому радиопереключателю будет установлен модификатор `disabled` со значением `yes`.

Способы установки: BEMJSON, JS.<br>
Допустимое значение: `yes`.


```js
{
    block: 'radiobox',
    mods: {size: 's', disabled: 'yes', theme: 'normal'},
    name: 'test',
    content: [
        {
            elem: 'radio',
            elemMods: {checked: 'yes'},
            content: 'только друзьям',
            controlAttrs: {value: 'val-1'}
        },'&nbsp;',
        {
            elem: 'radio',
            content: 'только мне',
            controlAttrs: {value: 'val-2'}
        },'&nbsp;',
        {
            elem: 'radio',
            content: 'виден всем',
            controlAttrs: {value: 'val-3'}
        }
    ]
}
```

### BEMJSON-поля блока

<a name="#fields-value"></a>
#### Поле `value`

Определяет значение выбранного радиопереключателя. Должно совпадать со значением `value` поля `controlAttrs` только одного из элементов `radio` блока. По умолчанию выбран первый радиопереключатель группы.

На этапе инициализации блока выбранному радиопереключателю автоматически устанавливается модификатор элемента `checked` со значением `yes`.

```js
{
    block: 'radiobox',
    mods: {size: 'm', theme: 'normal'},
    name: 'bla',
    value: 'val-2',
    content: [
        {
            elem: 'radio',
            content: 'Радио 1',
            controlAttrs: {value: 'val-1'}
        },
        '&nbsp;&nbsp;&nbsp;&nbsp;',
        {
            elem: 'radio',
            content: 'Радио 2',
            controlAttrs: {value: 'val-2'}
        },
        '&nbsp;&nbsp;&nbsp;&nbsp;',
        {
            elem: 'radio',
            content: 'Радио 3',
            controlAttrs: {value: 'val-3'}
        }
    ]
}
```

### Элементы блока

<a name="elems-radio"></a>
#### Элемент `radio`

Определяет радиопереключатель в группе.

Функциональность основана на нативном переключателе `<input type="radio">`, который скрыт. В версиях браузера MSIE ниже 8 деградирует до нативного переключателя.


### Модификаторы элемента `radio`

| Модификатор        | Допустимые значения  | Способы установки | Описание
| ------------------ | -------------------- | ----------------- | ------------------
| [checked](#mods-checked) |`yes` | BEMJSON, JS | Выбранный элемент. Выставляется только для одного радиопереключателя. Также может быть установлен предварительно, на этапе инициализации блока, через значение  `value` радиогруппы. По умолчанию выбран первый радиопереключатель группы.  |
| [disabled](#mods-disabled) |`yes` | BEMJSON, JS | Неактивное состояние элемента. |
| [focused](#mods-focused) | `yes` | JS | Фокус на элементе. |

Переход по элементам радиогруппы в фокусе осуществляется клавишами: ** ←, ↑, →, ↓ **.

```js
{
    block: 'radiobox',
    mods: {size: 's', theme: 'normal'},
    name: 'test',
    value: 'val-1',
    content: [
        {
            elem: 'radio',
            elemMods: {checked: 'yes'},
            content: 'checked',
            controlAttrs: {value: 'val-1'}
        },'&nbsp;',
        {
            elem: 'radio',
            elemMods: {focused: 'yes'},
            content: 'focused',
            controlAttrs: {value: 'val-2'}
        },'&nbsp;',
        {
            elem: 'radio',
            elemMods: {disabled: 'yes'},
            content: 'disabled',
            controlAttrs: {value: 'val-3'}
        },'&nbsp;',
        {
            elem: 'radio',
            elemMods: {disabled: 'yes', checked: 'yes'},
            content: 'disabled+checked',
            controlAttrs: {value: 'val-3'}
        }
    ]
}
```

### BEMJSON-поля элемента `radio`

| Поле | Тип | Описание |
| ---- | --- | -------- |
| `value`| String| **Обязательное**. Значение HTML-атрибута `value`. Уникальное для каждого элемента `radio` радиогруппы.|
| `content` | String | Текст метки радиопереключателя. |
|`controlAttrs` | Object | Дополнительные HTML-атрибуты для радиопереключателя (совпадают с атрибутами нативного переключателя): <ul><li>`value {String}` — **Обязательное**. Значение HTML-атрибута `value`. Уникальное для каждого элемента `radio` радиогруппы.</li><li>`name {String}` — Значение HTML-атрибута `name`. Передается из поля `name` блока `radiobox`. Одинаковое для всех элементов радиогруппы.</li><li>`id {String}` — Уникальный идентификатор. Генерируется автоматически, если явно не задан. Используется для связи метки `<label for="значение_id">` с соответствующим `<input type="radio" id="значение_id">`. </li><li>`tabindex {Number}` — Значение HTML-атрибута `tabindex`.</li></ul> |


<a name="marge-radiobox"></a>
### Объединение радиогрупп

Несколько блоков `radiobox` можно объединить в единую радиогруппу. Это позволит выбрать только один элемент из общей совокупности элементов этих радиогрупп.

Для этого нужно каждой из объединяемых радиогрупп:

* в JS-параметрах указать одинаковое значение параметра `id` (произвольная строка);
* указать одинаковое значение в поле `name`. Все радиопереключатели с одинаковым значением `name`, находятся в одной радиогруппе и обрабатываются вместе.

В результате при инициализации блоков создается один JS-объект, поле `{jQuery} domElem` которого содержит ссылки на DOM-узлы радиогрупп.

Идентификатор `id` используется только в момент инициализации экземпляра блока.
Значение `id` должно быть уникальным в пределах экземпляров одного блока.
Радиогруппы могут располагаться в произвольном месте страницы.
[Подробнее о распределенных блоках]( https://github.com/bem/bem-core/blob/v1/common.docs/i-bem-js/i-bem-js.ru.md#%D0%9E%D0%B4%D0%B8%D0%BD-js-%D0%B1%D0%BB%D0%BE%D0%BA-%D0%BD%D0%B0-%D0%BD%D0%B5%D1%81%D0%BA%D0%BE%D0%BB%D1%8C%D0%BA%D0%B8%D1%85-html-%D1%8D%D0%BB%D0%B5%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%85).

```js
[{
    block: 'radiobox',
    js: {id: 'radio-group'},
    mods: {size: 's', theme: 'normal'},
    name: 'test',
    value: 'val-2',
    content: [
        {
            elem: 'radio',
            content: 'только друзьям',
            controlAttrs: {value: 'val-1'}
        },'&nbsp;',
        {
            elem: 'radio',
            content: 'только мне',
            controlAttrs: {value: 'val-2'}
        }
    ]
}, '&nbsp;',
{
    block: 'radiobox',
    js: {id: 'radio-group'},
    mods: {size: 's', theme: 'normal'},
    name: 'test',
    content: [
        {
            elem: 'radio',
            content: 'виден всем',
            controlAttrs: {value: 'val-3'}
        }
    ]
}]
```

<a name="live"></a>
### Отложенная инициализация блока

Чтобы снизить нагрузку на браузер и повысить его производительность при большом количестве блоков на странице, используется отложенная инициализация блока.

Способы включения отложенной инициализации:

* **Локально** – для конкретного экземпляра блока `radiobox`.
Достаточно в BEMJSON-декларации блока указать JS-параметр `live` со значением `true`. Значение по умолчанию: `false` (автоматическая инициализация блока при загрузке страницы, то есть после наступления события `domReady`).

```javascript
{
    block: 'radiobox',
    js: { live: true }
    ...
}
```

* **Глобально** – для всех блоков `radiobox` проекта.
В этом случае, на уровне своего проекта нужно доопределить `BEMHTML`-шаблон блока
`radiobox/radiobox.bemhtml.js` следующим образом:

```javascript
block('radiobox').js()(function() {
    return this.extend({live: true}, this.ctx.js);
});
```

для `BH`-шаблона `radiobox/radiobox.bh.js` доопределение будет таким:

```javascript
module.exports = function(bh) {
    bh.match('radiobox', function(ctx) {
        ctx.js(ctx.extend({live: true}, ctx.js()));
    });
};
```

Все блоки `radiobox` проекта станут инициализироваться отложено, кроме блоков с явно отключенной live-инициализацией в BEMJSON через JS-параметр `live: false`:

```javascript
{
    block: 'radiobox',
    js: { live: false }
    ...
}
```

В этих случаях радиопереключатель инициализируется сразу.
