# Radiogroup
Используется для создания радио-переключателей. [Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/radio/)

## Использование
```jsx
var Radiogroup = require('bem-react/lib/Radiogroup');

var options = [
    {
        text: 'Radio 1',
        val: 1
    },
    {
        text: 'Radio 2',
        val: 2
    },
    {
        text: 'Radio 3',
        val: 3,
        disabled: true
    }
];

var handleChange = function(payload) {
    console.log('User selected %i', payload.value);
};

<Radiogroup name="radio1" options={options} size="l"
    type="line" onChange={handleChange} val={2} />
```

## Параметры

#### disabled `Boolean`
Неактивное состояние

#### name `String`
Название контрола

#### onChange(payload)
Колбэк изменения значения радиогруппы
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **value** `String` `Number`  
    Значение, отправляемое на сервер

#### options `Array`
Массив радио-переключателей
- **item** `Object`
  - **disabled** `Boolean`  
    Неактивное состояние
  - **text** `String`  
    Название переключателя
  - **val** `Number` `String`  
    Значение, отправляемое на сервер

#### size `String`
Размер переключателя: `m`, `l`

#### theme `String`
Тема: `islands`

#### type `String`
Тип радио-переключателей: `button`, `line`

#### val `String` `Number`
Значение выбранного переключателя
