Circle

```jsx harmony
const { Loader, Map, Collection, Circle } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 500 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={10} state={{ controls: [] }}>
        <Collection>
          <Circle center={[55.76, 37.64]} radius={10000} options={{
              fillColor: '#ffffff',
              fillOpacity: 0.5,
              strokeStyle: 'solid',
              strokeColor: '#000000',
              strokeOpacity: 0.5,
              strokeWidth: 1
            }} />
        </Collection>
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```
