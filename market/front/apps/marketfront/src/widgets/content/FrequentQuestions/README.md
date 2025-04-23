### Виджет 'Частые вопросы'

```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const View = require('./components/View/index.js').default;

    const props = {
        title: 'Часто спрашивают',
        questions: [
            {
                text: 'Первый вопрос',
                id: 'Первый вопрос',
                answer: '<span>Первый ответ</span>',
            },
            {
                text: 'Второй вопрос',
                id: 'Второй вопрос',
                answer: '<span>Второй ответ</span>',
            },
        ],
        openedTabIds: ['Первый вопрос'],
        toggleTab: () => {},
    };

    let store = createStore(() => {});


    <Provider store={store}>
        <View {...props} />
    </Provider>
```
