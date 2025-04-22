### EditableString example

```jsx
initialState = {value: 'Some value'};
require('./popup/editable-string-popup.styl');
require('./title/editable-string-title.styl');
const {default: EditableString} = require('./editable-string');

const setValue = (value) => {
  setState({value});
}

<EditableString value={state.value} onSubmit={setValue} />
```
