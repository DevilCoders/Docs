Отслеживание событий карты

```jsx harmony
const { Loader, Map, MapOnClick } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={{ controls: [] }}>
        <MapOnClick onClick={() => alert('Клик!')} />
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```
