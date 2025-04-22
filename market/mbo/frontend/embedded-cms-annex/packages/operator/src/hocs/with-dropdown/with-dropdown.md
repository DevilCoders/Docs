withDropdown example:

```jsx
initialState = {isActive: false};
require('@/components/dropdown/dropdown.styl');
const {default: withDropdown} = require('./with-dropdown');
const Target = (props) => (
  <button onClick={props.onClick}>
    {props.isActive ? 'close' : 'open'}
  </button>
);
const DropdownByButton = withDropdown(Target);
const toggleIsActive = () => setState({isActive: !state.isActive});

<DropdownByButton isActive={state.isActive}
                  onClick={toggleIsActive}>
  <span style={{fontSize: 15}}>SomeText</span>
</DropdownByButton>
```
