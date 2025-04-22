# `Vector Map Rendering Engine`

Rendering engine for vector map data.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-vector/ |
| CI | https://teamcity.yandex-team.ru/project.html?projectId=maps_Vector&tab=projectOverview |
| Statistics | TBD |

## Debian packages

* [yandex-maps-ui-vector](https://c.yandex-team.ru/packages/yandex-maps-ui-vector)
* [yandex-maps-ui-vector-static](https://c.yandex-team.ru/packages/yandex-maps-ui-vector-static)

## Public programming interface
Vector engine build provides number of modules for jsapi 2.1

| Name | Type | Description |
|---|---|---|
| `vectorEngine.implementation.VectorMapLayer` | [ILayer](https://github.yandex-team.ru/mapsapi/jsapi-v2/blob/master/src/interface/i-layer.js) | Scheme map layer ['yandex#map'](https://tech.yandex.ru/maps/doc/jsapi/2.1/ref/reference/Map-docpage/#method_detail__setType-param-type) |
| `vectorEngine.implementation.VectorTrafficLayer` | [ILayer](https://github.yandex-team.ru/mapsapi/jsapi-v2/blob/master/src/interface/i-layer.js) | Actual traffic and road events [layer](https://tech.yandex.ru/maps/doc/jsapi/2.1/ref/reference/traffic.provider.Actual-docpage/) |

More about module defining see [here]( https://tech.yandex.ru/maps/doc/jsapi/2.1/dg/concepts/modules-docpage/). Only 'ymaps' namespace is now supported.

## Documentation
* [Wiki](https://wiki.yandex-team.ru/maps/dev/ui/products/vector/)
* In the repo:
  * [Vector API adapter](./src/vector_render_engine/adapters/vector_api/doc/vector_api_adapter.md)
  * [Text rendering](./src/vector_render_engine/font/doc/font.md)
  * [Images](./src/vector_render_engine/billboard/doc/image_management.md)
  * [Testing](./tests/doc/test.md)
  * [Deploy and version config](./debian.md)

## Known clients

* [JS API v2.1](https://github.yandex-team.ru/mapsapi/jsapi-v2#jsapi-v21)

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
