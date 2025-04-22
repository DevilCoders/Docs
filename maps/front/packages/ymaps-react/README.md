# ymaps-react ![Version](https://badger.yandex-team.ru/npm/@yandex-int/ymaps-react/version.svg)

## What is it?

This package provides a set of React components and helpers for [ymaps api 2.1](https://tech.yandex.ru/maps/).

## Demo
See [storybook](https://github.yandex-team.ru/pages/maps/ymaps-react/storybook-static).

## How to use it?

### Installation
```
npm i @yandex-int/ymaps-react
```

If you use typescript, don't forget to install typings for ymaps api:

```
npm i @yandex-int/jsapi-v2-types
```

### YMaps api loading

`ymaps-react` doesn't load original ymaps api, you need to load it by yourself with:
```html
<script src="https://api-maps.yandex.ru/...">
```

Async loading is supported as well but you have to add `id="ymaps-loader"` attribute to your script:
```html
<script async id="ymaps-loader" src="https://api-maps.yandex.ru/...">
```

### Components
All of the components must have `<Map>` ancestor (except `<Map>` itself) in the tree of components.

The list of provided components:
  * `<Map>`
  * `<MapEventListener>`
  * `<Layer>`
  * `<HotspotLayer>`
  * `<GeoObjectCollection>`
  * `<Placemark>`
  * `<Polyline>`
  * `<Polygon>`
  * `<Rectangle>`
  * `<Circle>`
  * `<Clusterer>`
  * `<Button>`
  * `<TypeSelector>`
  * `<RulerControl>`
  * `<SearchControl>`
  * `<TrafficControl>`
  * `<ZoomControl>`
  * `<FullscreenControl>`
  * `<GeolocationControl>`

## Helpers
The list of provided helpers:
  * `withYmaps`
  * `withMap`
  * `useMap`
  
## Geometry types
The list of provided types:
  * `PointGeometry`
  * `LineStringGeometry`
  * `PolygonGeometry`
  * `CircleGeometry`
  * `RectangleGeometry`
  * `Geometry`
