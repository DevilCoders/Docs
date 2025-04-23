Tooltip (тултип) — небольшая подсказка, содержащая поясняющий текст, которая появляется по наведению или нажатию на элемент.

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
        <InformationPanel theme={'success'} icon='answer'>
            <InformationPanel.Title>
            Когда использовать
            </InformationPanel.Title>
            <InformationPanel.Content>
                <div>
                    Tooltip используем в случаях взаимодействия пользователя с сервисом (например, пользователь нажимает на кнопкой подробной информации о фильтре).
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

Работает на основе Абстрактного Тултипа ([@self/root/src/uikit/components/AbstractTooltip](./#/UI-Kit/components/AbstractTooltip)), примеры использования можно посмотреть на нём.
