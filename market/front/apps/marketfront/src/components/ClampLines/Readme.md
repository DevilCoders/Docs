```jsx noeditor
import Text from '@self/root/src/uikit/components/Text';
import ClampLines from '@self/root/src/components/ClampLines';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <Helper.Playground
        component={ClampLines}
        forceUpdate={true}
        defaultValues={{text: helper.generateText({words: 100})}}
        example={props => (
            <div>
                <div style={{lineHeight: `${props.lineHeight}px`}}>
                    <ClampLines {...props} />
                </div>
                <br/>
                <Text theme="muted" size="100">
                    Примечание: у контейнера так же задано `line-height: {props.lineHeight}px`
                </Text>
            </div>
        )}
    />
</Provider>
```
