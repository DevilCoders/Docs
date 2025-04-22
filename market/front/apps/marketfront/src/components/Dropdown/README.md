### Выпадалка

### Песочница
```js noeditor
<Helper.Playground
    component={Dropdown}
    defaultValues={{
        open: true,
        children: 'Hello world'
    }}
/>
```

### Пример использования
```jsx
const withClickOutside = require('@self/root/src/components/HOC/withClickOutside').default;
const withOpener = require('@self/root/src/components/HOC/withOpener').default;

const CloseOuthideThisZone = withClickOutside(({open, close, toggle, onClickOutside, isOpened}) => (
    <div>
        <button onClick={open}>Открыть выпадалку</button>
        <button onClick={toggle}>Открыть/Закрыть выпадалку</button>
        <Dropdown open={isOpened}>
            Закроюсь при клике в любом месте экрана
            <button onClick={close}>Закрыть выпадалку</button>
        </Dropdown>
    </div>
))

const Root = withOpener(({close, ...rest}) => (
    <div style={{position: 'relative', display: 'flex'}}>
        <CloseOuthideThisZone onClickOutside={close} close={close} {...rest} />
    </div>
));

<Root />

```

