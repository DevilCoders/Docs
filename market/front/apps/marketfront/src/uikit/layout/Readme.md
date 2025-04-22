```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
import InformationPanel from '@self/root/src/components/InformationPanel';

<Provider store={store}>
    <div>
        <br/>
        <InformationPanel theme={'warning'} icon='info'>
            <InformationPanel.Title>
            Чтобы не создавать лишних стилей лучше использовать набор компонентов <i>@self/root/src/uikit/components/Layout</i>
            </InformationPanel.Title>
        </InformationPanel>

        <br/>

        <InformationPanel theme={'success'} icon='answer'>
            <InformationPanel.Title>
                Где использовать
            </InformationPanel.Title>
            <InformationPanel.Content>
                Импорт констант (брейкпоинты, гуттеры)
            </InformationPanel.Content>
        </InformationPanel>

        <br/>
    </div>
</Provider>
```

### Брейкпоинты

```jsx noeditor
    import Text from '@self/root/src/uikit/components/Text';
    const {$green400, $orange200} = require('@self/root/src/uikit/palette/colors');
    const breakpoints = require('@self/root/src/uikit/layout/breakpoints');
    const LayoutComponent = require('@self/root/src/uikit/components/Layout').default;
    const {Container, Grid, Column} = LayoutComponent;

    const breakpointNames = Object.keys(breakpoints);

    <table style={{width: '350px'}}>
        <tbody>
            {breakpointNames.map(name => (
                <tr style={{marginTop: '10px'}}>
                    <td>
                        <Text theme="muted">{name}</Text>
                    </td>
                    <td>
                        <Text theme="normal">{breakpoints[name]}</Text>
                    </td>
                </tr>
            ))}
        </tbody>
    </table>
```

### Сетка

Для того чтобы использовать сеточный лэйаут,
нужно подключить миксины `ui-layout()` в корень и `ui-grid($num)` в месте использования сетки,
где `$num` - количество колонок лэйаута.

#### Миксин `ui-layout()` дает несколько общих классов:

##### `.container`

```scss
.container {}
```
Контэйнер задает лэйаут. Может встраиваться в колонку. Адаптивен

##### `.col`

```scss
.col {}
```

#### Миксин `ui-grid($num)` расширяет свойства колонок:

##### `.col-{$num}`

```scss
.col-1 {}
/* ... */
.col-24 {}
```

##### Примеры

###### Сетка на 24 колонки
```scss
ui-layout();

.grid-24 {
    ui-grid(24);
}
```

```
    const _ = require('lodash');
    const {$green400, $orange200} = require('@self/root/src/uikit/palette/colors');
    const LayoutComponent = require('@self/root/src/uikit/components/Layout').default;
    const {Container, Grid, Column} = LayoutComponent;

    const column = <div style={{background: $green400, height: '40px'}} />;

    <div>
        <Grid size={24}>
            {_.times(24, i => (
                <Column size={1}>
                    {column}
                </Column>
            ))}
        </Grid>

        <br/>

        <Grid size={24}>
            <Column size={1}>
                {column}
            </Column>
            <Column size={2}>
                {column}
            </Column>
            <Column size={3}>
                {column}
            </Column>
            <Column size={6}>
                {column}
            </Column>
            <Column size={12}>
                {column}
            </Column>
        </Grid>
    </div>
```

###### Сетка на 12 колонок
```scss
ui-layout();

.grid-12 {
    ui-grid(12);
}
```

```jsx
    const _ = require('lodash');
    const {$green400, $orange200} = require('@self/root/src/uikit/palette/colors');
    const LayoutComponent = require('@self/root/src/uikit/components/Layout').default;
    const {Container, Grid, Column} = LayoutComponent;

    const column = <div style={{background: $green400, height: '40px'}} />;

    <div>
        <Grid size={12}>
            {_.times(12, i => (
                <Column size={1}>
                    {column}
                </Column>
            ))}
        </Grid>

        <br/>

        <Grid size={12}>
            <Column size={1}>
                {column}
            </Column>
            <Column size={2}>
                {column}
            </Column>
            <Column size={3}>
                {column}
            </Column>
            <Column size={6}>
                {column}
            </Column>
        </Grid>
    </div>
```

###### Вложенные сетки
```scss
ui-layout();

.grid-24 {
    ui-grid(24);
}

.grid-12 {
    ui-grid(12);
}
```

```
    const _ = require('lodash');
    const {$green400, $orange200} = require('@self/root/src/uikit/palette/colors');
    const LayoutComponent = require('@self/root/src/uikit/components/Layout').default;
    const {Container, Grid, Column} = LayoutComponent;

    const column = <div style={{background: $green400, height: '40px'}} />;

    <div>
        <Grid size={24}>
            {_.times(24, i => (
                <Column size={1}>
                    {column}
                </Column>
            ))}
        </Grid>

        <br/>

        <Grid size={24}>
            <Column size={1}>
                {column}
            </Column>
            <Column size={2}>
                {column}
            </Column>
            <Column size={3}>
                {column}
            </Column>
            <Column size={6}>
                {column}
            </Column>
            <Column size={12}>
                <div style={{background: $orange200, height: '40px'}}>
                    <Grid size={12}>
                        <Column size={1}>
                            {column}
                        </Column>
                        <Column size={2}>
                            {column}
                        </Column>
                        <Column size={3}>
                            {column}
                        </Column>
                        <Column size={6}>
                            {column}
                        </Column>
                    </Grid>
                </div>
            </Column>
        </Grid>
    </div>
```


###### Лэйаут с брейкпоинтами
```scss
.layout {
    ui-breakpoint-layout();
}
```

```
    const _ = require('lodash');
    const {$green400, $orange200} = require('@self/root/src/uikit/palette/colors');
    const LayoutComponent = require('@self/root/src/uikit/components/Layout').default;
    const {Container, Grid, Column} = LayoutComponent;

    const column = <div style={{background: $green400, height: '40px'}} />;

    <div style={{overflowX: 'scroll'}}>
        <LayoutComponent>
            <Grid size={24}>
                {_.times(24, i => (
                    <Column size={1}>
                        {column}
                    </Column>
                ))}
            </Grid>
        </LayoutComponent>
    </div>
```
