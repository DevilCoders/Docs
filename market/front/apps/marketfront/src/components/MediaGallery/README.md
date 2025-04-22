MediaGallery — Компонент с баннерами (и не только), расположенными по сетке.
Для работы требует верно отформатированного лейаута.

Занимает всю ширину. Картинки при изменении размера сжимаются почти пропорционально. При это всегда остаются в сетке.
Главная задача компонента - сохраниение силуэта и сетки.

## Примеры

### Простой лейаут
```jsx
import Card from '@self/root/src/components/Card';
import MediaGallery from '@self/root/src/components/MediaGallery';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const layout = require('./mocks').zeroth;

const demoContainer = {
    outline: 'solid 1px #dcdcdc',
    maxWidth: '1420px',
    margin: 'auto',
};

const grid = {
    width: '1000px',
    margin: 'auto',
};

<Provider store={store}>
    <div style={demoContainer}>
        <div style={grid}>
            <Card>
                <MediaGallery layout={layout}/>
            </Card>
        </div>
    </div>
</Provider>
```

### Лейаут посложнее
```jsx
import Card from '@self/root/src/components/Card';
import MediaGallery from '@self/root/src/components/MediaGallery';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const layout = require('./mocks').first;

const demoContainer = {
    outline: 'solid 1px #dcdcdc',
    maxWidth: '1420px',
    margin: 'auto',
};
const grid = {
    width: '1000px',
    margin: 'auto',
};

<Provider store={store}>
    <div style={demoContainer}>
        <div style={grid}>
            <Card>
                <MediaGallery layout={layout}/>
            </Card>
        </div>
    </div>
</Provider>
```

### Еще один пример сложного лейаута. С настоящими картинками на фоне.
```jsx
import MediaGallery from '@self/root/src/components/MediaGallery';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const layout = require('./mocks').second;

const demoContainer = {
    outline: 'solid 1px #dcdcdc',
    maxWidth: '1420px',
    margin: 'auto',
    backgroundColor: '#c02485',
};

const grid = {
    width: '1000px',
    margin: 'auto',
};

<Provider store={store}>
    <div style={demoContainer}>
        <div style={grid}>
            <MediaGallery layout={layout}/>
        </div>
    </div>
</Provider>
```

### Раскладки можно комбинировать чтобы получить более сложные
```jsx
import Section from '@self/root/src/components/Section';
import MediaGallery from '@self/root/src/components/MediaGallery';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const layout1 = require('./mocks').third;
const layout2 = require('./mocks').fourth;

const demoContainer = {
    outline: 'solid 1px #dcdcdc',
    maxWidth: '1420px',
    margin: 'auto',
    backgroundColor: '#c02485',
};

const grid = {
    width: '1000px',
    margin: 'auto',
};

<Provider store={store}>
    <div style={demoContainer}>
        <div style={grid}>
            <Section
                title={'Сложна плитка из нескольких MediaGallery'}
                backgroundColor="transparent"
                theme="dark">

               <MediaGallery layout={layout1}/>
               <MediaGallery layout={layout2}/>
               <MediaGallery layout={layout1}/>
            </Section>
        </div>
    </div>
</Provider>
```

### Ошибки в лейауте
Если в лейауте чего-то не доехало, сам компонент ничего об этом не знает и попробует отрисоваться. Такие случаи нужно пресекать на сервере.
#### Не доехал один баннер, его соседа вытянуло
```jsx
import MediaGallery from '@self/root/src/components/MediaGallery';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const layout = require('./mocks').error;

const demoContainer = {
    outline: 'solid 1px #dcdcdc',
    maxWidth: '1420px',
    margin: 'auto',
};

<Provider store={store}>
    <div style={demoContainer}>
        <MediaGallery layout={layout}/>
    </div>
</Provider>
```

#### Доехал всего один баннер
```jsx
import MediaGallery from '@self/root/src/components/MediaGallery';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const layout = require('./mocks').error2;

const demoContainer = {
    outline: 'solid 1px #dcdcdc',
    maxWidth: '1420px',
    margin: 'auto',
};

<Provider store={store}>
    <div style={demoContainer}>
        <MediaGallery layout={layout}/>
    </div>
</Provider>
```
