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
        <InformationPanel theme={'normal'} icon='info'>
            <InformationPanel.Title>
                Что это?
            </InformationPanel.Title>
            <InformationPanel.Content>
                Это базовый компонент для Price и MonthlyPayment.
                Использовать его напрямую не нужно.
                Примеры см. на страницах этих компонентов.
            </InformationPanel.Content>
        </InformationPanel>
    </Provider>
    <br/>
</div>

```

### Песочница
```jsx noeditor
// т.к. есть export cost PriceBase осьминожек не понимает
import PriceBase from '.';

<Helper.Playground component={PriceBase} />
```
