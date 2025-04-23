### Section - компонент для блока с отступами, фоном и возможностью закруглять края

Просто с серым фоном:

```jsx
const generateLoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').generate;
<Section theme="gray">
    {generateLoremIpsum(100)}
</Section>
```

Как контейнер для кнопок в модалке:
```jsx
const ButtonGroup = require('../button-group').default;
const Button = require('../button').default;

<Section theme="gray" padding="m" roundBorders="bottom">
    <ButtonGroup>
        <Button theme="accent">Button 1</Button>
        <Button>Button 2</Button>
    </ButtonGroup>
</Section>
```
