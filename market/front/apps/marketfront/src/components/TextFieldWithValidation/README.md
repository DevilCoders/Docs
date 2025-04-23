## TextFieldWithValidation

 - валидация введенного значения в TextField
 - отображение ошибки при потере фокуса и скрытие при фокусе
 - отправка данных в метрику на основе errorCodes и результата выполнения validate
 - вызов коллбэка `onSuccess`, если поле заполнено корректно
 - вызов коллбэка `onError`, если поле заполнено не корректно

Компонент не хранит в себе введенное значение, за это отвечают потребители.


### Примеры

#### Поле с валидацией

```jsx
    import {TextFieldWithValidation as TextFieldWithValidationView} from '.';
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const store = createStore(() => ({
        collections: {},
    }));

    <Provider store={store}>
        <div>
            <TextFieldWithValidationView
                textFieldProps={({
                    label: 'Номер телефона',
                    size: 'm',
                    defaultValue: 'asqw'
                })}
                validate={(value => {
                    if (value && value.length === 0) {
                        return {
                            text: 'Введите номер телефона',
                            codes: 'PHONE_ERROR',
                            value,
                        }
                    }
                })}
            />
        </div>
    </Provider>
```

#### Поле с валидацией и коллбэками

```jsx
    import {TextFieldWithValidation as TextFieldWithValidationView} from '.';
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const store = createStore(() => ({
        collections: {},
    }));

    <Provider store={store}>
        <div>
            <TextFieldWithValidationView
                textFieldProps={({
                    label: 'Номер телефона',
                    size: 'm',
                })}
                validate={(value => {
                    if (value && value.length === 0) {
                        return {
                            text: 'Введите номер телефона',
                            codes: 'PHONE_ERROR',
                            value,
                        }
                    }
                })}
                onSuccess={() => alert(`onSuccess: value "${value}"`)}
                onError={error => alert(`onError: error text "${error.text}"`)}
            />
        </div>
    </Provider>
```

#### Поле с отображением ошибки (без валидации)

```jsx
    import {TextFieldWithValidation as TextFieldWithValidationView} from '.';
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const store = createStore(() => ({
        collections: {},
    }));

    <Provider store={store}>
        <div>
            <TextFieldWithValidationView
                textFieldProps={({
                    label: 'Email',
                    size: 'm',
                })}
                errorText='Введите email'
            />
        </div>
    </Provider>
```
