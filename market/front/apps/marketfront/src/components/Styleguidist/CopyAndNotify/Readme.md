Копирует текст в буфер обмена и уведомляет пользователя об этом.

#### Пример

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const Button = require('@self/root/src/uikit/components/Button').default;

<Provider store={store}>
    <div style={{display:'inline-block'}}>
        <CopyAndNotify text={'12345'}>
            <Button>Нажми на меня</Button>
        </CopyAndNotify>
    </div>
</Provider>
```
