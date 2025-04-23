```jsx noeditor
const {$white, $purple600, $gray200} = require('@self/root/src/uikit/palette/colors');

const imageSrc = helper.generateImage({
    w: 400,
    h: 400,
    text: 'Картинка',
    color: $white,
    backgroundColor: $purple600
});

<Helper.Playground
    component={ImageBase}
    defaultValues={{
        width: 500,
        height: 150,
        src: imageSrc,
        children: 'Заглушка'
    }}
/>
```
