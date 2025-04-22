Карта

```jsx harmony
const { Loader, Map } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} />
    </Loader>
  </div>
</React.Fragment>;
```

Инициализация карты через `bounds`

```jsx harmony
const { Loader, Map } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map
        bounds={[
          [54.81961939331861, 32.68516601562499],
          [56.67814629201904, 42.59483398437498]
        ]}
      />
    </Loader>
  </div>
</React.Fragment>;
```

Смена центра карты через center

```jsx harmony
const { Loader, Map } = require('../..');

const COORDS = [
  [55.76, 37.64],
  [56.83, 60.59]
];

<React.Fragment>
  <div style={{ marginBottom: 10 }}>
    <button type="button" onClick={() => setState({ shift: !state.shift })}>
      Сменить координаты
    </button>
  </div>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={state.shift ? COORDS[1] : COORDS[0]} zoom={7} />
    </Loader>
  </div>
</React.Fragment>;
```

Смена зума карты через zoom

```jsx harmony
const { Loader, Map } = require('../..');

const COORDS = [55.76, 37.64];
const ZOOMS = [7, 10];

<React.Fragment>
  <div style={{ marginBottom: 10 }}>
    <button type="button" onClick={() => setState({ shift: !state.shift })}>
      Сменить zoom
    </button>
  </div>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={COORDS} zoom={state.shift ? ZOOMS[0] : ZOOMS[1]} />
    </Loader>
  </div>
</React.Fragment>;
```

Одновременно смена зума карты и центра карты через zoom и center

```jsx harmony
const { Loader, Map } = require('../..');

const COORDS = [
  [55.76, 37.64],
  [56.83, 60.59]
];
const ZOOMS = [7, 15];

<React.Fragment>
  <div style={{ marginBottom: 10 }}>
    <button type="button" onClick={() => setState({ shift: !state.shift })}>
      Сменить zoom и center
    </button>
  </div>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map
        center={state.shift ? COORDS[1] : COORDS[0]}
        zoom={state.shift ? ZOOMS[0] : ZOOMS[1]}
      />
    </Loader>
  </div>
</React.Fragment>;
```

Поддержка передачи любых параметров карты из документации https://tech.yandex.ru/maps/doc/jsapi/2.1/ref/reference/Map-docpage/

```jsx harmony
const { Loader, Map } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader load="Map" coordorder="longlat" lang="ru_RU">
      <Map
        center={[55.76, 37.64]}
        zoom={7}
        state={{
          minZoom: 12,
          controls: [],
          behaviors: ['drag', 'scrollZoom'],
          margin: [250, 60, 150, 60]
        }}
        options={{
          suppressMapOpenBlock: true,
          yandexMapDisablePoiInteractivity: true,
          copyrightLogoVisible: false,
          copyrightProvidersVisible: false,
          copyrightUaVisible: false
        }}
      />
    </Loader>
  </div>
</React.Fragment>;
```

Можно подписываться на события через пропс events

```jsx harmony
const { Loader, Map } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader load="Map" coordorder="longlat" lang="ru_RU">
      <Map
        center={[55.76, 37.64]}
        zoom={7}
        events={{ click: e => alert(e.get('coords')) }}
      />
    </Loader>
  </div>
</React.Fragment>;
```
