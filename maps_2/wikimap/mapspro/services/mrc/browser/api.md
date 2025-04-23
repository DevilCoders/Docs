# API for interaction with MRC photos

## MRC photos visualization API

### Supported layers

The Api provides the following layer types for visualizing MRC photos:
- `mrcauto`: covered edges of the automotive road graph
- `mrcpdst`: covered edges of the pedestrian road graph

### GET /tiles
Get vector tile of automotive graph coverage

| **Method** | GET |
|------------|-----|
| **Parameters** |
| x, y, z    | tile coordinates |
| zmin, zmax | range of zooms intended for rendering (allowed only for protobuf format)|
| l | visualization layer|
| v          | content version |
| vec_protocol | protobuf protocol version, possible values: `2`, `3` (default: `2`)|
| **Request Headers** |
| Accept | application/x-protobuf<br>image/png |
| **Response codes** |
| 200 | OK |
| 204 | There is no photos covering automotive road graph in this tile |
| 400 | Invalid parameters |
| 404 | There is no tile (x,y,z) in the requested content version (v) |
| **Response Headers** |
| Content-Type | application/x-protobuf<br>image/png |
| **Response body** |
| Tile contents | image, possible formats:<br>png<br>[yandex.maps.proto.renderer.vmap2.Tile](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/renderer/vmap2/tile.proto)<br>[yandex.maps.proto.renderer.vmap3.Tile](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/renderer/vmap3/tile.proto)|


### GET /version
Get version

| **Method** | GET |
|------------|-----|
| **Parameters** | No |
| Accept | application/x-protobuf<br>text/plain |
| **Response codes** |
| 200 | OK |
| **Response Headers** |
| Content-Type | application/x-protobuf<br>text/plain |
| **Response body** |
| message | version in text format or in [yandex.maps.proto.mobile_config.mapkit2.layers.FixedVersion](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mobile_config/mapkit2/layers.proto?rev=r8078622) |


## Photo navigation API

### GET /v2/photo/hotspot
Get the nearest photo to a chosen geo position in a specified layer

| **Method** | GET |
|------------|-----|
| **Parameters** |
| ll | longitude/latitude coordinates to search for a photo  |
| l  | photo layer to search the nearest photo within |
| z  | zoom level to take into account |
| **Request Headers** |
| **Response codes** |
| 200 | OK |
| 204 | No photo found for a specified layer |
| 400 | Invalid parameters |
| 404 | Invalid photo layer or version |
| **Response Headers** |
| Content-Type | application/x-protobuf |
| **Response body** |
| message | [yandex.maps.proto.mrcphoto.photo.Photo](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrcphoto/photo.proto) |

**Example response **
```
Photo {
  id: "212543802"
  image: {
    url_template: "https://core-nmaps-mrc-browser.maps.yandex.ru/feature/212543802/image?size_name=%s"
    size: [
      {
        size: "1920x1080"
        width: 1920
        height: 1080
      },
      {
        size: "284x180"
        width: 284
        height: 160
      }
    ]
    tag: []
  }
  createdAt: 1599982523
  shootingPoint: {
    point: {
      lon: 56.3254857316814
      lat: 44.0119608255359
    }
    direction: {
      azimuth: 47.0871085727737
      tilt: 0
    }
  }
  attribution: {
    author: {
      name: "anlizev"
      uri: "urn:yandex-puid:12345"
    }
    avatarImage: {
      url_template: ""
    }
  }
  annotation: {
    layer: "mrcauto"
    spatialConnection : [
      {
        photoId: "212543801"
        shootingPoint: {
          point: {
            lon: 56.3254405172859
            lat: 44.0118727627509
          }
          direction: {
            azimuth: 47.9595388670283
            tilt: 0
          }
        }
      },
      {
        photoId: "212543817"
        shootingPoint: {
          point: {
            lon: 56.3255221149054
            lat: 44.0120248499389
          }
          direction: {
            azimuth: 35.4401769339835
            tilt: 0
          }
        }
      },
      ...
    ]
    historicalConnection : [
      {
        photoId: "212542801"
        createdAt: 1599972521
      },
      {
        photoId: "212542817"
        createdAt: 1599972524
      },
      ...
    ]
  }
}
```

