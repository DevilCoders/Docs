# Checkbox
Используется для создания переключателей. [Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/checkbox/)

## Использование
```jsx
var Checkbox = require('bem-react/lib/Checkbox');

var handleChange = function(payload) {
    var state = payload.checked ? 'checked' : 'unchecked';

    console.log('Checkbox is %s with value: %s', state, payload.value);
};

<Checkbox size="l" text="Some checkbox" tabIndex={5}
    onChange={handleChange} name="check1" value={123456} />
```

## Параметры

#### disabled `Boolean`
Неактивное состояние

#### id `String`
Уникальный идентификатор

#### name `String`
Название чекбокса

#### onChange(payload)
Колбэк нажатия кнопки
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **value** `String` `Number`  
    Значение чекбокса
  - **checked** `Boolean`
    Состояние чекбокса

#### size `String`
Размер чекбокса: `m`, `l`

#### tabIndex `Number`
Последовательность перехода фокуса

#### text `String`
Текст подписи к чекбоксу

#### theme `String`
Тема: `islands`

#### val `String` `Number`
Значение, отправляемое на сервер
