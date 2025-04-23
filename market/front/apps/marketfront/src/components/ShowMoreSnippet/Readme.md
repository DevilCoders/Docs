### Элемент для показа всех элементов ScrollBox'a.
2 варианта отображения - ссылка и кнопка.

Для десктопа показывается ссылка.

Для тача сейчас (июнь 2020) показывается ссылка в ScrollBox, в других компонентах может быть кнопка.

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';

const Touch = require('.').default;
const Desktop = require('.').default;

const props = {
    url: '@self/platform/Components/ShowMoreSnippet',
    title: 'Хочешь ещё?',
    displayMode: 'link',
};

const ShowMoreSnippet = createPlatformProxyComponent({Touch, Desktop, childProps: props});

const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <div style={{display: 'flex', flexDirection: 'column', width: '300px'}}>
        <ShowMoreSnippet {...props} />
        <br />
        <ShowMoreSnippet {...props} displayMode={'button'} />
        <br />
        <ShowMoreSnippet {...props} theme={'success'} />
        <br />
    </div>
</Provider>
```

### Playground
```jsx

import {Provider} from 'react-redux';
import {createStore} from 'redux';

const Touch = require('.').default;
const Desktop = require('.').default;

const store = createStore(() => ({
    collections: {},
}));

initialState = {
    url: '#',
    title: 'Хочешь ещё?',
    displayMode: 'link',
    theme: 'normal'
};

//export type Props = {
//    url: string,
//    title?: string,
//    displayMode?: ShowMoreSnippetDisplayMode,
//    theme?: $ElementType<LinkProps, 'theme'>,
//};

const ShowMoreSnippetProxy = createPlatformProxyComponent({Touch, Desktop, childProps: initialState});
const themes = 'normal, dark, gray, light, black, purple, white, yellow, cobalt-blue, success, error, warning'.split(', ');

<Provider store={store}>
    <div>
        <Helper.Playground
            component={ShowMoreSnippet}
            forceUpdate={true}
            settings={{background: 'transparent'}}
            defaultValues={state}
            example={props => (
                <ShowMoreSnippetProxy {...props} />
            )}
            props={{
                url: {
                    required: true,
                    type: 'string',
                    defaultValue: state.url,
                },
                title: {
                    required: false,
                    type: 'string',
                    defaultValue: state.title,
                },
                displayMode: {
                    required: false,
                    type: 'enum',
                    defaultValue: state.displayMode,
                    values: ['link', 'button'],
                },
                theme: {
                    required: false,
                    type: 'enum',
                    defaultValue: state.theme,
                    values: themes,
                },
            }}
        />
    </div>
</Provider>
```
