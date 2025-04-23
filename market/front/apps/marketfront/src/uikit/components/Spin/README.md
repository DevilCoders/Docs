## Спиннер

### Песочница
```js noeditor
<Helper.Playground component={Spin} settings={{background: 'transparent'}} />
```

### Примеры
### size

#### size='xxs'
```jsx
    <Spin size="xxs"/>
```

#### size='xs'
```jsx
    <Spin size="xs"/>
```

#### size='s'
```jsx
    <Spin size="s"/>
```

#### size='m' (default)
```jsx
    <Spin size="m"/>
```

#### size='l'
```jsx
    <Spin size="l"/>
```


### theme

#### theme='normal' (default)
```jsx
    <Spin/>
```

#### theme='light'
```jsx
    <div style={{background: 'black', padding: '20px'}}>
        <Spin theme="light"/>
    </div>
```

#### theme='action'
```jsx
    <div style={{background: 'black', padding: '20px'}}>
        <Spin theme="light"/>
    </div>
```

### Все вместе

```jsx
    <div>
        <div style={{padding: '20px'}}>
            <Spin size="xxs"/>
            <Spin size="xs"/>
            <Spin size="s"/>
            <Spin size="m"/>
            <Spin size= "l"/>
        </div>
        <div style={{background: 'black', padding: '20px'}}>
            <Spin theme="light" size="xxs"/>
            <Spin theme="light" size="xs"/>
            <Spin theme="light" size="s"/>
            <Spin theme="light" size="m"/>
            <Spin theme="light" size= "l"/>
        </div>
        <div style={{padding: '20px'}}>
            <Spin theme="action" size="xxs"/>
            <Spin theme="action" size="xs"/>
            <Spin theme="action" size="s"/>
            <Spin theme="action" size="m"/>
            <Spin theme="action" size= "l"/>
        </div>
    </div>
```
