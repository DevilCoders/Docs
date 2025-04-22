### theme=light
```jsx
    const items = require('./mocks');
    
    const demoContainer = {
        background: '#f7f7f7',
        padding: '30px 20px',
    };
    
    <div style={demoContainer}>
        <Breadcrumbs theme='light' items={items} />
    </div>
```

### theme=dark
```jsx
    const items = require('./mocks');

    const demoContainer = {
        background: '#222',
        padding: '30px 20px',
    };
    
    <div style={demoContainer}>
        <Breadcrumbs theme='dark' items={items} />
    </div>
```

Элементы навигационной цепочки, не умещающиеся по ширине в контейнере, переносятся с левой стороны.

```jsx
    const items = require('./mocks');
    
    const demoContainer = {
        background: '#f7f7f7',
        padding: '30px 20px',
        maxWidth: '400px',
    };
    
    <div style={demoContainer}>
        <Breadcrumbs items={items} />
    </div>
```
Не вмещающийся по ширине текст обрезается и завершается знаком троеточия.

```jsx
    const items = require('./mocks');
    
    const demoContainer = {
        background: '#f7f7f7',
        padding: '30px 20px',
        maxWidth: '150px',
    };
    
    <div style={demoContainer}>
        <Breadcrumbs items={items} />
    </div>
```

### wrapping=wrap

```jsx
    const items = require('./mocks');
    
    const demoContainer = {
        background: '#f7f7f7',
        padding: '30px 20px',
        maxWidth: '400px',
    };
    
    <div style={demoContainer}>
        <Breadcrumbs items={items} wrapping='wrap' />
    </div>
```

### screen=touch
```jsx
    const items = require('./mocks');
    
    const demoContainer = {
        padding: '30px 20px',
    };
    
    <div style={demoContainer}>
        <Breadcrumbs items={items} screen='touch' />
    </div>
```
