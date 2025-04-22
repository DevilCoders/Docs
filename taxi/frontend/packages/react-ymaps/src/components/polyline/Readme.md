Polyline

```jsx harmony
const { Loader, Map, Collection, Polyline } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={{ controls: [] }}>
        <Collection>
          <Polyline coords={[[55.76, 37.64], [55.4, 37.3], [55.3, 37.4], [55.74, 37.67]]} />
        </Collection>
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```
