### Примеры

```jsx

const vendorNames = ['Apple', 'Maybelline', 'Главторг'];
    
<div>
    {vendorNames.map(name => (
        <div style={{marginBottom: '20px'}}>
            <SnippetVendor name={name}/>
        </div>
    ))}
</div>
```
