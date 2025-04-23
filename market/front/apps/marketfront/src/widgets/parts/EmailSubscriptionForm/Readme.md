### Виджет подписки

```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const ViewPort = require('@self/root/src/components/Styleguidist/ViewPort').default;
    const Touch = require('./components/EmailSubscriptionForm/index.touch').default;
    const Desktop = require('./components/EmailSubscriptionForm/index.desktop').default;
    const {STEPS, STATUSES, THEME} = require('./constants.js')
    const EmailSubscriptionFormComp = createPlatformProxyComponent({Touch, Desktop});

    const steps = Object.values(STEPS);
    const statuses = Object.values(STATUSES);
    const themes = Object.values(THEME);
    const buttonThemes = ['normal', 'action', 'pseudo',
    'minor', 'danger', 'primary',
    'medium' , 'outline' , 'yaPay',
    'quickFilter', 'yaPlusGradient', 'white',
    'black', 'yellow'];


    <Helper.Playground
        component={EmailSubscriptionFormComp}
        props={{
            title: {
                type: 'string',
                required: false,
                defaultValue: 'Подпишись на рассылку!',
            },
            text: {
                type: 'string',
                required: false,
            },
            step: {
                type: 'enum',
                required: false,
                values: steps,
                defaultValue: STEPS.EMAIL,
            },
            email: {
                type: 'string',
                required: false,
                defaultValue: 'nullNulovich@yandex.ru',
            },
            status: {
                type: 'enum',
                required: false,
                values: statuses,
                defaultValue: STATUSES.UNDEFINED,
            },
            theme: {
                type: 'enum',
                required: false,
                values: themes,
            },
            buttonTheme: { 
                type: 'enum',
                required: false,
                values: buttonThemes,
            },
            shouldShowEnvelope: {
                type: 'boolean',
                required: false,
            },
            onEmailChange: () => null,
            onEmailCheck: () => null,
            onClear: () => null,
            onSubscribe: () => null,
        }}
    />
```
