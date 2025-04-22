### Input example:
styles: 
- @/components/input/input.styl

```jsx
require('./input.styl');
<Input placeholder="test" />
```

### Input with tags example:
styles: 
- @/components/input/input.styl
- @/components/input/with-content/input-with-content.styl

```jsx
const {default: Example} = require('./with-content/example');

<Example />
```
