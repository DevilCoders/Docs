Мутный слой

```jsx harmony
const { Loader, Map, MoodyLayer } = require('../..');

const VALUES = ['20', '40', '60', '80'];
// задаем индес по умолчанию, потому что в первом рендере его там нет
// почему то initialState перестало работать
const index = state.index || 0;

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <button style={{position: 'absolute', margin: 16, zIndex: 10}} onClick={() => {
      setState({index: (index + 1) % VALUES.length})
    }}>Change opacity (current: {VALUES[index]})</button>
    
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={{ controls: [] }}>
        <MoodyLayer opacity={VALUES[index]} />
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```
