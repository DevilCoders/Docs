Кастомный контрол масштаба

```jsx harmony
const { Loader, Map, ZoomControl } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={{ controls: [] }}>
        <ZoomControl/>
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```

Контрол слева

```jsx harmony
const { Loader, Map, ZoomControl } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={{ controls: [] }}>
        <ZoomControl style={{left: 5, right: 'auto'}} onClick={_ => console.log(`click on zoom`)}/>
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```
