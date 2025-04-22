# Panoramas UGC private backend

This is API documentation. SEDEM service documentation is one level up.
Every request should be made with TVM `ServiceTicket` and `UserTicket`.
Every handler supports `format=protobuf/text/json` for debugging purposes.

## HTTP codes

| HTTP code | Response | Explanation |
|---|---|---
| 200 Ok | proto ||
| 201 Created |  proto ||
| 204 No content | empty ||
| 400 Bad Request | xml | Request parameters malformed |
| 401 Unauthorized | xml | No valid user ticket |
| 403 Forbidden | xml | User does not have access to this object |
| 404 Not Found | xml | Database object or handler not found |
| 409 Conflict | xml | Database update or multipart upload conflict |
| 410 Gone | xml | The upload is Gone |
| 422 Custom error | proto Error | Protobuf error code |
| 500 Internal Server Error | XML | Contact developers |

[Protobuf Error](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/panougc/error.proto)

## Suppliers API

| Method | URI | Success | Description |
|---|---|---|---|---|---|
| GET | `/v1/suppliers/auth` | 204 | Used to check authorization |
| POST | `/v1/suppliers/agree` | 204 | Accept agreement before creating shipments  |

## Shipments API

| Method | URI | Params | Success | Error |
|---|---|---|---|---|
| GET | `/v1/shipments/get` | `shipmentId` | 200`Shipment` | - |
| GET | `/v1/shipments/geometry` | `shipmentId` | 200`ShipmentGeometry` | - |
| GET | `/v1/shipments/list` | `shipmentIds` | 200`Shipments` | - |
| GET | `/v1/shipments/find` | `[baseId]`<br>`[beforeLimit]`<br>`[afterLimit]`<br>`[filterText]` | 200`Shipments` | - |
| POST | `/v1/shipments/create` |  `name`<br>`defaultPreset`<br>`[showAuthorship]` | 201`Shipment` | 422`Error` | 
| PATCH | `/v1/shipments/update` | `shipmentId`<br>`[name]`<br>`[showAuthorship]` | 200`Shipment` | 422`Error` |
| PATCH | `/v1/shipments/submit` | `shipmentId` | 200`Shipment` | 422`Error` |
| DELETE | `/v1/shipments/delete` | `shipmentId` | 204 | 422`Error` |

[Protobuf Shipment](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/panougc/shipment.proto)

### Shipments pagination examples

| Type | Method | URL |
|---|---|---|
| Initial load | GET | `/v1/shipments/find?afterLimit=`|
| Around base | GET | `/v1/shipments/find?baseId=&beforeLimit=&afterLimit=` |
| Page down | GET | `/v1/shipments/find?baseId=&afterLimit=` (does not include base)
| Page up | GET | `/v1/shipments/find?baseId=&beforeLimit=` (does not include base) |

## Links API
| Method | URI | Params | Success | Error |
|---|---|---|---|---|
| PUT | `/v1/links/create` | `shipmentId`<br>`srcId`<br>`dstId` | 204 | 422`Error` |
| DELETE | `/v1/links/delete` | `shipmentId`<br>`srcId`<br>`dstId` | 204 | 422`Error` |

## Panoramas API

