# Textarea
Используется для создания текстовой области. [Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/textarea/)

## Использование
```jsx
var Textarea = require('bem-react/lib/Textarea');

var handleChange = function(payload) {
    console.log('User typed:', payload.value);
};

var handleKeyDown = function(payload) {
    if (payload.keyCode === 27) {
        console.log('Esc pressed');
    }
};

<Textarea id="sample-textarea" name="sample" size="l"
    placeholder="Enter some" onChange={handleChange}
    onKeyDown={handleKeyDown} />
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

#### disabled `Boolean`
Неактивное состояние*

#### id `String`
Уникальный идентификатор

#### name `String`
Имя текстовой области

#### onChange(payload)
Колбэк изменения текстовой области
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **value** `String`  
    Значение текстовой области


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
Размер текстовой области: `s`, `m`, `l`, `xl`

#### tabIndex `Number`
Последовательность перехода фокуса

#### theme `String`
Тема: `islands`

#### val `String` `Number`
Содержимое текстовой области, указанное по умолчанию

#### width `String`
Ширина текстовой области: `available`
