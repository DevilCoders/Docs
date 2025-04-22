# `ymaps3-import`

## Configuration example

```js
// Allow imports:
// From src/map ymaps3/{raster|common|map}
// From src/raster ymaps3/{raster|common}
// From src/common ymaps3/{common}

"importsRules": {
    "src/map": [
        "ymaps3/raster",
        "ymaps3/common",
        "ymaps3/map"
    ],
    "src/raster": [
        "ymaps3/common",
        "ymaps3/raster"
    ],
    "src/common": [
        "ymaps3/common"
    ]
}
```
