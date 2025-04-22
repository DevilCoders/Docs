# Attach
Используется для выбора файла, предназначенного для отправки на сервер. [Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/attach/)

## Использование
```jsx
var Attach = require('bem-react/lib/Attach');

var button = (
    <button>
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16">
            <path d="M1 13v2h14v-2h-14zm13-7h-3v-5h-6v5.031l-3-.031 6 6 6-6z" />
        </svg>
    </button>
);

var handleChange = function(payload) {
    console.log('File selected:', paylod.value);
};

<Attach name="sample" button={button}
    placeholder="File not selected" onChange={handleChange} />
```

## Параметры

#### button `ReactElement` `String`
Содержимое кнопки

#### disabled `Boolean`
Неактивное состояние

#### name `String`
Имя контрола

#### onChange(payload)
Колбэк изменения текстового поля
- **payload** `Object`
  - **target** `BEM`  
    Экземпляр BEM блока
  - **value** `String`  
    Значение текстовой области
  - **files** `FileList`  
    Объект с выбранными файлами

#### placeholder `String`
Текст сообщения, когда файл не выбран

#### size `String`
Размер контрола: `s`, `m`, `l`, `xl`

#### theme `String`
Тема: `islands`
