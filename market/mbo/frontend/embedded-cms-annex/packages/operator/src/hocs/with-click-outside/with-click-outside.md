withClickOutside example:

```jsx
initialState = {isActive: false};

require('@/components/dropdown/dropdown.styl');
const {default: Dropdown} = require('@/components/dropdown/dropdown');
const {default: withClickOutside} = require('./with-click-outside');

const DropdownWithClickOutside = withClickOutside(Dropdown);
const toggleIsActive = () => setState({isActive: !state.isActive});

<DropdownWithClickOutside target={
                            <button onClick={toggleIsActive}>
                              {state.isActive ? 'close' : 'open'}
                            </button>
                          }
                          isActive={state.isActive} 
                          disableOnClickOutside={!state.isActive}
                          onOutsideClick={() => setState({isActive: false})}>
  <span style={{fontSize: 15}}>SomeText</span>
</DropdownWithClickOutside>
```
