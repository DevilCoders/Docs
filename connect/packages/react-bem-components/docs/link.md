# Link
Используется для создания ссылок. [Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/link/)

## Использование
```jsx
var Link = require('bem-react/lib/Link');

var handleClick = function(payload) {
    console.log('User clicked on:', payload.url);
};

<Link size="xl" visible={true} url="http://ya.ru"
    onClick={handleClick} text="Click me" />
```

## Параметры

#### disabled `Boolean`
Неактивное состояние

#### onClick()
Колбэк клика по ссылке, срабатывает только в случае `pseudo={true}`
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **url** `String`  
    Адрес ссылки

#### pseudo `Boolean`
Запрещает переход по ссылке

#### size `String`
Размер ссылки: `s`, `m`, `l`, `xl`

#### tabIndex `Number`
Последовательность перехода фокуса

#### target `String`
Поведение ссылки: `_blank`, `_self`, `_parent`, `_top`

#### theme `String`
Тема: `islands`

#### title `String`
Текст всплывающей подсказки

#### url `String`
Адрес ссылки
