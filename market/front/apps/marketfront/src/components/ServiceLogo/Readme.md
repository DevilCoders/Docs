**Логотип сервиса** (без подложки)

### Песочница
```js noeditor
<Helper.Playground component={ServiceLogo} settings={{background: 'transparent'}} />
```

### size

```jsx
const {$purple600} = require('@self/root/src/uikit/palette/colors');
<div  style={{padding: 20, background: $purple600}}>
    <ServiceLogo size={'l'} />

    <br/>

    <ServiceLogo size={'m'} />

    <br/>

    <ServiceLogo size={'s'} />
</div>

```

### theme

```jsx

const {$purple600, $gray200} = require('@self/root/src/uikit/palette/colors');
<div>
    <div style={{padding: 20, display: 'inlineBlock', background: $purple600}}>
        <ServiceLogo/>
    </div>

    <br/>

    <div style={{padding: 20, display: 'inlineBlock', background: $gray200}}>
            <ServiceLogo theme={'inverted'}/>
     </div>
</div>

```
