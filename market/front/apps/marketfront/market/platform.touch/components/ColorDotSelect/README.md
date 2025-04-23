```jsx

const colors = ['#fff', '#4abe4e', '#000', '#0062CC'];

<div>
    {colors.map(color => (
        <div
            style={{marginRight: '10px', display: 'inline-block'}} 
            key={color}
        >
            <ColorDotSelect
                value={{code: color}}
                active={false}
            />    
        </div>
    ))}        
</div>
```

#### Свойство `active` 

```jsx

const colors = ['#fff', '#4abe4e', '#000', '#0062CC'];

<div>
    {colors.map(color => (
        <div
            style={{marginRight: '10px', display: 'inline-block'}} 
            key={color}
        >
            <ColorDotSelect
                value={{code: color}}
                active={true}
            />    
        </div>
    ))}        
</div>
```

#### Свойство `disabled` 

```jsx

const colors = ['#fff', '#4abe4e', '#000', '#0062CC'];

<div>
    {colors.map(color => (
        <div
            style={{marginRight: '10px', display: 'inline-block'}} 
            key={color}
        >
            <ColorDotSelect
                value={{code: color}}
                active={false}
                disabled={true}
            />    
        </div>
    ))}        
</div>
```
