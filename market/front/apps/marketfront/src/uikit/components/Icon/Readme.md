Основные иконки на сервисе

### Параметры

#### `size`

Размер иконки

```jsx

const sizes = ['xxs', 'xs', 's', 'm', 'l', 'xl'];

<div style={{display: 'flex', alignItems: 'center'}}>
    {sizes.map(size => (
        <div style={{display: 'inline-block', marginRight: '15px'}} key={size}>
            <Icon size={size} name="shield" key={size} />
        </div>
    ))}
</div>
```

#### Возможные цвета

Любой цвет из палитры, импортится из colors.json.
Если цвет не указан, то берется текущий цвет у родительского элемента

```jsx

const colors = require('@self/root/src/uikit/palette/colors');
const sortedColors = Object.values(colors).sort();

<div style={{display: 'flex', alignItems: 'center', 'flexWrap': 'wrap'}}>
    {sortedColors.map((color, id) => (
        <div style={{display: 'inline-block', marginRight: '15px'}} key={id}>
            <Icon size='l' name="shield" color={color} key={color} />
        </div>
    ))}
    <div style={{display: 'inline-block', marginRight: '15px', color: '#222222'}}>
        <Icon size='l' name="shield" key="currentColor" />
    </div>
</div>
```

#### Возможные иконки

```jsx

const icons = require('./icons').default;

const names = Object.keys(icons);

<div>
    {names.map((name, id) => (
        <div style={{marginBottom: '15px'}} key={id}>
            <div style={{display: 'inline-block'}}>
                <Icon name={name} />
                <div
                    style={{
                        display: 'inline-block',
                        verticalAlign: 'top',
                        marginLeft: '10px',
                    }}
                >
                        {name}
                </div>
            </div>
        </div>
    ))}
</div>
```
