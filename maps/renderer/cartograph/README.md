[[toc]]

## RTC: Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks | Balancers |
| ------- | ------------- | -------------- | ----------------- |-----------|
| stable | [maps_core_renderer_cartograph_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_cartograph_stable/) | [core-renderer-cartograph.stable](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-cartograph-stable-panel-main/) | [maps_core_renderer_cartograph_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_cartograph_stable&view=tiles&limit=200) | [core-renderer-cartograph.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-renderer-cartograph.maps.yandex.net/show/)|
| testing | [maps_core_renderer_cartograph_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_cartograph_testing/) | [core-renderer-cartograph.testing](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-cartograph-testing-panel-main/) | [maps_core_renderer_cartograph_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_cartograph_testing&view=tiles&limit=200) | [core-renderer-cartograph.testing.maps.n.yandex.ru](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-renderer-cartograph-testing-slb)|

## Hosts
| Stage      | URL |
| ---------- | --- |
| Stable     | https://core-renderer-cartograph.maps.yandex.net |
| Testing    | https://core-renderer-cartograph.testing.maps.n.yandex.ru |


## API

### GET /
Simple embbed style editor


### POST /tiles
Render tile with a style passed in the request body.

#### Required params
* **x**: X coord
* **y**: Y coord
* **z**: Zoom level

#### Optional params
* **tile_format**: `png` or `vec`. *Default: `png`*
* **zmin**: Min zoom level for multizoom `vec` tile. *Default: value of `z`*
* **zmax**: Max zoom level for multizoom `vec` tile. *Default: value of `z`*
* **lang**: Locale. *Default: `ru_RU`*
* **scale**: Image scale. *Default: 1*
* **mode**: Style mode if applicable (`basic` or `night`). *Default: None or `basic`*
* **indoor_level**: Indoor level id

#### Body
JSON with layers and resource dictionary:
```
{
    "layers" : [
        ...
    ],
    "resources": {
        ...
    }
}
```

### GET /tiles
Renderer tile with a style from Stylerepo.

Accepts the **same params as** `POST tiles` handle and additional params.

#### Required params
* **revision**: Stylerepo revision id
* **styleset**: Stylerepo styleset name


### POST /inspect
Inspect features in close proximity to a given coordinate.

Returns GeoJSON feature collection object.

#### Required params
* **ll**: `lon,lat` coordinate
* **z**: Zoom

#### Optional params
* **lang**: Locale. *Default: `ru_RU`*
* **indoor_level**: Indoor level id

#### Body
Style in the same format as `POST tiles` handle


### GET /vmap2/tiles
Same as `GET /tiles`, but default `tile_format` is `vec`.

### GET /icons
Get icon by vector `id`. Icongen-generated icons support color customization.

#### Required params
* **id**

#### Optional params
* **с1**: Icon primary color (background or fill)
* **с2**: Icon secondary color (glyph or stroke)
* **с3**: Icon tertiary color (shadow or stroke)
* **scale**: Image scale. *Default: 1*


### GET /glyphs

#### Required params
* **font_id**
* **range**

### GET /system_data_sets
Return an JSON array with preloaded data sets uris (`map`, `trf`, etc.).

## Dev

### Style schema
<https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/renderer/style>

### Env variables
* **RENDERER_CARTOGRAPH_DEBUG** Debug log level
* **RENDERER_CARTOGRAPH_PRELOAD_FONTS** Preload fonts

### Run local yacare app in http mode
```
cd $ARCADIA_ROOT/maps/cartograph
ya make -r bin
env YCR_MODE=http:<port> YCR_THREADS=<thread_num> ./bin/renderer-cartograph
open http://<host>:<port>
```
