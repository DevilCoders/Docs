### Tag example:

```jsx
initialState = {};
require('./tag.styl');
const {default: CmsTag} = require('./tag.tsx');

<CmsTag>value as text</CmsTag>
```

### Example with removable:

```jsx
initialState = {};
const {default: CmsTag} = require('./tag.tsx');

<CmsTag isRemovable={true}>value as text</CmsTag>
```
