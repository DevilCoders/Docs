## m-datepicker_type_month
Выводится месяц, доступны выбор даты, выбор месяца и года.

### Базовый вариант, отображается текущий месяц, дата не выбрана

```js
{
    block: 'm-datepicker',
    mods: { type: 'month' },
    js: true
}
```

### Дата не выбрана, отображается месяц из JS-параметра date
(конкретная дата месяца не имеет значения и может быть опущена)

```js
{
    block: 'm-datepicker',
    mods: { type: 'month' },
    js: { date: '2012-10' }
}
```

### Дата выбрана, отображается месяц с выбранной датой

```js
{
    block: 'm-datepicker',
    mods: { type: 'month' },
    js: { value: '2012-10-21' }
}
```

### Дата выбрана, отображается месяц из JS-параметра date

```js
{
    block: 'm-datepicker',
    mods: { type: 'month' },
    js: { date: '2012-05', value: '2012-10-21' }
}
```

### Можно раскрасить определенные дни с помощью JS-параметра `specialDays` или метода `setSpecialDays(dates)` (см. API)

```js
{
    block: 'm-datepicker',
    mods: { type: 'month' },
    js: {
        value: '2012-10-21',
        specialDays: {
            '2012-10-02': { background: '#f00', title: 'вау, выходной!', 'color': '#fff' },
            '2012-10-05': { background: '#060', title: 'фак!' },
            '2012-11-10': { background: '#060', title: 'йоу' }
        }
    }
}
```

### Можно ограничить максимальную и минимальную даты с помощью JS-параметра `limits`
или методов `setLimits(min, max)`, `setMinDate(date)` и `setMaxDate(date)` (см. API)

```js
{
    block: 'm-datepicker',
    mods: { type: 'month' },
    js: {
        value: '2012-10-21',
        limits: {
            min: '2012-10-02',
            max: '2012-10-25'
        }
    }
}
```

### API

  * `getDate` — возвращает объект `Date`, если дата выбрана и `false`, если нет.
  * `setDate` — принимает в качестве аргумента дату в формате ISOString, устанавливает дату. Принимает `boolean` (`doNotRebuild`) в качестве второго аргумента: если вы только что сгенерировали `m-datepicker` с нужными настройками и нужно только вызвать событие `change`, то нужно передать вторым аргументом `true`.
  * `clearDate` — удаляет выбранное значение даты, метод `getDate` до повторной установки даты вернет `false`.
  * `getSelectedDay` — возвращает `number` равный текущей выбранной дате (1—31) или `false`, если дата не выбрана.
  * `setSpecialDays(dates)` — принимает объект, описывающий день, который нужно отметить, цвет фона, цвет текста и строку, которая попадет в атрибут `title` ячейки с датой. Когда отобразится месяц, в котором есть указанные даты, они будут отмечены.
  * `setLimits(min, max)` — принимает в качестве аргументов даты в формате ISOString, устанавливает максимальную и минимальную.
  * `setMinDate(date)` — принимает в качестве аргумента дату в формате ISOString, устанавливает минимально возможную дату.
  * `setMaxDate(min, max)` — принимает в качестве аргумента дату в формате ISOString, устанавливает максимально возможную дату.
  * При выборе даты генерируется BEM-событие `change`, где в `event.data` лежит результат `getDate`.

```javascript
({
    '2012-10-02': { background: '#f00', title: 'вау, выходной!', 'color': '#fff' }
})
```

## m-datepicker_type_scope

Выводится промежуток дат `scope: { from: ISODate, to: ISODate }` и устанавливается промежуток `value: { from: ISODate, to: ISODate }`.

### Базовый вариант, отображается выбранный промежуток дат и промежуток дат выбран

```js
{
    block: 'm-datepicker',
    mods: { type: 'scope' },
    js: {
        scope: {
            from: '2012-09-13',
            to: '2013-02-07'
        }
    }
}
```

### Отображается выбранный промежуток дат, дата выбрана

```js
{
    block: 'm-datepicker',
    mods: { type: 'scope' },
    js: {
        value: {
            from: '2012-10-21',
            to: '2012-10-27'
        },
        scope: {
            from: '2012-09-10',
            to: '2013-02-07'
        }
    }
}
```

### API

  * `getDate` — возвращает объект `{ from: объект Date, to: объект Date }`, если дата выбрана и `false`, если нет.
  * `setDate` — принимает в качестве аргумента дату в формате `{ from: ISOString, to: ISOString }`, устанавливает дату. Принимает `boolean` (`doNotRebuild`) в качестве второго аргумента: если вы только что сгенерировали `m-datepicker` с нужными настройками и нужно только вызвать событие `change`, то нужно передать вторым аргументом `true`.
  * `clearDate` — удаляет выбранное значение даты, метод `getDate` до повторной установки дат вернет `false`.

## m-datepicker_has_clear

Доступна кнопка очистки выбранной даты (дата может быть как заранее установлена, так и отсутствовать).

## m-datepicker_type_month

```js
{
    block: 'm-datepicker',
    mods: { type: 'month', has: 'clear' },
    js: { value: '2012-10-21' }
}
```

## m-datepicker_type_scope

```js
{
    block: 'm-datepicker',
    mods: { type: 'scope', has: 'clear' },
    js: {
        value: {
            from: '2012-10-21',
            to: '2012-10-27'
        },
        scope: {
            from: '2012-09-10',
            to: '2013-02-07'
        }
    }
}
```

## m-datepicker_disable_change

Запрещено изменение месяца и выбор даты, только отображение установленного значения.

## m-datepicker_type_month

```js
{
    block: 'm-datepicker',
    mods: { type: 'month', disable: 'change' },
    js: { value: '2012-10-21' }
}
```

## m-datepicker_type_scope

```js
{
    block: 'm-datepicker',
    mods: { type: 'scope', disable: 'change' },
    js: {
        value: {
            from: '2012-10-21',
            to: '2012-10-27'
        },
        scope: {
            from: '2012-09-10',
            to: '2013-02-07'
        }
    }
}
```
