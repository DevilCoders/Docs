# Superweb maps

React components for data visualization on maps.
Layered data drawing is powered by [Deck.GL](https://deck.gl/), a WebGL-based framework.
Two map providers are currently supported - [Yandex maps](https://a.yandex-team.ru/arcadia/maps/front/packages/ymaps3) and [Google maps](https://developers.google.com/maps/documentation/javascript/overview). The library is not limited by these provider, our approach allows to add new providers if needed.

## Installation

Published on [npm.yandex-team.ru](https://oko.yandex-team.ru/pkg/@superweb/maps)

```shell
npm install --save @superweb/maps
```

...or if you are using yarn:

```shell
yarn add @superweb/maps
```

## Usage

### Yandex Maps

You don't need an api key to work with Yandex maps. Instead of an api key, a domain check is used by ymaps3 maintainers. If you have a domain other than Yandex, contact the [MAPSAPI](https://st.yandex-team.ru/createTicket?queue=MAPSAPI) queue.

```jsx
import { Map } from "@superweb/maps";
// Сonnection of styles is necessary for Yandex maps to work.
import "@superweb/maps/dist/style.css";

const [viewport, setViewport] = useState({
  lat: 55.698,
  lng: 37.611,
  zoom: 12,
});

<Map provider="yandex" viewport={viewport} onViewportCahnge={setViewport} />;
```

### Google Maps

```jsx
import { Map } from "@superweb/maps";

const [viewport, setViewport] = useState({
  lat: 55.698,
  lng: 37.611,
  zoom: 12,
});

<Map
  provider="google"
  providerOptions={{ apiKey: "YOU_API_KEY" }}
  viewport={viewport}
  onViewportCahnge={setViewport}
/>;
```

## Layers

The order of layers on the map corresponds to the order they are added in JSX

### ScatterplotLayer

Layer for drawing points. Documentation: https://deck.gl/docs/api-reference/layers/scatterplot-layer

```jsx
import { Map, ScatterplotLayer } from "@superweb/maps";

// Sample data can be downloaded from the link:
// https://raw.githubusercontent.com/visgl/deck.gl-data/master/website/bart-stations.json
const data = [
  {
    name: "Colma (COLM)",
    code: "CM",
    address: "365 D Street, Colma CA 94014",
    exits: 4214,
    coordinates: [-122.466233, 37.684638],
  },
];

<Map provider="yandex" viewport={viewport}>
  <ScatterplotLayer
    data={data}
    opacity={0.8}
    pickable={true}
    stroked={true}
    filled={true}
    radiusScale={6}
    radiusMinPixels={1}
    radiusMaxPixels={100}
    lineWidthMinPixels={1}
    getPosition={(d) => d.coordinates}
    getRadius={(d) => Math.sqrt(d.exits)}
    getFillColor={(d) => [255, 140, 0]}
    getLineColor={(d) => [0, 0, 0]}
  />
</Map>;
```

#### Result:

![image](https://jing.yandex-team.ru/files/boyur/Screenshot%202022-07-05%20at%2016.50.57.png =600x400)
