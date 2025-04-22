# Menu
Используется для создания различных типов меню. [Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/menu)

## Использование
```jsx
var Menu = require('bem-react/lib/Menu');

var options = [
    {
        title: 'Group B',
        group: [
            {
                text: 'Good',
                val: 'good'
            },
            {
                text: 'Bye',
                val: 'bye'
            }
        ]
    },
    {
        text: 'Some disabled item',
        val: 'noop',
        disabled: true
    },
    {
        text: 'Some selected item',
        val: 'what?'
    }
];

var handleClick = function(payload) {
    console.log('Clicked on "%s"', payload.value);
};

<Menu options={options} onClick={handleClick} />
```

## Параметры

#### disabled `Boolean`
Неактивное состояние

#### mode `String`
Режим выбора пунктов меню: `check`, `radio`, `radio-check`

[Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/menu/docs/#mode)

#### onChange(payload)
Колбэк изменения текстового поля
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **value** `Array` `Number` `String`  
    Выбранные значения меню

#### onClick(payload)
Колбэк клика на пункт меню
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **value** `Number` `String`  
    Значение пункта меню

#### options `Array`
Массив пунктов меню
- **item** `Object`
  - **disabled** `Boolean`  
    Неактивное состояние
  - **text** `String`  
    Название элемента
  - **val** `Number` `String`  
    Значение элемента

Пункты меню могут быть организованы в группы
- **item** `Object`
  - **title** `String`  
    Название группы
  - **group** `Array`  
    Массив элементов

#### size `String`
Размер меню: `s`, `m`, `l`, `xl`

#### theme `String`
Тема: `islands`

#### val `Array` `Number` `String`
Выбранные значения по умолчанию
