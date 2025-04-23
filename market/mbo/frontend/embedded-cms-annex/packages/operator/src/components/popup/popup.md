Popup example:

```jsx
initialState = {isActive: false};
require('./popup.styl');

const toggleIsActive = () => setState({isActive: !state.isActive});
<Popup target={<button onClick={toggleIsActive}>
                 {state.isActive ? 'close' : 'open'}
               </button>}
       isActive={state.isActive}>
  <div style={{fontSize: 15}}>
    Some children
  </div>
</Popup>
```
