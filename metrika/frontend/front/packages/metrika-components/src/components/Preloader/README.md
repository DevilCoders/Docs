Прозрачный фон; белый фон
```jsx
<div style={{ display: 'flex' }}>
    <div style={{
            background: 'linear-gradient(45deg, #e66465, #9198e5)',
            width: 100,
            height: 100,
            position: 'relative',
            border: '1px solid #e66465',
        }}
    >
        <Preloader transparent size="xs" />
    </div>
    <div style={{
            background: 'linear-gradient(45deg, #e66465, #9198e5)',
            width: 100,
            height: 100,
            position: 'relative',
            border: '1px solid #e66465',
            marginLeft: 10
        }}
    >
        <Preloader size="xs" />
    </div>
</div>
```