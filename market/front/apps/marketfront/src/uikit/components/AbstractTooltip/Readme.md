```jsx noeditor
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));
const InformationPanel = require('@self/root/src/components/InformationPanel').default;

<div>
    <br/>
    <Provider store={store}>
        <InformationPanel icon='info' theme='warning'>
            <InformationPanel.Title>
                Важное замечание
            </InformationPanel.Title>
            <InformationPanel.Content>
            Компонент является базовым для Hint, Tooltip и Popover. В продуктовом коде необходимо использовать именно их.
            </InformationPanel.Content>
        </InformationPanel>
    </Provider>
    <br/>
</div>
```

**AbstractTooltip** — подсказка, содержащая поясняющий текст, которая появляется по наведению или нажатию на элемент.


### Песочница
`isOpen` в примере отключено, свойство меняется при клике на `anchor` элемент
```jsx noeditor
const AnchorWithTooltip = require('./_mock').default;

<Helper.Playground
    component={AbstractTooltip}
    settings={{background: 'transparent'}}
    defaultValues={{children: 'click me!'}}
    props={{
        position: {
            required: false,
            type: 'enum',
            values: 'top-left,top-center,top-right,right,bottom-left,bottom-center,bottom-right,left'.split(',')
        }
    }}
    example={AnchorWithTooltip}
/>

```

### Примеры
### `position`

```jsx

const AnchorWithTooltip = require('./_mock').default;


<div style={{width: 850}}>
    <div style={{display: 'flex', justifyContent: 'space-between'}}>
        <AnchorWithTooltip position={'top-left'}/>
        <AnchorWithTooltip position={'top-center'}/>
        <AnchorWithTooltip position={'top-right'}/>
    </div>
    <div style={{display: 'flex', justifyContent: 'space-between', marginTop: 70}}>
        <AnchorWithTooltip position={'right'}/>
        <AnchorWithTooltip position={'left'}/>
    </div>
    <div style={{display: 'flex', justifyContent: 'space-between', marginTop: 80}}>
        <AnchorWithTooltip position={'bottom-left'}/>
        <AnchorWithTooltip position={'bottom-center'}/>
        <AnchorWithTooltip position={'bottom-right'}/>
    </div>
</div>

```

### `theme`

```jsx
const AnchorWithTooltip = require('./_mock').default;

const themes = ['normal', 'accentDark', 'accentLight', 'popover', 'error', 'black'];

themes.map(theme => (
    <div style={{marginBottom: 20}}>
        <AnchorWithTooltip theme={theme} position={'right'}>
            {theme}
        </AnchorWithTooltip>
    </div>
))

```

### `hasAnimation`

```jsx
const AnchorWithTooltip = require('./_mock').default;


<div>
    <AnchorWithTooltip hasAnimation={false}>
        Без анимации
    </AnchorWithTooltip>

    <br/>

    <AnchorWithTooltip hasAnimation={true}>
        C анимацией
    </AnchorWithTooltip>
</div>

```

### `withDelay`

```jsx
const AnchorWithTooltip = require('./_mock').default;


<div>
    <AnchorWithTooltip>
        Без задержки
    </AnchorWithTooltip>

    <br/>

    <AnchorWithTooltip withDelay={true}>
        C задержкой
    </AnchorWithTooltip>
</div>
```

### `withTail`

```jsx
const AnchorWithTooltip = require('./_mock').default;


<div>
    <AnchorWithTooltip theme='popover'>
        С хвостиком
    </AnchorWithTooltip>

    <br/>

    <AnchorWithTooltip withTail={false} theme='popover'>
        Без хвостика
    </AnchorWithTooltip>
</div>
```

### `withCloser`

```jsx
const AnchorWithTooltip = require('./_mock').default;


<div>
    <AnchorWithTooltip withCloser={true} theme='popover'>
        С крестиком
    </AnchorWithTooltip>

    <br/>

    <AnchorWithTooltip theme='popover'>
        Без крестика
    </AnchorWithTooltip>
</div>
```