### GET /v2/photo/get
| **Method** | GET |
|------------|-----|
| **Parameters** |
| id | photo id  |
| l  | layer to search connected photos within |
| **Request Headers** |
| **Response codes** |
| 200 | OK |
| 400 | Invalid parameters |
| 404 | There is no photo with such ID |
| **Response Headers** |
| Content-Type | application/x-protobuf |
| **Response body** |
| message | [yandex.maps.proto.mrcphoto.photo.Photo](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrcphoto/photo.proto) |



### GET /v2/photos/get
| **Method** | GET | description |
|------------|-----|-----|
| **Parameters** |
| ids | photo ids  | comma-separated list of identifiers, e.g. 1,2,3 |
| l  | layer to search connected photos within |
| **Request Headers** |
| **Response codes** |
| 200 | OK |
| 400 | Invalid parameters |
| 404 | There is no photo with such ID |
| **Response Headers** |
| Content-Type | application/x-protobuf |
| **Response body** |
| message | [yandex.maps.proto.mrcphoto.photo.PhotoList](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrcphoto/photo.proto) |



### GET /v2/photo/strip
| **Method** | GET |
|------------|-----|
| description | Returns a photo description which is not snapped to any graph and without spatial and historical connections |
| **Parameters** |
| id | photo id  |
| **Request Headers** |
| **Response codes** |
| 200 | OK |
| 400 | Invalid parameters |
| 404 | There is no photo with such ID |
| **Response Headers** |
| Content-Type | application/x-protobuf |
| **Response body** |
| message | [yandex.maps.proto.mrcphoto.photo.Photo](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrcphoto/photo.proto) |


#### **POST /v2/track/preview**

| **Method** | POST |
|------------|-----|
| **Parameters** |
| **Request body** |
| [yandex.maps.proto.mrcphoto.PreviewRequest](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrcphoto/photo.proto) |
| **Response body** |
| [yandex.maps.proto.mrcphoto.TrackPreview](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrcphoto/photo.proto) |


Example query: `POST /v2/track/preview`

Request body
```(c++)
polyline{
  lons {
    first: 37247873
    deltas: 141449
    deltas: 219726
  }
  lats {
    first: 55563219
    deltas: 94833
    deltas: 127892
  }
}
```

Response body
```(c++)
preview {
  items {
    position {
      segment_index: 0
      segment_position: 0.0
    }
    photo_id: "1"
  }
  items {
    position {
      segment_index: 0
      segment_position: 0.9
    }
  }
  items {
    position {
      segment_index: 1
      segment_position: 0.2
    }
    photo_id: "2"
  }
  items {
    position {
      segment_index: 1
      segment_position: 0.5
    }
    photo_id: "3"
  }
}
chunk_list {
  chunks{
    subpolyline {
      begin {
        segment_index: 0
        segment_position: 0.0
      }
      end {
        segment_index: 0
        segment_position: 1.0
      }
    }
    chunk_descriptor {
      payload: "..."
    }
  }
  chunks {
    subpolyline {
      begin {
        segment_index: 0
        segment_position: 1.0
      }
      end {
        segment_index: 1
        segment_position: 1.0
      }
    }
    chunk_descriptor {
      payload: "..."
    }
  }
}
```


#### **POST /v2/track/chunk**

Annotates part of user's track with photo ids.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| **Request body** |
| [yandex.maps.proto.mrcphoto.TrackPreview.ChunkDescriptor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrcphoto/photo.proto) |
| **Response body** |
| [yandex.maps.proto.mrcphoto.TrackChunk](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrcphoto/photo.proto) |


Response body
```(c++)
photos {
  item {
    position {
      segment_index: 0
      segment_position: 1.
    }
  }
  item {
    position {
      segment_index: 1
      segment_position: 0.2
    }
    photo_id: "2"
  }
  item {
    position {
      segment_index: 1
      segment_position: 0.5
    }
    photo_id: "3"
  }
}
```
