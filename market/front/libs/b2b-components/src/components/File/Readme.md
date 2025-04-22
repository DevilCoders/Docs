```jsx
const FileControl = require('./index').default;

<FileControl  />
```

```jsx
const FileMultiSelect = require('./Multiple').default;

<FileMultiSelect onChange={files => console.log(files)} files={[{name: 'file1.jpg'}, {name: 'file2.png'}]} />
```
