Кнопка для загрузки

В Firefox input не работает внутри кнопки

```jsx harmony
const ButtonSpan = require('../button-span').default;
<File controlComponent={<ButtonSpan>Выберите файл</ButtonSpan>} />
```

Отображается имя файла

```jsx harmony
const ButtonSpan = require('../button-span').default;
<File
    controlComponent={<ButtonSpan>Выберите файл</ButtonSpan>}
    onChange={e => setState({text: e.target.value})}
    text={state.text}
/>
```

Текст по умолчанию

```jsx harmony
const ButtonSpan = require('../button-span').default;
<File
    controlComponent={<ButtonSpan>Выберите файл</ButtonSpan>}
    onChange={e => setState({text: e.target.value})}
    text={state.text || 'Файл не выбран'}
/>
```

Указание типа файла

```jsx harmony
const ButtonSpan = require('../button-span').default;
<File
    controlComponent={<ButtonSpan>Выберите CSV файл</ButtonSpan>}
    accept=".csv"
/>
```

Disabled

```jsx harmony
const ButtonSpan = require('../button-span').default;
<File text="Файл не выбран" controlComponent={<ButtonSpan disabled>Выберите файл</ButtonSpan>} disabled/>
```

Multi

```jsx harmony
const ButtonSpan = require('../button-span').default;
<File controlComponent={<ButtonSpan>Выберите файл</ButtonSpan>} multiple/>
```

С ошибкой

```jsx harmony
const ButtonSpan = require('../button-span').default;
<File error controlComponent={<ButtonSpan>Выберите файл</ButtonSpan>} text="Файл не выбран"/>
```
