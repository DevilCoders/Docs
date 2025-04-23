Hint — подсказка для привлечения внимания. Появляется с небольшой задержкой без тапа на объект.

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
        <InformationPanel theme={'success'} icon='info'>
            <InformationPanel.Title>
                Пояснение
            </InformationPanel.Title>
            <InformationPanel.Content>
                <div>
                Hint используем в случаях привлечения внимания пользователя (например, о появлении новой фичи).
                </div>
                <br/>
                <div>
                Если необходимо показать всплывающее сообщение в ответ на некоторое пользовательское действие – используй компонет Tooltip.
                </div>
            </InformationPanel.Content>
        </InformationPanel>
    </Provider>
    <br/>
</div>

```

Работает на основе Абстрактного Тултипа ([@self/root/src/uikit/components/AbstractTooltip](./#/UI-Kit/components/AbstractTooltip)), примеры использования можно посмотреть на нём.
