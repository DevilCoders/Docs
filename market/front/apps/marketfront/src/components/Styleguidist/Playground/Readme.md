Добавляет песочницу к описанию компонентов

### Примеры
Все примеры на примере компонента `Price`

#### По умолчанию
```jsx
    import Price from '@self/root/src/uikit/components/Price';

    <Helper.Playground component={Price} />
```

#### Настройки отображения примера
##### `settings`
##### `settings.background`
```jsx
    import Price from '@self/root/src/uikit/components/Price';

    <Helper.Playground component={Price} settings={{background: 'transparent'}}/>
```
##### `settings.resize`
```jsx
    import Price from '@self/root/src/uikit/components/Price';

    <Helper.Playground component={Price} settings={{resize: 'vertical'}}/>
```

#### Значение пропсов компонента по умолчанию
##### `defaultValues`
```jsx
    import Price from '@self/root/src/uikit/components/Price';

    <Helper.Playground component={Price} defaultValues={{theme: 'accent'}}/>
```

#### Кастомизация компонента
##### `example = props => React.Node`
```jsx
    import Price from '@self/root/src/uikit/components/Price';

    <Helper.Playground
        component={Price}
        example={props => {
            return (
                <div>
                    <Price {...props} />
                    <br/>
                    <Price {...props} price={{value: 100, currency: 'RUR'}} />
                    <br/>
                    <Price {...props} price={{value: 1000, currency: 'RUR'}} />
                </div>
            );
        }}
    />
```

#### Замена или добавление типов значений компонента
##### `props`
Импорты типов при генерации документации по flow-типам пока недоступны (https://github.com/reactjs/react-docgen/issues/33).
Поэтому иногда их нужно прописать руками, используя существующие типы (или добавив новый тип).

```jsx
    import Price from '@self/root/src/uikit/components/Price';

    const prices = [
        {value: 123, currency: 'RUR'},
        {value: 1234, currency: 'RUR'},
    ];

    <Helper.Playground
        component={Price}
        props={{
            price: {
                required: true,
                type: 'enum',
                defaultValue: prices[0],
                values: prices
            }
        }}
    />
```

#### Форсирование обновления компонента
##### `forceUpdate={false} (default)`
Используется, если в stateful компоненте входные свойства `props` перебиваются свойствами внутреннего `state`.
В этом случае при изменении соотвествующего входящего свойства `props` (`background` в случае с `Example`)
перерисовки компонента не будет.

Однако, в остальных случаях форсирование обновления не хочется включать,
чтобы видеть как срабатывает анимация при изменении свойства (например, изменение темы у `Button`)
```jsx noeditor
    import Example from '@self/root/src/components/Styleguidist/Example';

    <Helper.Playground
        component={Example}
        defaultValues={{children: 'при изменении `background` компонент не обновляется'}}
        forceUpdate={false}
    />
```
##### `forceUpdate={true}`
```jsx noeditor
    import Example from '@self/root/src/components/Styleguidist/Example';

    <Helper.Playground
        component={Example}
        defaultValues={{children: 'при изменении `background` компонент обновляется'}}
        forceUpdate={true}
    />
```
