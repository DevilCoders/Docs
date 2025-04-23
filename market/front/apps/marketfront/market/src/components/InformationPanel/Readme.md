Панель с информацией

### Песочница

```jsx
    import {Provider} from 'react-redux';
    import {createStore} from 'redux';
    const store = createStore(() => ({
        collections: {},
    }));

    <Provider store={store}>
        <Helper.Playground
            component={InformationPanel}
            defaultValues={{
                withTail: true,
                withCloser: true,
                theme: 'warning',
            }}
            example={props => {
                return (
                    <div>
                        <InformationPanel icon={'info'} {...props}>
                            <InformationPanel.Title>
                                Заказ приедет в нескольких посылках, потому что товары лежат на разных складах
                            </InformationPanel.Title>
                        </InformationPanel>
                    </div>
                );
            }}
        />
    </Provider>
```

```jsx
    import Text from '@self/root/src/uikit/components/Text';
    import {Provider} from 'react-redux';
    import {createStore} from 'redux';
    const store = createStore(() => ({
        collections: {},
    }));

    <Provider store={store}>
        <div>
            <InformationPanel withCloser={true} icon='car'>
                <InformationPanel.Title>
                    Изменилась цена на 1 товар
                </InformationPanel.Title>

                <InformationPanel.Content>
                    <Text size="250">
                        У товара "Капсулы Tide Go Pods автомат Альпийская свежесть" уменьшилась цена на 301 ₽
                    </Text>
                </InformationPanel.Content>
            </InformationPanel>

            <br/>
            <br/>

            <InformationPanel theme='error' icon='disallow'>
                <InformationPanel.Title>
                    Что-то пошло не так
                </InformationPanel.Title>
                <InformationPanel.Content>
                    <Text size="250" theme="invert">
                        Попробуйте вернуться назад и ещё раз перейдите по ссылке из письма. Если это не поможет, пожалуйста, обратитесь в службу поддержки.
                    </Text>
                </InformationPanel.Content>
            </InformationPanel>

            <br/>
            <br/>

            <InformationPanel theme='success' icon='megaphone'>
                <InformationPanel.Title>
                    Заказ №2342345 привязан
                </InformationPanel.Title>

                <InformationPanel.Content>
                    <Text size="250" theme="invert">
                        Теперь вы можете следить за статусом заказа на странице «Мои заказы».
                    </Text>
                </InformationPanel.Content>
            </InformationPanel>
        </div>
    </Provider>
```
