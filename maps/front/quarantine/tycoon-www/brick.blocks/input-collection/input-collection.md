# input-collection

Блок для построения динамической коллекции инпутов.

## Обзор блока

### Модификаторы блока

| Модификатор | Допустимые значения | Способы использования | Описание |
| ----------- | ------------------- | -------------------- | -------- |
| <a href="#theme">theme</a> | <code>'islands'</code> | <code>BEMJSON</code> | Стилевое оформление. |
| <a href="#size">size</a> | <code>'m'</code> | <code>BEMJSON</code> | Размер текстовых полей. Используется только с модификатором <a href="#theme">theme в значении islands</a>.|

### Специализированные поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| <a href="#name">name</a> | <code>String</code> | Уникальное имя для группы инпутов. |
| <a href="#val">val</a> | <code>String</code>, <code>Number</code> | Содержимое главного поля ввода, указанное по умолчанию. |
| <a href="#placeholder">placeholder</a> | <code>String</code> | Подсказка в текстовых полях. |
| <a href="#maxLength">maxLength</a> | <code>String</code> | Максимальное количество вводимых символов. |
| <a href="#autocomplete">autocomplete</a> | <code>Boolean</code> | Браузерное автозаполнение в текстовом поле. |

## Описание блока

Блок `input-collection` служит для создания динамической коллекции инпутов.

### Модификаторы блока

<a name="theme"></a>

#### Модификатор `theme`

Допустимое значение: `'islands'`.

Способ использования: `BEMJSON`.

Отвечает за стилевое оформление блока.

Необходимо использовать с модификатором <a href="#size">size</a>.

```js
{
    block : 'input-collection',
    mods : { theme : 'islands', size: 'm' },
    placeholder : 'Введите запрос'
}
```

<a name="size"></a>

#### Модификатор `size`

Допустимые значения для темы `islands`: `'m'`.

Способ использования: `BEMJSON`.

Необходимо использовать с модификатором <a href="#theme">theme</a> в значении `islands`.

Задает размер всем типам текстовых полей.

**m**

```js
{
    block : 'input-collection',
    mods : { theme : 'islands', size: 'm' },
    placeholder : 'Размер m'
}
```

### Специализированные поля блока

<a name="name"></a>

#### Поле `name`

Тип: `String`.

Определяет уникальное имя группы инпутов.

```js
{
    block : 'input-collection',
    mods : { theme : 'islands', size: 'm' },
    name : 'Statistics'
}
```

<a name="val"></a>

#### Поле `val`

Тип данных: `String`.

Определяет содержимое первого поля ввода.

```js
{
    block : 'input-collection',
    mods : { theme : 'islands', size: 'm' },
    name : 'Statistics',
    val : 'Привет!'
}
```

<a name="placeholder"></a>

#### Поле `placeholder`

Тип данных: `String`.

Определяет текст подсказки в текстовых полях.

```js
{
    block : 'input-collection',
    mods : { theme : 'islands', size : 'm' },
    placeholder : 'Введите имя'
}
```

<a name="maxLength"></a>

#### Поле `maxLength`

Тип данных: `Number`.

Определяет максимальное количество вводимых символов.

```js
{
    block : 'input-collection',
    mods : { theme : 'islands', size : 'm' },
    placeholder : 'Введите имя',
    maxLength : 20
}
```

<a name="autocomplete"></a>

#### Поле `autocomplete`

Тип данных: `Boolean`.

Отвечает за включение / выключение автозаполнения текстового поля в браузере.

Если поле `autocomplete` не задано, автозаполнение включено.

Для отключения автозаполнения используйте значение `false`:

```js
{
    block : 'input-collection',
    mods : { theme : 'islands', size : 'm' },
    placeholder : 'Введите имя',
    autocomplete : false
}
```
