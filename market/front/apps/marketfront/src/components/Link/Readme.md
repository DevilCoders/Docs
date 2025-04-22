### Компонент ссылки
Использовать через контейнер Link

#### theme 'normal'
```jsx
const Link = require('.').default;

<Link theme='normal' url='test'>
    Ссылка
</Link>
```

#### theme 'dark'
```jsx
const Link = require('.').default;

<div style={{background: 'red'}}>
    <Link theme='dark' url='test'>
        Ссылка
    </Link>
</div>
```

#### theme 'light'
```jsx
const Link = require('.').default;

<Link theme='light' url='test'>
    Ссылка
</Link>
```

#### theme 'gray'
```jsx
const Link = require('.').default;

<div style={{background: 'red'}}>
    <Link theme='gray' url='test'>
        Ссылка
    </Link>
</div>
```

#### theme 'black'
```jsx
const Link = require('.').default;

<Link theme='black' url='test'>
    Ссылка
</Link>
```

#### theme 'white'
```jsx
const Link = require('.').default;

<div style={{background: 'red'}}>
    <Link theme='white' url='test'>
        Ссылка
    </Link>
</div>
```

#### theme 'success'
```jsx
const Link = require('.').default;

<Link theme='success' url='test'>
    Ссылка
</Link>
```

#### theme 'error'
```jsx
const Link = require('.').default;

<Link theme='error' url='test'>
    Ссылка
</Link>
```

#### theme 'warning'
```jsx
const Link = require('.').default;

<Link theme='warning' url='test'>
    Ссылка
</Link>
```

#### Ссылка которая ничего не делает
```jsx
const Link = require('.').default;

<Link>
    Ссылка без pointer
</Link>
```

#### Playground
```jsx
const Touch = require('.').default;
const Desktop = require('.').default;

const LinkProxy = createPlatformProxyComponent({Touch, Desktop});

<Helper.Playground
    component={Link}
    example={props => <LinkProxy {...props}/>}
/>

```

