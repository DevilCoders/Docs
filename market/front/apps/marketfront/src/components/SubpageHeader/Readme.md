
## Примеры

### Шапка с заголовком и двумя контролами
```jsx
import ViewPort from '@self/root/src/components/Styleguidist/ViewPort';
import Icon from '@self/root/src/uikit/components/Icon';
const {$gray600} = require('@self/root/src/uikit/palette/colors');

<ViewPort width={300} height={300}>
    <SubpageHeader
        title='Заголовок'
        leftControl={
            <Icon name='arrow-left' color={$gray600} />
        }
        rightControl={
            <Icon name='cross' color={$gray600} />
        }
    />
</ViewPort>
```
