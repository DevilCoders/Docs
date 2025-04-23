Можно увидеть в Header ("Войти в аккаунт" и "Мой профиль")

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
        <InformationPanel icon='info' theme='warning'>
            <InformationPanel.Title>
                Важное замечание
            </InformationPanel.Title>
            <InformationPanel.Content>
            Компонент является базовым для content виджетов HeaderUserBadge и HeaderNotAuthUserBadge
            </InformationPanel.Content>
        </InformationPanel>
    </Provider>
    <br/>
</div>

```

## Пример кастомного бейджа
```jsx
<div style={{backgroundColor: 'black'}}>
    <HeaderUserBadge>
        <HeaderUserBadge.Button component="a" href="//yandex.ru">
            <HeaderUserBadge.ManIcon />
            <HeaderUserBadge.Text>Пойти за хлебом</HeaderUserBadge.Text>
        </HeaderUserBadge.Button>
    </HeaderUserBadge>
</div>
```
