Типографика размеров в [миксинах типографики текста](./#/UI-Kit/mixins/typography)

```jsx
    <div>
        <Text>Текст по умолчанию</Text>
    </div>
```

### Песочница
```js noeditor
// todo поддержать TypoSize
const sizes = 'default,800,700,600,500,400,350,300,250,200,100'.split(',');
// todo поддержать TypoTheme
const themes = 'normal,warning,muted,invert,primary,success,error'.split(',');
// todo поддержать TypoWeight
const weights = 'regular,medium,bold'.split(',');


<Helper.Playground
    component={Text}
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
        weight: {
            type: 'enum',
            required: false,
            values: weights,
        },
    }}
/>
```

### Примеры
#### Размеры

```
    <div>
        <Text size="800">Текст 800</Text>
        <br/>
        <Text size="700">Текст 700</Text>
        <br/>
        <Text size="600">Текст 600</Text>
        <br/>
        <Text size="500">Текст 500</Text>
        <br/>
        <Text size="400">Текст 400</Text>
        <br/>
        <Text size="350">Текст 350</Text>
        <br/>
        <Text size="300">Текст 300</Text>
        <br/>
        <Text size="250">Текст 250</Text>
        <br/>
        <Text size="200">Текст 200</Text>
        <br/>
        <Text size="100">Текст 100</Text>
    </div>
```

#### Темы

```
    <div>
        <Text theme="normal">Текст основной</Text>
        <br/>
        <Text theme="muted">Текст минорный</Text>
        <br/>
        <Text theme="warning">Текст варнинг</Text>
        <br/>
        <Text theme="primary">Текст purple</Text>
        <br/>
        <Text theme="success">Текст success</Text>
        <br/>
        <Text theme="error">Текст error</Text>
        <br/>
        <div style={{backgroundColor: 'black'}}>
            <Text theme="invert">Текст инвертированный</Text>
        </div>
    </div>
```

#### Жирность

```
    <div>
        <Text weight="regular">Текст 400</Text>
        <br/>
        <Text weight="medium">Текст 500</Text>
        <br/>
        <Text weight="bold">Текст 700</Text>
    </div>
```
