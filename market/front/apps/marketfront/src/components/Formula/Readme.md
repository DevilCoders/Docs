### Formula, известна также как картинка+ссылка

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const Touch = require('.').default;
const Desktop = require('.').default;

const props = {
    src: 'https://avatars.mds.yandex.net/get-marketcms/879900/img-904427fb-4ad9-4020-8e42-ac6497418a61.png/optimize',
    height: 200,
    width: 200,
    name: 'Телефоны',
    link: '@self/platform/Components/Formula',
};

const Formula = createPlatformProxyComponent({Touch, Desktop, childProps: props});

const Example = ({text, width, props}) => (
    <div style={{margin: '20px', width}}>
        <div style={{marginBottom: '10px'}}>{text}</div>
        <Formula {...props} />
    </div>
);

<Provider store={store}>
    <div style={{display: 'flex', flexDirection: 'row', height: '500px', backgroundColor: '#00000007'}}>
        <Example text={'Картинка с текстом'} props={props} />
        <Example text={'Картинка с текстом как сниппет'} width={'250px'} props={{...props, likeSnippet: true}} />
    </div>
</Provider>
```

### Playground
```jsx

import {Provider} from 'react-redux';
import {createStore} from 'redux';

import TextField from '@self/root/src/uikit/components/TextField';

const Touch = require('.').default;
const Desktop = require('.').default;

const store = createStore(() => ({
    collections: {},
    withoutSize: false,
}));

initialState = {
    height: 200,
    width: 200,
    src: 'https://avatars.mds.yandex.net/get-marketcms/879900/img-904427fb-4ad9-4020-8e42-ac6497418a61.png/optimize',
    name: 'Телефоны',
    containerWidth: 300,
};

const onChange = event => {
    setState({ containerWidth: event.target.value });
};
const onClear = event => {
    setState({ containerWidth: '' });
};

const FormulaProxy = createPlatformProxyComponent({Touch, Desktop, childProps: initialState});

<Provider store={store}>
    <div>
        <TextField
            size='l'
            value={state.containerWidth}
            onChange={onChange}
            onClear={onClear}
            label='Ширина контейнера:'
        />
        <br/>
        <Helper.Playground
            component={Formula}
            forceUpdate={true}
            settings={{background: 'transparent'}}
            defaultValues={state}
            example={props => (
                <div style={{width: `${state.containerWidth}px`}}>
                    <FormulaProxy {...props} />
                </div>
            )}
            props={{
                height: {
                    required: false,
                    type: 'number',
                    defaultValue: state.height,
                },
                width: {
                    required: false,
                    type: 'number',
                    defaultValue: state.width,
                }
            }}
        />
    </div>
</Provider>
```
