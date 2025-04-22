## m-calendar

Блок, вызывающий по клику на `b-form-input` или `b-form-button` блок `m-datepicker` внутри `b-popupa` и позволяющий отобразить выбранные даты в `b-form-input` или `b-form-button`.

  * Модификатор `toggler` в значениях `input` или `button` управляет отображением контрола, который вызовет попап.
  * JS-параметр `defaultText` отразится как `placeholder` инпута или станет значением кнопки.
  * JS-параметр `value` устанавливает выбранную дату.
  * JS-параметр `specialDates` аналогичен одноимённому параметру в [m-datepicker](../m-datepicker/m-datepicker.ru.md).
  * JS-параметр `limits` аналогичен одноимённому параметру в [m-datepicker](../m-datepicker/m-datepicker.ru.md).
  * специальные поля `size` и `theme` конфигурируют соответствующие модификаторы блоков `b-form-input` или `b-form-button` из Лего.

### m-calendar_type_month

Рендерятся контролы, вызывающие попап (кнопка или инпут), в попапе отображается месяц, доступны выбор даты, выбор месяца и года.

  * JS-параметр `keyboard` принимает true/false и позволяет включить управление календарем с клавиатуры.
  * JS-параметр `value` должен содержать строку даты в формате `ISOString`.
  * JS-параметр `date` отобразит месяц и год, указанный в значении в формате `ISOString`, но дата выбрана не будет. Можно использовать. сокращенную запись: `js: { date: '2012-10' }` или полную, конкретная дата не влияет на результат.
  * JS-параметры `value` и `date` можно выставить одновременно, тогда дата выставится из `value`, но при открытии попапа покажется месяц и год из `date`.
  *  Можно раскрасить определенные дни с помощью JS-параметра `specialDays` или метода `setSpecialDays(dates)` (см. API).

```js
{
    block: 'm-calendar',
    mods: { toggler: 'input', type: 'month' },
    js: {
        defaultText: 'выбери дату',
        date: '2012-09',
        specialDays: {
            '2012-10-02': { background: '#f00', title: 'вау, выходной!', 'color': '#fff' },
            '2012-10-05': { background: '#060', title: 'фак!' },
            '2012-11-10': { background: '#060', title: 'йоу' }
        }
    },
    size: 'm',
    theme: 'grey',
}
```

### Примеры с инпутом и кнопкой, дата не выбрана

```js
[{
    block: 'm-calendar',
    mods: { toggler: 'input', type: 'month' },
    js: { defaultText: 'выбери дату' },
    size: 'm',
    theme: 'grey'
},
{
    block: 'm-calendar',
    mods: { toggler: 'button', type: 'month' },
    js: { defaultText: 'выбери дату' },
    size: 'l',
    theme: 'grey'
}]
```

### Примеры с инпутом и кнопкой, дата выбрана

```js
[{
    block: 'm-calendar',
    mods: { toggler: 'input', type: 'month' },
    js: { value: '2012-10-21', defaultText: 'выбери дату' },
    size: 'm',
    theme: 'grey'
},
{
    block: 'm-calendar',
    mods: { toggler: 'button', type: 'month' },
    js: { value: '2012-10-21', defaultText: 'выбери дату' },
    size: 'l',
    theme: 'grey'
}]
```

### Примеры с ограничением ввода дат

```js
[{
    block: 'm-datepicker',
    mods: { type: 'month' },
    js: {
        date: '2014-11',
        limits: {
            min: '2014-10-03',
            max: '2015-01-20'
        }
    }
}]
```

### API

  * `getDate` — возвращает объект `Date`, если дата выбрана и `false`, если нет.
  * `setDate` — принимает в качестве аргумента дату в формате ISOString, устанавливает дату.
  * `clearDate` — удаляет выбранное значение даты, метод `getDate` до повторной установки даты вернет `false`.
  * `setSpecialDays(dates)` — принимает объект, описывающий день, который нужно отметить, цвет фона, цвет текста и строку, которая попадет в атрибут `title` ячейки с датой. Когда отобразится месяц, в котором есть указанные даты, они будут отмечены.
  * `setMaxDate(date)`, `setMinDate(date)` и `setLimits(min, max)` аналогичны одноимённым методам в `m-datepicker`.

```javascript
{
    '2012-10-02': { background: '#f00', title: 'вау, выходной!', 'color': '#fff' }
}
```

  * при выборе даты генерируется BEM-событие `change`, где в `event.data` находится результат `getDate`.

## m-calendar_type_scope

Рендерятся контролы, вызывающие попап (кнопка или инпут), в попапе отображается промежуток дат, доступны выбор промежутка дат:

  * JS-параметр `scope` должен содержать строку объект в формате `{ from: ISOString, to: ISOString }`.
  * JS-параметр `value` должен содержать строку объект в формате `{ from: ISOString, to: ISOString }`.

### Примеры с инпутом и кнопкой, дата не выбрана

```js
[{
    block: 'm-calendar',
    mods: { toggler: 'input', type: 'scope' },
    js: {
        scope: {
            from: '2012-09-13',
            to: '2013-02-07'
        },
        defaultText: 'выбери дату'
    },
    size: 'm',
    theme: 'grey'
},
{
    block: 'm-calendar',
    mods: { toggler: 'button', type: 'scope' },
    js: {
        scope: {
            from: '2012-09-13',
            to: '2013-02-07'
        },
        defaultText: 'выбери дату'
    },
    size: 'm',
    theme: 'grey'
}]
```

### Примеры с инпутом и кнопкой, дата выбрана

```js
[{
    block: 'm-calendar',
    mods: { toggler: 'input', type: 'scope' },
    js: {
        value: {
            from: '2012-10-21',
            to: '2012-10-27'
        },
        scope: {
            from: '2012-09-10',
            to: '2013-02-07'
        },
        defaultText: 'выбери дату'
    },
    size: 'l',
    theme: 'grey'
},
{
    block: 'm-calendar',
    mods: { toggler: 'button', type: 'scope' },
    js: {
        value: {
            from: '2012-10-21',
            to: '2012-10-27'
        },
        scope: {
            from: '2012-09-10',
            to: '2013-02-07'
        },
        defaultText: 'выбери дату'
    },
    size: 'l',
    theme: 'grey'
}]
```

### API

  * `getDate` — возвращает объект `{ from: объект Date, to: объект Date }`, если дата выбрана и `false`, если нет.
  * `setDate` — принимает в качестве аргумента дату в формате `{ from: ISOString, to: ISOString }`, устанавливает дату.
  * `clearDate` — удаляет выбранное значение даты, метод `getDate` до повторной установки дат вернет `false`.

## m-calendar_has_clear

Доступна кнопка очистки выбранной даты (дата может быть как установлена, так и отсутствовать).

## m-calendar_type_month

```js
{
    block: 'm-calendar',
    mods: { type: 'month', has: 'clear' },
    js: { value: '2012-10-21' }
}
```

## m-calendar_type_scope

```js
{
    block: 'm-calendar',
    mods: { toggler: 'button', type: 'scope', has: 'clear' },
    js: {
        value: {
            from: '2012-10-21',
            to: '2012-10-27'
        },
        scope: {
            from: '2012-09-10',
            to: '2013-02-07'
        },
        defaultText: 'выбери дату'
    },
    size: 'l',
    theme: 'grey'
}
```
