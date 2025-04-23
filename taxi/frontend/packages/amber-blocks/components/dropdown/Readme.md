Dropdown

```jsx harmony
const Button = require('../button').default;
const List = require('./examples/list-simple').default;

<Dropdown controlComponent={<Button>Действия...</Button>} placement="top">
    <List />
</Dropdown>;
```

Ширина s, m, l

```jsx harmony
const Button = require('../button').default;
const List = require('./examples/list-simple').default;

<React.Fragment>
    {['s', 'm', 'l'].map(size => (
        <div key={size} style={{marginBottom: 8}}>
            <Dropdown
                size={size}
                controlComponent={<Button style={{width: 300}}>{`Размер ${size}`}</Button>}
                placement="top"
            >
                <List />
            </Dropdown>
        </div>
    ))}
</React.Fragment>;
```

Placement

```jsx harmony
const Button = require('../button').default;
const List = require('./examples/list-simple').default;

<React.Fragment>
    {[
        'auto-start',
        'auto',
        'auto-end',
        'top-start',
        'top',
        'top-end',
        'right-start',
        'right',
        'right-end',
        'bottom-end',
        'bottom',
        'bottom-start',
        'left-end',
        'left',
        'left-start'
    ].map(placement => (
        <div key={placement} style={{marginBottom: 8}}>
            <Dropdown controlComponent={<Button>{`Расположение ${placement}`}</Button>} placement={placement} size="l">
                <List />
            </Dropdown>
        </div>
    ))}
</React.Fragment>;
```

С иконками

```jsx harmony
const Button = require('../button').default;
const List = require('./examples/list-icons').default;

<Dropdown controlComponent={<Button>Действия...</Button>} placement="top">
    <List />
</Dropdown>;
```

С контролами

```jsx harmony
const Button = require('../button').default;
const List = require('./examples/list-controls').default;

<Dropdown controlComponent={<Button>Действия...</Button>} placement="top">
    <List />
</Dropdown>;
```

С кликабельными элементами

```jsx harmony
const Button = require('../button').default;
const List = require('./examples/list-with-modal').default;
const Modal = require('./examples/modal').default;

<React.Fragment>
    <Dropdown controlComponent={<Button>Действия...</Button>} placement="top">
        <List onClick={() => setState({openModal: true})} />
    </Dropdown>
    {state.openModal && <Modal onClose={() => setState({openModal: false})} />}
</React.Fragment>;
```

Внутри модалки

```jsx harmony
const Button = require('../button').default;
const List = require('./examples/list-simple').default;
const Modal = require('./examples/modal').default;

<React.Fragment>
    <Button onClick={() => setState({openModal: true})}>Открыть модалку</Button>
    {state.openModal && (
        <Modal onClose={() => setState({openModal: false})}>
            <Dropdown controlComponent={<Button>Действия...</Button>} placement="top">
                <List/>
            </Dropdown>
        </Modal>
    )}
</React.Fragment>;
```

Disabled элементы

```jsx harmony
const Button = require('../button').default;
const List = require('./examples/list-disabled').default;

<React.Fragment>
    <Dropdown controlComponent={<Button>Действия...</Button>} placement="top">
        <List onClick={() => alert('OK')} />
    </Dropdown>
</React.Fragment>;
```