| Method | URI | Params (Body) | Success | Error |
|---|---|---|---|---|
| GET | `/v1/panoramas/get` | `panoramaId` | 200`Panorama` | - |
| GET | `/v1/panoramas/list` | `panoramaIds` | 200`Panoramas` | - |
| GET | `/v1/panoramas/find` | `shipmentId`<br>`[baseId]`<br>`[beforeLimit]`<br>`[afterLimit]`<br>`[filterText]` | 200`Panoramas` | - |
| GET | `/v1/panoramas/description` | `panoramaId` | 200`panoramas.Panorama` | - |
| POST | `/v1/panoramas/create` | (`image/jpeg`) | 200/201`Panorama` | 422`Error` | 
| PATCH | `/v1/panoramas/update` | panoramaId (`UpdatePanorama`) | 200`Panorama` | 422`Error` |
| PATCH | `/v1/panoramas/update_batch` | (`UpdatePanoramas`) | 200`Panoramas` | 422`Error` |
| DELETE | `/v1/panoramas/delete` | `panoramaId` | 204 | 422`Error`` |

[Protobuf Panorama](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/panougc/panorama.proto)
[Protobuf panoramas.Panorama](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/panoramas/panorama.proto)

### Panoramas pagination examples

| Type | Method | URL |
|---|---|---|
| Initial load | GET | `/v1/panoramas/find?shipmentId=&afterLimit=` |
| Around base | GET | `/v1/panoramas/find?shipmentId=&baseId=&beforeLimit=&afterLimit=` |
| Page down | GET | `/v1/panoramas/find?shipmentId=&baseId=&afterLimit=` (does not include base) |
| Page up | GET | `/v1/panoramas/find?shipmentId=&baseId=&beforeLimit=` (does not include base) |


## Resumable upload API

### Ручка для асинхронной загрузки панорам

#### Начинаем сессию загрузки
`
POST /v1/uploads/create
`

**Параметры:**
- md5= хеш от файла. Нужен для проверки что все куски загрузились правильно. В случае если контент уже есть на сервере позволяет ничего не загружать.
- mtime= дата модификации файла.
- length= размер файла в байтах

**Ответ:**

| HTTP status | headers | описание |
|---|---|---|
| HTTP 308 | ResumableUpload | Сервер имеет не все данные, нужно дозагружать файл кусками используя параметр uploadId |
| HTTP 200 | ResumableUpload | Сервер имеет все данные, загрузку можно считать успешной |

#### Загружаем кусок и узнаем состояние
`
PUT /v1/uploads/upload
`

**Параметры:**
- uploadId - id загрузки
- offset - смещение в байтах от начала файла

**Ответ:**

| HTTP status | headers | описание |
|---|---|---|
| HTTP 308 | ResumableUpload | Сервер имеет не все данные, нужно продолжать грузить файл кусками |
| HTTP 200 | ResumableUpload | Сервер имеет все данные, загрузку можно считать успешной |


#### Прерываем загрузку
`
DELETE /v1/uploads/delete
`

**Параметры:**

- uploadId - id загрузки.

**Ответ:**
| HTTP status | headers | описание|
|---|---|---|
| HTTP 200 |  | Загрузка отменена |


### Примеры последовательности вызовов ручек
#### Загружаем картинку которая уже есть. Находим ее по хешу и сразу возвращаем 200

**Запрос:**
`
POST /v1/uploads/create?md5=&mtime=&length=2000000
Content-Length : 0
`

**Ответ:**
`
HTTP 200
ResumableUpload {
    id: PQIADFJBJNKQWUIEQN
    length: 2000000
    offset: 2000000
}
`

#### Начинаем загрузку контента которого у нас еще нет. Возвращаем 308 и незавершенный uploadId.
**Запрос:**
`
POST /v1/uploads/create?md5=&mtime=&length=2000000
Content-Length : 0
`

**Ответ:**
`
HTTP 308
ResumableUpload {
    id: PQIADFJBJNKQWUIEQN
    length: 2000000
    offset: 0
}
`

#### Статус загрузки
**Запрос:**
`
GET /v1/uploads/get?uploadId=PQIADFJBJNKQWUIEQN
`

**Ответ:**

`
308 Resume Incomplete
ResumableUpload {
    id: PQIADFJBJNKQWUIEQN
    length: 2000000
    offset: 0
}
`

#### Загружаем не последний кусок
**Запрос:**
`
PUT /v1/uploads/upload?uploadId=PQIADFJBJNKQWUIEQN&offset=524288
Content-Length : 524288
`

**Ответ:**
`
308 Resume Incomplete
ResumableUpload {
    id: PQIADFJBJNKQWUIEQN
    length: 2000000
    offset: 524288
}
`

#### Загружаем последний кусок
**Запрос:**
`
PUT /v1/uploads/upload?uploadId=PQIADFJBJNKQWUIEQN&offset=524288
Content-Length : 1475712
`

**Ответ:**
`
200 Created
ResumableUpload {
    id: PQIADFJBJNKQWUIEQN
    length: 2000000
    offset: 2000000
}
`

#### Прерываем загрузку
`
DELETE /v1/uploads/delete?uploadId=PQIADFJBJNKQWUIEQN
`
