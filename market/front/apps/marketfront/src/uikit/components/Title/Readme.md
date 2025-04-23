Типографика размеров в [миксинах типографики заголовков](./#/UI-Kit/mixins/typography)

```jsx
    <div>
        <Title>Заголовок по умолчанию</Title>
    </div>
```

### Песочница
```js noeditor
// todo поддержать TypoSize
const sizes = 'default,1200,800,700,600,500,400,350,300,250,200,100'.split(',');
// todo поддержать TypoTheme
const themes = 'normal,warning,muted,invert,primary,success,error'.split(',');

<Helper.Playground
    component={Title}
    defaultValues={{children: 'беру!'}}
    props={{
        size: {
            type: 'enum',
            required: false,
            values: sizes,
        },
        theme: {
            type: 'enum',
            required: false,
            values: themes,
        },
    }}
/>
```

### Примеры
#### Размеры

```jsx
    <div>
        <Title size="1200">Заголовок 1200</Title>
        <Title size="800">Заголовок 800</Title>
        <Title size="700">Заголовок 700</Title>
        <Title size="600">Заголовок 600</Title>
        <Title size="500">Заголовок 500</Title>
        <Title size="400">Заголовок 400</Title>
        <Title size="350">Заголовок 350</Title>
        <Title size="300">Заголовок 300</Title>
        <Title size="250">Заголовок 250</Title>
        <Title size="200">Заголовок 200</Title>
        <Title size="100">Заголовок 100</Title>
    </div>
```

#### Темы

```jsx
    <div>
        <Title theme="normal">Заголовок normal</Title>
        <Title theme="muted">Заголовок muted</Title>
        <Title theme="warning">Заголовок warning</Title>
        <Title theme="primary">Заголовок primary</Title>
        <Title theme="success">Заголовок success</Title>
        <Title theme="error">Заголовок error</Title>
        <div style={{backgroundColor: 'black'}}>
            <Title theme="invert">Заголовок invert</Title>
        </div>
    </div>
```
