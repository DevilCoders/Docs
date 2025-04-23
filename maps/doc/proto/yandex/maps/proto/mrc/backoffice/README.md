## Backoffice API 

* Предназначен для межсервисного взаимодействия: из пользовательского ui запросы сюда не приходят.

### Headers
### Request requirements
Every request must be pefrormed with TVM `ServiceTicket`

### Response codes
| HTTP code | Explanation |
|---|---|
| 201 Created |  |
| 400 Bad Request | Request parameters or body malformed |
| 401 Unauthorized | No valid service ticket |
| 500 Internal Server Error | Contact developers |

### API

#### **/v2/objects/create**

**Method**   | POST |
-------------|-|
**Params**   | |
**Description** | Добавить новый объект с фотографиями. |
**Request Body** | [CreateObjectRequest][Backoffice] |
**Response Body** | [CreateObjectResponse][Backoffice] |
**Пример запроса**:
```
type: ObjectType::BARRIER
geometry {
  point {
    lon: 37.247873
    lat: 55.563219
  }
}
comment: "Шлагбаум"
photos {
  image : <bytes>
  shooting_point {
    point {
      point {
        lon: 37.247873
        lat: 55.563219
      }
    }
    direction {
      azimuth: 90.0
      tilt: 0.0
    }
  }
  taken_at {
    value: 1605873286
    tz_offset: 0
    text: "2020-11-20T11:54:46"
  }
}
photos {
  ...
}
nmaps_object_id: "some_id"
```

#### **/v2/photos/create**

**Method**   | POST |
-------------|-|
**Params**   | |
**Description** | Добавить фотографии. |
**Request Body** | [CreatePhotoRequest][Backoffice] |
**Response Body** | [CreatePhotoResponse][Backoffice] |
**Пример запроса**:
```
photo {
  image : <bytes>
  shooting_point {
    point {
      point {
        lon: 37.247873
        lat: 55.563219
      }
    }
    direction {
      azimuth: 90.0
      tilt: 0.0
    }
  }
  taken_at {
    value: 1605873286
    tz_offset: 0
    text: "2020-11-20T11:54:46"
  }
}
```

[Backoffice]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrc/backoffice/backoffice.proto
[Readme]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrc/backoffice/README.md
