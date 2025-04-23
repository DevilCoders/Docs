```jsx

const colors = ['tomato', '#4abe4e', 'gold', '#0062CC'];
const sizes = ['s', 'm', 'l'];

const initialState = { activeColor: 'tomato' };
const onChange = value => {
    setState({ activeColor: value });
};

<div>
    {sizes.map(size => (
        <div style={{marginBottom: '30px'}} key={size}>
            {colors.map(color => (
                <div
                    style={{marginRight: '20px', display: 'inline-block'}} 
                    key={color}
                >
                    <VisualFilterValue
                        name='color'
                        value={color}
                        color={color}
                        
                        size={size}
                        active={color === state.activeColor}
                        onChange={onChange}
                    />      
                </div>
            ))}        
        </div>
    ))}
</div>
```

#### Свойство `disabled` 

```jsx

const colors = ['tomato', '#4abe4e', 'gold', '#0062CC'];

<div>
    {colors.map(color => (
        <div style={{marginRight: '20px', display: 'inline-block'}} key={color}>
            <VisualFilterValue
                name='color'
                value={color}
                color={color}
                
                disabled={true}
            />      
        </div>
    ))}
</div>
```

#### Свойство `text` 

```jsx

const sizes = ['30 см', '32 см', '34 см', '36 см'];

const initialState = { activeSizeValue: '30 см' };
const onChange = value => {
    setState({ activeSizeValue: value });
};

<div>
    {sizes.map(size => (
        <div style={{marginRight: '20px', display: 'inline-block'}} key={size}>
            <VisualFilterValue
                name='color'
                value={size}
                
                text={size}
                
                active={size === state.activeSizeValue}
                onChange={onChange}
            />      
        </div>
    ))}
</div>
```
