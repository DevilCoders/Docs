# Select
Используется для создания выпадающего списка с возможностью одиночного или множественного выбора. [Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/select/)

## Использование
```jsx
var Select = require('bem-react/lib/Select');

var options = [
    {
        title: 'Group A',
        group: [
            {
                text: 'Hello',
                val: 'hello'
            },
            {
                text: 'World',
                val: 'world'
            }
        ]
    },
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
        text: 'Some disabled option',
        val: 'noop',
        disabled: true
    },
    {
        text: 'Some selected option',
        val: 'default'
    }
];

var handleChange = function(payload) {
    console.log('User selected %i item(s)', payload.value.length);
};

<Select options={options} placeholder="Nothing selected"
    mode="check" onChange={handleChange} val={['default']} />
```

## Параметры

#### disabled `Boolean`
Неактивное состояние

#### id `String`
Уникальный идентификатор

#### maxHeight `Number`
Максимальная высота выпадающего списка

#### mode `String`
Режим выбора пунктов выпадающего списка: `check`, `radio`, `radio-check`

[Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/select/docs/#mode)

#### name `String`
Имя выпадающего списка

#### onChange(payload)
Колбэк изменения текстового поля
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **value** `Array` `Number` `String`  
    Значение текстовой области

#### options `Array`
Массив элементов списка
- **item** `Object`
  - **disabled** `Boolean`  
    Неактивное состояние
  - **text** `String`  
    Название элемента
  - **val** `Number` `String`  
    Значение элемента

Элементы списка могут быть организованы в группы
- **item** `Object`
  - **title** `String`  
    Название группы
  - **group** `Array`  
    Массив элементов

#### placeholder `String`
Текст-подсказка, в случае, если ничего не выбрано. Используется только в случае `mode="*check"`

#### size `String`
Размер выпадающего списка: `s`, `m`, `l`, `xl`

#### tabIndex `Number`
Последовательность перехода фокуса

#### theme `String`
Тема: `islands`

#### val `Array` `Number` `String`
Выбранные значения по умолчанию

#### width `String`
Ширина выпадающего списка: `available`
