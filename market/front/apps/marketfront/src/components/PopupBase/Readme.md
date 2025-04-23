```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const InformationPanel = require('@self/root/src/components/InformationPanel').default;

<div>
    <br/>
    <Provider store={store}>
        <InformationPanel theme='warning' icon='info'>
            <InformationPanel.Title>
                Компонент является базовым для Popup и PopupModal. В продуктовом коде необходимо использовать именно их.
            </InformationPanel.Title>
        </InformationPanel>
    </Provider>
    <br/>
</div>

```

```jsx noeditor
import Button from '@self/root/src/uikit/components/Button';
const withOpener = require('@self/root/src/components/HOC/withOpener').default;

const PopupBaseExample = ({isOpened, open, close, toggle, ...props}) => (
    <div>
        <Button onClick={toggle} theme="action">
            {isOpened ? 'Закрыть попап' : 'Открыть попап'}
        </Button>

        {isOpened && <PopupBase {...props} onClose={toggle}/>}
    </div>
);

<Helper.Playground
    component={PopupBase}
    example={withOpener(PopupBaseExample)}
    defaultValues={{children: 'Содержимое попапа'}}
/>

```
