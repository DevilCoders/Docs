# attach

Используется для выбора файла, предназначенного для отправки на сервер.

## Обзор блока

### Модификаторы блока

| Модификатор | Допустимые значения | Способы использования | Описание |
| ----------- | ------------------- | -------------------- | -------- |
| <a href="#theme">theme</a>&#42; | `'normal'` | `BEMJSON` | Стилевое оформление. |
| <a href="#size">size</a>&#42; | `'s'`, `'m'` | `BEMJSON` | Размер блока. |
| <a href="#disabled">disabled</a> | `yes` | `BEMJSON`, `JS` | Неактивное состояние. |
| <a href="#use">use</a> | `button2` | `BEMJSON`, `JS` | Тип кнопки. Кнопка будет реализована блоком <a href="../button/button2.ru.md">button2</a>. |

&#42; Обязательный модификатор.

### Специальные поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| <a href="#name">name</a> | `String` | Уникальное имя блока. |
| <a href="#id">id</a> | `String` | Уникальный идентификатор кнопки. |
| <a href="#text">text</a> | `String`| Текст кнопки. |
| <a href="#button">button</a> | `BEMJSON` | API кнопки для выбора файла. |
| <a href="#holder">holder</a> | `Boolean`, `String` | Текст сообщения, когда файл не выбран. |
| <a href="#tab">tabindex</a> | `Number` | Последовательность перехода между контролами при нажатии на `Tab`. |

## Описание

Блок `attach` использует функциональность нативного контрола `<input type="file" >`.

По умолчанию визуально представлен:

* кнопкой ([button](../button/button.ru.md)), вызывающей системное окно загрузки файла;
* текстовым сообщением "Файл не выбран".

> **Примечание** В блок `attach` добавлена возможность использовать кнопку [button2](../button/button2.ru.md). Для этого необходимо определить модификатор `attach_use_button2`.

После выбора файла отображаются:

* имя файла (элемент `text`);
* крестик для отмены выбора (элемент `reset`).

Реализация блока не позволяет:

* прикреплять несколько файлов;
* перетаскивать элементы (`drag-and-drop`).

### Пример JSON

```js
{
    block: 'attach',
    mods: { size: 'm', theme: 'normal' },
    name: 'attach-logo',
    id: 'attach-logo',
    text: 'Выберите файл',
    holder: true || 'Файл не выбран',
    tabindex: 2
}
```

### Модификаторы блока

<a name="theme"></a>

#### Модификатор `theme`

Допустимое значение: `'normal'`.

Отвечает за стилевое оформление блока.

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' }
    // ...
}
```

<a name="size"></a>

#### Модификатор `size`

Допустимые значения: `'s'`, `'m'`.

Задает размер блока.

**s**

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 's' }
}
```

**m**

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' }
}
```

<a name="disabled"></a>

#### Модификатор `disabled`

Допустимое значение: `'yes'`.

Отвечает за неактивное состояние, при котором блок виден, но недоступен для действий пользователя.

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm', disabled: 'yes' }
}
```

<a name="use"></a>

#### Модификатор `use`

Допустимое значение: `'button2'`.

Определяет кнопку, которая отображается с помощью блока [button2](../button/button2.ru.md).

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 's', use: 'button2' }
}
```

> **Примечание** Для обратной совместимости блок `button` также будет попадать в сборку даже при использовании модификатора `attach_use_button2`. Поэтому если важно, чтобы в сборку попадала только нужная реализация `button2`, необходимо отменить зависимости от блока `button` на текущем уровне переопределения:
>
> *Файл `attach.deps.js`*
>
> ```js
>({
>    block: 'attach',
>    noDeps: [
>        { block: 'button' },
>        { block: 'button', elem: 'text' },
>        { block: 'button', mods: { theme: 'normal', size: ['s', 'm'], disabled: 'yes'} }
>    ]
> })
> ```

### Специальные поля блока

<a name="name"></a>

#### Поле `name`

Тип: `String`.

Определяет уникальное имя блока.

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' },
    name: 'attach-logo'
}
```

> **Примечание** По умолчанию поле `name` имеет значение `attachment` (в случае, если явно не задано в BEMJSON).

<a name="id"></a>

#### Поле `id`

Тип: `String`.

Определяет уникальный идентификатор блока.

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' },
    id: 'attach-logo'
}
```

<a name="text"></a>

#### Поле `text`

Тип: `String`.

Задает текст кнопки. Если поле не определено, по умолчанию используется текст «Выбрать файл».

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' },
    text: 'Выберите файл'
}
```

> **Примечание** Поле `text` позволяет определить текст кнопки и подходит для решения большинства задач, однако через него нельзя задать произвольный BEMJSON. Если необходимо внутри блока `attach` определить некую HTML-разметку, нужно использовать поле `content`. В этом случае специальные поля `text`, `holder`, `button` будут проигнорированы.

<a name="button"></a>

#### Поле `button`

Тип: `BEMJSON`.

Определяет внешний вид и тип кнопки (прокси API для `button` и `button2`):

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' },
    button: {
        mods: { size: 'xs', theme: 'action' },
        content: [
            {
                 block: 'image',
                 mix: [ { block: 'button', elem: 'icon',  elemMods: {'16': 'settings'} } ],
                 alt: 'twitter'
            },
            'Twitter'
       ]
    }
}
```

<a name="holder"></a>

#### Поле `holder`

Тип: `String`, `Boolean`.

Определяет текст сообщения, когда файл не выбран:

**String:**

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' },
    holder: 'Выберите файл'
}
```

**Boolean:**

```js
{
    block: 'attach',
    mods: { theme: 'normal', size: 'm' },
    holder: true // текст по умолчанию «файл не выбран»
}
```

<a name="tab"></a>

#### Поле `tabindex`

Тип: `Number`.

Определяет порядок получения фокуса при переходе между контролами с помощью клавиши `Tab`.

```js
{
  block: 'attach',
  mods: { theme: 'normal', size: 'm' },
  tabindex: 2
}
```
