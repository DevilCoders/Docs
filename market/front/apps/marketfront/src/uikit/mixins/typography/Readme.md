## Миксины типографии

### Миксины заголовков

Миксины, использующиеся в компоненте Title
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const {Example} = require('./example');

<Provider store={store}>
    <div>
        <Example example="ui-typo-title-default" />
        <br/>
        <Example example="ui-typo-title-800" />
        <Example example="ui-typo-title-700" />
        <Example example="ui-typo-title-600" />
        <Example example="ui-typo-title-500" />
        <Example example="ui-typo-title-400" />
        <Example example="ui-typo-title-350" />
        <Example example="ui-typo-title-300" />
        <Example example="ui-typo-title-250" />
        <Example example="ui-typo-title-200" />
        <Example example="ui-typo-title-100" />
    </div>
</Provider>
```

### Миксины текста

Миксины, использующиеся в компоненте Text
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const {Example} = require('./example');

<Provider store={store}>
    <div>
        <Example example="ui-typo-text-800" />
        <Example example="ui-typo-text-700" />
        <Example example="ui-typo-text-600" />
        <Example example="ui-typo-text-500" />
        <Example example="ui-typo-text-400" />
        <Example example="ui-typo-text-350" />
        <Example example="ui-typo-text-300" />
        <Example example="ui-typo-text-250" />
        <Example example="ui-typo-text-200" />
        <Example example="ui-typo-text-100" />
    </div>
</Provider>
```

### Миксины размеров (базовые, без жирности)

Общие миксины размеров, из которых строятся все тексты.
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const {Example} = require('./example');

<Provider store={store}>
    <div>
        <Example example="ui-typo-size-800" />
        <Example example="ui-typo-size-700" />
        <Example example="ui-typo-size-600" />
        <Example example="ui-typo-size-500" />
        <Example example="ui-typo-size-400" />
        <Example example="ui-typo-size-350" />
        <Example example="ui-typo-size-300" />
        <Example example="ui-typo-size-250" />
        <Example example="ui-typo-size-200" />
        <Example example="ui-typo-size-100" />
    </div>
</Provider>
```

### Миксины типов шрифтов
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const {Example} = require('./example');

<Provider store={store}>
    <div>
        <Example example="ui-typo-font-normal" />
    </div>
</Provider>
```

### Миксины тем
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const {Example} = require('./example');

<Provider store={store}>
    <div>
        <Example example="ui-typo-theme-normal" />
        <Example example="ui-typo-theme-primary" />
        <Example example="ui-typo-theme-warning" />
        <Example example="ui-typo-theme-error" />
        <Example example="ui-typo-theme-success" />
        <Example example="ui-typo-theme-muted" />
        <div style={{background: "grey"}}>
            <Example example="ui-typo-theme-invert" />
        </div>
    </div>
</Provider>
```


### Миксины жирности
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const {Example} = require('./example');

<Provider store={store}>
    <div>
        <Example example="ui-typo-weight-regular" />
        <Example example="ui-typo-weight-medium" />
        <Example example="ui-typo-weight-bold" />
    </div>
</Provider>
```
