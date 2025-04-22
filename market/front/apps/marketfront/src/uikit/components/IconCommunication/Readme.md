### Параметры

#### `size`

Размер иконки

```jsx

const sizes = ['s', 'm', 'l'];

<div style={{display: 'flex', alignItems: 'center'}}>
    {sizes.map((size, key) => (
        <div key={key}>
            <div style={{display: 'inline-block', marginRight: '15px'}}>
                <IconCommunication size={size} name="ok" />
            </div>
            <div style={{display: 'inline-block', marginRight: '15px'}}>
                <IconCommunication size={size} name="fail" />
            </div>
        </div>
    ))}
</div>
```

#### Возможные иконки

```jsx

const icons = require('./icons').default;

const names = Object.keys(icons);

<div>
    {names.map((name, key) => (
        <div style={{marginBottom: '15px'}} key={key}>
            <div style={{display: 'inline-flex'}}>
                <div style={{display: 'inline-block', marginRight: '10px',}}>
                    <IconCommunication name={name} />
                </div>
                {name}
            </div>
        </div>
    ))}
</div>
```
