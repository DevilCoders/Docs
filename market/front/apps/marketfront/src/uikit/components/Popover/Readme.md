Popover — подсказка, окно с информацией и элементами навигации, которое появляется по нажатию или наведению на элемент.

```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
import InformationPanel from '@self/root/src/components/InformationPanel';

<div>
    <br/>
    <Provider store={store}>
        <InformationPanel theme={'success'} icon='answer'>
            <InformationPanel.Title>
            Когда использовать
            </InformationPanel.Title>
            <InformationPanel.Content>
                <div>
                Popover используем в случаях взаимодействия пользователя с сервисом (например, пользователь нажимает на кнопкой подробной информации о кредите).
                В отличие от Tooltip, Popover это как правило более большое и информативное окно, которое может содержать элементы навигации и не закрывается при нажатии на содержимое.
                </div>
                <br/>
                <div>
                Если сервис самостоятельно хочет дать пользователю новую информацию – используй компонент Hint.
                </div>
            </InformationPanel.Content>
        </InformationPanel>
    </Provider>
    <br/>
</div>
```

Работает на основе Абстрактного Тултипа ([@self/root/src/uikit/components/AbstractTooltip](./#/UI-Kit/components/AbstractTooltip)).

```js
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const AnchorWithPopover = require('./_mock').default;

<Provider store={store}>
    <div style={{width: 850}}>
        <div style={{display: 'flex', justifyContent: 'space-between'}}>
            <AnchorWithPopover position={'top-left'}/>
            <AnchorWithPopover position={'top-center'}/>
            <AnchorWithPopover position={'top-right'}/>
        </div>
        <div style={{display: 'flex', justifyContent: 'space-between', marginTop: 70}}>
            <AnchorWithPopover position={'right'}/>
            <AnchorWithPopover position={'left'}/>
        </div>
        <div style={{display: 'flex', justifyContent: 'space-between', marginTop: 80}}>
            <AnchorWithPopover position={'bottom-left'}/>
            <AnchorWithPopover position={'bottom-center'}/>
            <AnchorWithPopover position={'bottom-right'}/>
        </div>
    </div>
</Provider>
```

### `withTail`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const AnchorWithPopover = require('./_mock').default;

<Provider store={store}>
    <div>
        <AnchorWithPopover>
            С хвостиком
        </AnchorWithPopover>

        <br/>

        <AnchorWithPopover withTail={false}>
            Без хвостика
        </AnchorWithPopover>
    </div>
</Provider>
```

### `withCloser`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const AnchorWithPopover = require('./_mock').default;

<Provider store={store}>
    <div>
        <AnchorWithPopover withCloser={true}>
            С крестиком
        </AnchorWithPopover>

        <br/>

        <AnchorWithPopover>
            Без крестика
        </AnchorWithPopover>
    </div>
</Provider>
```

### `width`

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const AnchorWithPopover = require('./_mock').default;

<Provider store={store}>
    <div>
        <AnchorWithPopover width='short' position='right'>
            Short
        </AnchorWithPopover>

        <br/>

        <AnchorWithPopover width='medium' position='right'>
            Medium
        </AnchorWithPopover>

        <br/>

        <AnchorWithPopover width='long' position='right'>
            Long
        </AnchorWithPopover>
    </div>
</Provider>
```
