### Песочница

```jsx noeditor
<Helper.Playground
    component={Preloader}
    settings={{
        background: 'transparent',
        resize: 'vertical',
    }}
/>
```

### Прелоадер

```jsx
const Preloader = require('.').default;

<div style={{position: 'relative', width: '100px', height: '60px', background: '#eee'}}>
    <Preloader />
</div>
```

#### Неактивный прелоадер
```jsx
const Preloader = require('.').default;

<div style={{position: 'relative', width: '100px', height: '60px', background: '#eee'}}>
    <Preloader progress={false}/>
</div>
```

#### Активное состояние
```jsx
const Preloader = require('.').default;

<div style={{position: 'relative', width: '100px', height: '60px', background: '#eee'}}>
    <Preloader progress={true}/>
</div>
```

#### Размеры спиннеров
##### size="m" (по умолчанию)
```jsx
const Preloader = require('.').default;

<div style={{position: 'relative', width: '100px', height: '60px', background: '#eee'}}>
    <Preloader size="m" progress={true} />
</div>
```

##### size="s"
```jsx
const Preloader = require('.').default;

<div style={{position: 'relative', width: '100px', height: '60px', background: '#eee'}}>
    <Preloader size="s" progress={true} />
</div>
```

##### size="l"
```jsx
const Preloader = require('.').default;

<div style={{position: 'relative', width: '100px', height: '60px', background: '#eee'}}>
    <Preloader size="l" progress={true} />
</div>
```

#### Положение спиннера

##### position="center" (по умолчанию)
```jsx
const Preloader = require('.').default;

<div style={{position: 'relative', width: '100px', height: '300px', background: '#eee'}}>
    <Preloader position="center" progress={true} />
</div>
```

##### position="top"
```jsx
const Preloader = require('.').default;

<div style={{position: 'relative', width: '100px', height: '300px', background: '#eee'}}>
    <Preloader position="top" progress={true} />
</div>
```

#### Прелоадер с контентом
```jsx
const Preloader = require('.').default;

<div style={{position: 'relative', width: '200px', height: '300px', background: '#eee'}}>
    <Preloader position="top" progress={true}>
        Processing...
    </Preloader>
</div>
```
