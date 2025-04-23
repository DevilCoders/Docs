## Overview

ScrollBox - это контейнер, который обеспечивает отображение любого количества контента в одну строку.
Если места во вьюпорт-контейнере не хватит, то появится скролл.


## Sandbox

Все настройки в одном месте

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

import Checkbox from '@self/root/src/uikit/components/Checkbox';
import Radio from '@self/root/src/uikit/components/Radio';
import Button from '@self/root/src/uikit/components/Button';

const store = createStore(() => ({
    collections: {},
}));

initialState = {
    ratio: [2, 5],
    showControls: false,
    withGutters: true,
};

const createOnCheckboxChange = key => () =>
    setState(prevState => ({[key]: !prevState[key]}));

const createOnRatioChange = ratio => ({currentTarget: {checked}}) =>
    checked && setState({ratio});

const isRatioChecked = ({ratio}, value) =>
    String(ratio) === String(value);

const onResetRatioClick = () => setState({ratio: null});

<Provider store={store}>
    <div>
        <Checkbox
            label='Отображение кнопки'
            checked={state.showControls}
            onChange={createOnCheckboxChange('showControls')}
        />
        <br/>
        <Checkbox
            label='Отображение внутренних отступов'
            checked={state.withGutters}
            onChange={createOnCheckboxChange('withGutters')}
        />
        <br/>
        <Checkbox
                label='Включить Autoplay'
                checked={state.autoplay}
                onChange={createOnCheckboxChange('autoplay')}
            />
        <br/>
            <Checkbox
                label='Прокручивать вначало, когда дошли до конца'
                checked={state.looped}
                onChange={createOnCheckboxChange('looped')}
            />
        <br/>
        <h1>Соотношение ширины одного элемента (в колонках) к общему количеству колонок.</h1>
        <Radio
            label='Соотношение [1, 1]'
            value={[1, 1]}
            checked={isRatioChecked(state, [1, 1])}
            onChange={createOnRatioChange([1, 1])}
        />
        <br/>
        <Radio
            label='Соотношение [2, 5]'
            value={[2, 5]}
            checked={isRatioChecked(state, [2, 5])}
            onChange={createOnRatioChange([2, 5])}
        />
        <br/>
        <Radio
            label='Соотношение [3, 7]'
            value={[3, 7]}
            checked={isRatioChecked(state, [3, 7])}
            onChange={createOnRatioChange([3, 7])}
        />
        <br/>
        <br/>
        <Button text='Сбросить соотношение' onClick={onResetRatioClick}/>
        <br/>
        <br/>
        <ScrollBox
            ratio={state.ratio}
            withGutters={state.withGutters}
            showControls={state.showControls}
            autoplay={state.autoplay}
            looped={state.looped}
        >
            {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
        </ScrollBox>
    </div>
</Provider>
```


## Props

### `compensateSideMargin`

Компенсация отступов сетки.

### `compensateSideMargin={true}` (default)

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox
        withGutters={true}
        compensateSideMargin={true}
    >
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```

### `withGutters`

Отображение внутренних отступов между элементами.


#### `withGutters={true}` (default)

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox withGutters={true}>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


#### `withGutters={false}`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox withGutters={false}>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


### `ratio`

Задает отношение размера (в колонках) одного элемента к ширине `ScrollBox` (в колонках).
Если не задан, то разбиения на колонки не случится.


#### `ratio={null}` (default)

Без колонок

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox ratio={null}>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} src={helper.generateImage({w: 10 * Math.floor(Math.random() * 10) + 50, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


#### `ratio={[2, 5]}`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox ratio={[2, 5]}>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


### `showControls`

Включает элементы управления.


#### `showControls={false}` (default)

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox showControls={false}>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


#### `showControls={true}`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox showControls>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


### `controlsSize`

Размер элементов управления.


#### `controlsSize='s'`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox showControls controlsSize='s'>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


#### `controlsSize='m'` (default)

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox showControls controlsSize='m'>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


#### `controlsSize='l'`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox showControls controlsSize='l'>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```

### `align`

#### `align='top'` (default)
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox showControls controlsSize='m' align='top'>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: `${id * 10}%`}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```

#### `align='center'`
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox showControls controlsSize='m' align='center'>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: `${id * 10}%`}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


#### `align='bottom'`
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox showControls controlsSize='m' align='bottom'>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: `${id * 10}%`}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```

#### `sidesSpace='xs|s|m|l'`

Задает отступы с краев

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox
            ratio={[2,5]}
            withGutters={true}
            showControls={true}
            autoplay={true}
            looped={true}
            sidesSpace='l'
        >
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```

### Other examples


#### `withGutters={true}`, `showControls={true}`, `ratio={[2, 5]}`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox
        withGutters
        showControls
        ratio={[2, 5]}
    >
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


#### `withGutters={true}`, `showControls={true}`, `ratio={[2, 5]}`

Когда мало элементов.

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox
        withGutters
        showControls
        ratio={[2, 5]}
    >
        {[1, 2].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


#### `withGutters={false}`, `showControls={true}`, `ratio={[2, 5]}`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox
        withGutters={false}
        showControls
        ratio={[2, 5]}
    >
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 350, h: 200, text: id})}/>)}
    </ScrollBox>
</Provider>
```


#### `withGutters={true}`, `showControls={true}`, `ratio={[1, 1]}`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox
        withGutters
        showControls
        ratio={[1, 1]}
    >
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 250, h: 100, text: id})}/>)}
    </ScrollBox>
</Provider>
```


#### `withGutters={false}`, `showControls={true}`, `ratio={[1, 1]}`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <ScrollBox
        withGutters={false}
        showControls
        ratio={[1, 1]}
    >
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 250, h: 100, text: id})}/>)}
    </ScrollBox>
</Provider>
```

### Кастомный контрол

В ScrollBox можно передать свой компонент кнопки, для скролла вправо/влево: `ControlButton`.
В пропсы компоненту будут переданы размер, направление и обработчик клика

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const store = createStore(() => ({
    collections: {},
}));

const CustomControl = ({side, size, onClick}) => (
    <span style={{
            width: '50px',
            height: '50px',
            'border-radius': '50%',
            border: '1px solid black',
            position: 'absolute',
            top: '20%',
            [side === 'right'? 'right' : 'left']: 0,
            'text-align': 'center',
            'line-height': '50px',
            cursor: 'pointer'
        }}
        onClick={onClick}
    >

      {`${side[0]}-${size}`}
    </span>
);

<Provider store={store}>
    <ScrollBox
        withGutters={false}
        showControls
        ratio={[1, 4]}
        ControlButton={CustomControl}
    >
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map(id => <img key={id} style={{width: '100%'}} src={helper.generateImage({w: 250, h: 100, text: id})}/>)}
    </ScrollBox>
</Provider>
```
