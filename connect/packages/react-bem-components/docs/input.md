# Input
Используется для создания текстового поля. [Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/input/)

## Использование
```jsx
var Input = require('bem-react/lib/Input');

var handleChange = function(payload) {
    console.log('User typed:', payload.value);
};

<Input id="sample-input" name="sample" size="l" hasClear={true}
    autoComplete={true} maxLength={20} type="search"
    placeholder="Enter some" onChange={handleChange} />
```

## Методы

#### blur()
Убирает фокус с контрола

#### focus()
Устанавливает фокус на контрол

#### select()
Устанавливает фокус и выделяет содержимое внутри контрола

#### value()
Возвращает текущее значение контрола

## Параметры

#### autoComplete `Boolean`
Браузерное автозаполнение

#### disabled `Boolean`
Неактивное состояние

#### hasClear `Boolean`
Крестик для очистки содержимого

#### id `String`
Уникальный идентификатор

#### maxLength `Number`
Максимальное количество вводимых символов

#### name `String`
Имя текстового поля

#### onChange(payload)
Колбэк изменения текстового поля
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **value** `String`  
    Значение поля


#### onKeyDown(payload)
Колбэк нажатия клавиши
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **keyCode** `Number`  
    Числовой код
  - **value** `String`  
    Значение поля

#### onBlur(payload)
Колбэк потери фокуса
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **value** `String`  
    Значение поля

#### onFocus(payload)
Колбэк установки фокуса
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **value** `String`  
    Значение поля

#### placeholder `String`
Текст-подсказка

#### size `String`
Размер текстового поля: `s`, `m`, `l`, `xl`

#### tabIndex `Number`
Последовательность перехода фокуса

#### theme `String`
Тема: `islands`

#### type `String`
Тип текстового поля: `password`, `search`

#### val `String` `Number`
Содержимое поля, указанное по умолчанию

#### width `String`
Ширина текстового поля: `available`
