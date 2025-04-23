Алерс с ошибкой
```jsx harmony
<Alert type="error">
    Хьюстон, у нас волчанка. Или нет. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
</Alert>
```

Оповещения - для показа внутри форм и в правом нижнем углу
```jsx harmony
const Button = require('../button').default;

<React.Fragment>
    <Button onClick={() => setState({alert: 'info'})}>Инфо</Button>
    <br/><br/>
    {state.alert === 'info' &&
        <Alert onCloseClick={() => alert('Нажали close')} onClick={() => setState({alert: null})}>
            Хьюстон, у нас волчанка. Или нет. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </Alert>
    }
    <br/>
    <Button onClick={() => setState({alert: 'error'})}>Ошибка</Button>
    <br/><br/>
    {state.alert === 'error' &&
        <Alert type="error" onCloseClick={() => alert('Нажали close')} onClick={() => setState({alert: null})}>
            Хьюстон, у нас волчанка. Или нет. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </Alert>
    }
    <br/>
    <Button onClick={() => setState({alert: 'success'})} >Успех</Button>
    <br/><br/>
    {state.alert === 'success' &&
        <Alert type="success" onCloseClick={() => alert('Нажали close')} onClick={() => setState({alert: null})}>
            Хьюстон, у нас волчанка. Или нет. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </Alert>
    }
    <br/>
    <Button onClick={() => setState({alert: 'notification'})}>Нотификация-стайл</Button>
    <br/><br/>
    {state.alert === 'notification' &&
        <Alert type="success" theme="notification" onCloseClick={() => alert('Нажали close')} onClick={() => setState({alert: null})}>
            Хьюстон, у нас волчанка. Или нет.
        </Alert>
    }
</React.Fragment>
```
