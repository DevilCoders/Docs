### Параметры

```jsx
<div>
    Песочница на ремонте
</div>
```

#### `size`

Размер иконки

```jsx

const sizes = ['s', 'm', 'l'];

<div style={{display: 'flex', alignItems: 'center'}}>
    {sizes.map(size => (
        <div style={{display: 'inline-block', marginRight: '15px'}} key={size}>
            <IconRevision size={size} name="bell" key={size} />
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
            <IconRevision size='l' name="bell" color={color} />
        </div>
    ))}
    <div style={{display: 'inline-block', marginRight: '15px', color: '#222222'}}>
        <IconRevision size='l' name="bell" key="currentColor" />
    </div>
</div>
```

#### Возможные иконки

```jsx

const icons = require('./icons').default;

const names = Object.keys(icons);

<div>
    {names.map(name=> (
        <div style={{marginBottom: '15px'}} key={name}>
            <div style={{display: 'inline-flex'}}>
                <div style={{display: 'inline-block', marginRight: '10px',}}>
                    <IconRevision name={name} />
                </div>
                {name}
            </div>
        </div>
    ))}
</div>
```
