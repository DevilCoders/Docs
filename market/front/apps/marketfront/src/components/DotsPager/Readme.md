#### Песочница (не умеет в `direction`)
```jsx noeditor
<Helper.Playground
    component={DotsPager}
    defaultValues={{
        index: 3,
        around: 1,
        pages: 10,
    }}
/>
```

#### Песочница (умеет в `direction`, но всегда перерисовывает компонент)
```jsx noeditor
<Helper.Playground
    component={DotsPager}
    forceUpdate={true}
    defaultValues={{
        index: 3,
        around: 1,
        pages: 10,
    }}
/>
```


#### Примеры
##### `pages={2}`
```jsx
<div>
    <DotsPager index={0} pages={2} />
    <br />
    <DotsPager index={1} pages={2} />
</div>
```

##### `pages={3}`
```jsx
<div>
    <DotsPager index={0} pages={3} />
    <br />
    <DotsPager index={1} pages={3} />
    <br />
    <DotsPager index={2} pages={3} />
</div>
```

##### `pages={4}`
```jsx
<div>
    <DotsPager index={0} pages={4} />
    <br />
    <DotsPager index={1} pages={4} />
    <br />
    <DotsPager index={2} pages={4} />
    <br />
    <DotsPager index={3} pages={4} />
</div>
```

##### `pages={5}`
```jsx
<div>
    <DotsPager index={0} pages={5} />
    <br />
    <DotsPager index={1} pages={5} />
    <br />
    <DotsPager index={2} pages={5} />
    <br />
    <DotsPager index={3} pages={5} />
    <br />
    <DotsPager index={4} pages={5} />
    <br />
    <DotsPager index={3} pages={5} />
    <br />
    <DotsPager index={2} pages={5} />
    <br />
    <DotsPager index={1} pages={5} />
    <br />
    <DotsPager index={0} pages={5} />
</div>
```
##### `pages={10}`
```jsx
<div>
    <DotsPager index={0} pages={10} />
    <br />
    <DotsPager index={1} pages={10} />
    <br />
    <DotsPager index={2} pages={10} />
    <br />
    <DotsPager index={3} pages={10} />
    <br />
    <DotsPager index={4} pages={10} />
    <br />
    <DotsPager index={3} pages={10} />
    <br />
    <DotsPager index={2} pages={10} />
    <br />
    <DotsPager index={1} pages={10} />
    <br />
    <DotsPager index={0} pages={10} />
</div>
```

#### Примеры с направлениями
##### `pages={5}`
```jsx
<div>
    <DotsPager index={0} pages={5} direction={0} />
    <br />
    <DotsPager index={1} pages={5} direction={1} />
    <br />
    <DotsPager index={2} pages={5} direction={1} />
    <br />
    <DotsPager index={3} pages={5} direction={1} />
    <br />
    <DotsPager index={4} pages={5} direction={1} />
    <br />
    <DotsPager index={3} pages={5} direction={-1} />
    <br />
    <DotsPager index={2} pages={5} direction={-1} />
    <br />
    <DotsPager index={1} pages={5} direction={-1} />
    <br />
    <DotsPager index={0} pages={5} direction={-1} />
</div>
```
##### `pages={10}`
```jsx
<div>
    <DotsPager index={0} pages={10} direction={0} />
    <br />
    <DotsPager index={1} pages={10} direction={1} />
    <br />
    <DotsPager index={2} pages={10} direction={1} />
    <br />
    <DotsPager index={3} pages={10} direction={1} />
    <br />
    <DotsPager index={4} pages={10} direction={1} />
    <br />
    <DotsPager index={3} pages={10} direction={0} />
    <br />
    <DotsPager index={2} pages={10} direction={-1} />
    <br />
    <DotsPager index={1} pages={10} direction={-1} />
    <br />
    <DotsPager index={0} pages={10} direction={-1} />
</div>
```

#### Примеры со счетчиком
##### `pages={2}`
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

import AmountSelect from '@self/root/src/components/AmountSelect';

const store = createStore(() => ({
    collections: {},
}));

initialState = {
    index: 0,
};

const handler = index => setState({index});
const pages = 2;

<Provider store={store}>
    <div>
        <DotsPager pages={pages} index={state.index} onClick={handler}/>
        <br />
        <AmountSelect
            min={0}
            max={pages - 1}
            amount={state.index}
            onChange={handler}
        />
    </div>
</Provider>
```

##### `pages={4}`
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

import AmountSelect from '@self/root/src/components/AmountSelect';

const store = createStore(() => ({
    collections: {},
}));

initialState = {
    index: 0,
};

const handler = index => setState({index});
const pages = 4;

<Provider store={store}>
    <div>
        <DotsPager pages={pages} index={state.index} onClick={handler}/>
        <br />
        <AmountSelect
            min={0}
            max={pages - 1}
            amount={state.index}
            onChange={handler}
        />
    </div>
</Provider>
```

##### `pages={5}`
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

import AmountSelect from '@self/root/src/components/AmountSelect';

const store = createStore(() => ({
    collections: {},
}));

initialState = {
    index: 0,
};

const handler = index => setState({index});
const pages = 5;

<Provider store={store}>
    <div>
        <DotsPager pages={pages} index={state.index} onClick={handler}/>
        <br />
        <AmountSelect
            min={0}
            max={pages - 1}
            amount={state.index}
            onChange={handler}
        />
    </div>
</Provider>
```

##### `pages={10}`
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

import AmountSelect from '@self/root/src/components/AmountSelect';

const store = createStore(() => ({
    collections: {},
}));

initialState = {
    index: 0,
};

const handler = index => setState({index});
const pages = 10;

<Provider store={store}>
    <div>
        <DotsPager pages={pages} index={state.index} onClick={handler}/>
        <br />
        <AmountSelect
            min={0}
            max={pages - 1}
            amount={state.index}
            onChange={handler}
        />
    </div>
</Provider>
```
