### Набор компонентов, формирующих лэйаут страницы

##### Лэйаут
```jsx static
<Layout />
```
Задает ширину блока, учитывая брейкпоинты:

```jsx noeditor
    import Text from '@self/root/src/uikit/components/Text';
    import {$green400, $orange200} from '@self/root/src/uikit/palette/colors';
    import breakpoints from '@self/root/src/uikit/layout/breakpoints';

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

##### Сетка
```jsx static
<Layout.Grid size={1..24} />
```
Задает сетку от 1 до 24 колонок.

##### Контейнер
```jsx static
<Container />
```
Необходимый блок для компенсации отступов (`$ui-gutter`). Используется внутри `<Layout.Grid/>`

##### Колонка
```jsx static
<Layout.Column size={1..24} />
```
Колонка внутри сетки с заданной шириной. Зависит от размера, указанного в `<Layout.Grid/>`


#### Примеры

###### Лэйаут с брейкпоинтами
```jsx
    import {times} from 'ambar'

    import {$green400, $orange200} from '@self/root/src/uikit/palette/colors';

    import Layout from '.';

    const column = <div style={{background: $green400, height: '40px'}} />;

    <div style={{overflowX: 'scroll'}}>
        <Layout>
            <Layout.Grid size={24}>
                {times(i => (
                    <Layout.Column size={1}>
                        {column}
                    </Layout.Column>
                ), 24)}
            </Layout.Grid>
        </Layout>
    </div>
```

###### Сетка на 24 колонки

```jsx
    import {times} from 'ambar'

    import Layout from '.';
    import {$green400, $orange200} from '@self/root/src/uikit/palette/colors';

    const column = <div style={{background: $green400, height: '40px'}} />;

    <div>
        <Layout.Grid size={24}>
            {times(i => (
                <Layout.Column size={1}>
                    {column}
                </Layout.Column>
            ), 24)}
        </Layout.Grid>

        <br/>

        <Layout.Grid size={24}>
            <Layout.Column size={1}>
                {column}
            </Layout.Column>
            <Layout.Column size={2}>
                {column}
            </Layout.Column>
            <Layout.Column size={3}>
                {column}
            </Layout.Column>
            <Layout.Column size={6}>
                {column}
            </Layout.Column>
            <Layout.Column size={12}>
                {column}
            </Layout.Column>
        </Layout.Grid>
    </div>
```

###### Сетка на 12 колонок

```jsx
    import {times} from 'ambar'

    import {$green400, $orange200} from '@self/root/src/uikit/palette/colors';

    import Layout from '.';

    const column = <div style={{background: $green400, height: '40px'}} />;

    <div>
        <Layout.Grid size={12}>
            {times(i => (
                <Layout.Column size={1}>
                    {column}
                </Layout.Column>
            ), 12)}
        </Layout.Grid>

        <br/>

        <Layout.Grid size={12}>
            <Layout.Column size={1}>
                {column}
            </Layout.Column>
            <Layout.Column size={2}>
                {column}
            </Layout.Column>
            <Layout.Column size={3}>
                {column}
            </Layout.Column>
            <Layout.Column size={6}>
                {column}
            </Layout.Column>
        </Layout.Grid>
    </div>
```

###### Вложенные сетки
```jsx
    import {times} from 'ambar'

    import {$green400, $orange200} from '@self/root/src/uikit/palette/colors';

    import Layout from '.';

    const column = <div style={{background: $green400, height: '40px'}} />;

    <div>
        <Layout.Grid size={24}>
            {times(i => (
                <Layout.Column size={1}>
                    {column}
                </Layout.Column>
            ), 24)}
        </Layout.Grid>

        <br/>

        <Layout.Grid size={24}>
            <Layout.Column size={1}>
                {column}
            </Layout.Column>
            <Layout.Column size={2}>
                {column}
            </Layout.Column>
            <Layout.Column size={3}>
                {column}
            </Layout.Column>
            <Layout.Column size={6}>
                {column}
            </Layout.Column>
            <Layout.Column size={12}>
                <div style={{background: $orange200, height: '40px'}}>
                    <Layout.Grid size={12}>
                        <Layout.Column size={1}>
                            {column}
                        </Layout.Column>
                        <Layout.Column size={2}>
                            {column}
                        </Layout.Column>
                        <Layout.Column size={3}>
                            {column}
                        </Layout.Column>
                        <Layout.Column size={6}>
                            {column}
                        </Layout.Column>
                    </Layout.Grid>
                </div>
            </Layout.Column>
        </Layout.Grid>
    </div>
```
