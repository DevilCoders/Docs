Bounds карты

```jsx harmony
const { Loader, Map, MapBounds } = require('../..');
const getSafeBounds = require('../../utils/getSafeBounds').default;

const mapState = { controls: [] };

const VALUES = [
  [[56.835941, 60.592658], [56.844083, 60.628364]],
  [[56.810338, 60.595405], [56.89461, 60.605018]],
  [[56.89461, 60.605018], [56.837652, 60.56179]]
];
// задаем индес по умолчанию, потому что в первом рендере его там нет
// почему то initialState перестало работать
const index = state.index || 0;

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <button
      style={{ position: 'absolute', margin: 16, zIndex: 10 }}
      onClick={() => {
        setState({ index: (index + 1) % VALUES.length });
      }}
    >
      Change bounds (current: {index})
    </button>

    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={mapState}>
        <MapBounds bounds={getSafeBounds(VALUES[index])} />
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```
