### Нотификация

### Песочница
```jsx noeditor
    import {Provider} from 'react-redux';
    import {createStore} from 'redux';

    const store = createStore(() => ({
        collections: {},
    }));

    <Provider store={store}>
        <Helper.Playground
            component={Notification}
            example={props => (
                <Notification {...props} icon='disallow'>
                    Текст нотификации
                </Notification>
            )}
        />
    </Provider>
```

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
import Button from '@self/root/src/uikit/components/Button';

const store = createStore(() => ({
    collections: {},
}));

initialState = {
    notificationError: false,
    notificationWarning: false,
    notificationSuccess: false,
};

const toggleNotification = (notice) => setState({[notice]: !state[notice]});

let notificationError, notificationWarning, notificationSuccess;

if (state.notificationError === true) {
    notificationError = (
        <Provider store={store}>
            <Notification
                icon='disallow'
                theme='error'
                onClick={() => toggleNotification('notificationError')}
            >
                Что-то пошло не так
            </Notification>
        </Provider>
    );
}

if (state.notificationWarning === true) {
    notificationWarning = (
        <Provider store={store}>
            <Notification
                position='sticky'
                theme='warning'
                onClick={() => toggleNotification('notificationWarning')}
            >
                Нотификация с текстом предупреждения
            </Notification>
        </Provider>
    );
}

if (state.notificationSuccess === true) {
    notificationSuccess = (
        <Provider store={store}>
            <Notification
                icon='megaphone'
                theme='success'
                message='Текст'
                onClick={() => toggleNotification('notificationSuccess')}
            >
                Всё прошло хорошо!
            </Notification>
        </Provider>
    );
}

const style = {marginTop: 20};

<div>
    {notificationError}

    <div style={{marginTop: 20}}>
        <Button onClick={() => toggleNotification('notificationError')}>
            Notification ошибки
        </Button>
    </div>

    {notificationSuccess}

    <div style={{marginTop: 20}}>
        <Button onClick={() => toggleNotification('notificationSuccess')}>
            Notification с иконкой `успешно`
        </Button>
    </div>

    {notificationWarning}

    <div style={{marginTop: 20}}>
        <Button onClick={() => toggleNotification('notificationWarning')}>
            Notification оповещения
        </Button>
    </div>

</div>
```
