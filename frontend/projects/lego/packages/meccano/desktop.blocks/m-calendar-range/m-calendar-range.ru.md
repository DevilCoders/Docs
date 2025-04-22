## m-calendar-range

Блок для выбора периода дат с помощью двух контролов `m-calendar`.

  * Модификатор `toggler` в значениях `input` или `button` управляет отображением контрола, который вызовет попап.
  * Js-параметр `value` служит для предварительной установки даты в формате `ISOString`: `{ from: ISOString, to: ISOString }`. Для сброса значения контрола нужно установить значение 'Infinite' у соответствующего свойства. Оба значения обязательны к заполнению.
  * `placeholder` для `input` или текст по умолчанию для кнопок задается специальным полем `defaultText` содержащим объект `{ from: 'с', to: 'по' }`.
  * Специальное поле `label` должно содержать объект `{ from: 'с', to: 'по' }` — это текстовые пояснения для input, которые будут выведены рядом, например: `с [кнопка] по [кнопка]`.
  * Специальные поля `size` и `theme` конфигурируют соответствующие модификаторы блоков `b-form-input` или `b-form-button` из Лего.

### Примеры с инпутом и кнопкой, дата не выбрана

```js
[{
    block: 'm-calendar-range',
    mods: { toggler: 'input' },
    js: true,
    label: { from: 'с', to: 'по' },
    size: 'm',
    theme: 'grey'
},
{
    block: 'm-calendar-range',
    mods: { toggler: 'button' },
    js: true,
    label: { from: 'с', to: 'по' },
    size: 'm',
    theme: 'grey'
}]
```

### Примеры с инпутом и кнопкой, дата не выбрана, вместо `label` используем `defaultText`

```js
[{
    block: 'm-calendar-range',
    mods: { toggler: 'input' },
    js: true,
    defaultText: { from: 'с', to: 'по' },
    size: 'm',
    theme: 'grey'
},
{
    block: 'm-calendar-range',
    mods: { toggler: 'button' },
    js: true,
    defaultText: { from: 'с', to: 'по' },
    size: 'm',
    theme: 'grey'
}]
```


### Примеры с инпутом и кнопкой, дата выбрана

```js
[{
    block: 'm-calendar-range',
    mods: { toggler: 'input' },
    js: {
        value: {
            from: '2012-10-21',
            to: '2012-10-24'
        }
    },
    label: { from: 'с', to: 'по' },
    size: 'm',
    theme: 'grey'
},
{
    block: 'm-calendar-range',
    mods: { toggler: 'button' },
    js: {
        value: {
            from: '2012-10-21',
            to: '2012-10-24'
        }
    },
    label: { from: 'с', to: 'по' },
    size: 'm',
    theme: 'grey'
}]
```

### API

  * `getDate` возвращает объект `{ from: объект Date, to: объект Date }`, если дата выбрана и значение `'Infinite'` в соответствующих полях, если одна или обе даты не выбраны.
  * `setDate` принимает в качестве аргумента дату в формате `{ from: ISOString|'Infinite', to: ISOString|'Infinite' }`.
  * `clearDate` устанавливает в поля `from` и `to` значение `'Infinite'`, вызывает метод `clearDate` у каждого блока `m-calendar`, метод `getDate` до повторной установки дат вернет `{ from: 'Infinite', to: 'Infinite' }`, вызов `clearDate` c аргументом это алиас к `setDate` c этим же аргументом, например, `{ from: ISOString, to: 'Infinite' }` очистит дату `to` и установит дату `from`.
  * при выборе даты генерируется BEM-событие `change`, где в `event.data` находится результат `getDate`.
