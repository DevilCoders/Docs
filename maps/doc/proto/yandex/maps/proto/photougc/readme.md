# Photo UGC internal backend

## Production endpoint:
http://core-pht-ugc.maps.yandex.net

## Testing endpoint:
http://core-pht-ugc.testing.maps.n.yandex.ru

## Request requirements
Every request must be performed with TVM `ServiceTicket` and `UserTicket`.
Every handler supports `format=protobuf/text/json`. Text/json are not supposed to be used in production environment. Default is protobuf.
Every updating request returns http header `X-Ya-Sync-Token`. The header must be included in the further request.

## Response codes general principles
| HTTP code | Response | Explanation |
|---|---|---
| 200 Ok | proto or empty ||
| 201 Created | proto ||
| 400 Bad Request |  | Request parameters malformed |
| 401 Unauthorized |  | No valid user ticket |
| 403 Forbidden |  | User does not have access to this object |
| 404 Not Found |  | photo_id or handler not found |
| 409 Conflict |  | concurrent update for the same object |
| 500 Internal Server Error |  | Contact developers |


# Handlers

## View public photos

### Get a published photo metadata
`
 GET      /v1/photos/get?photo_id=
`
     Output: HTTP 200 Photo

Example:
`
curl "http://core-pht-ugc.testing.maps.n.yandex.ru/v1/photos/get?photo_id=7&format=text"
`

### List published photos by toponym URI
`
GET      /v1/photos/list?uri=&limit=
`

Params:\
    uri - [encoded toponym URI](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo/GUIDE.md#uri), starts with  `ymapsbm1%3A//geo`\
    limit - maximum number of returned photos (should not exceed 30)

Example: https://core-pht-ugc.common.testing.maps.yandex.net/v1/photos/list?uri=ymapsbm1%3A%2F%2Fgeo%3Fll%3D37.587%252C55.735%26spn%3D0.001%252C0.001%26text%3D%25D0%25A0%25D0%25BE%25D1%2581%25D1%2581%25D0%25B8%25D1%258F%252C%2520%25D0%259C%25D0%25BE%25D1%2581%25D0%25BA%25D0%25B2%25D0%25B0%252C%2520%25D1%2583%25D0%25BB%25D0%25B8%25D1%2586%25D0%25B0%2520%25D0%25A2%25D0%25B8%25D0%25BC%25D1%2583%25D1%2580%25D0%25B0%2520%25D0%25A4%25D1%2580%25D1%2583%25D0%25BD%25D0%25B7%25D0%25B5%252C%252011%25D1%258156&format=text

## Manage photos by owner

### Get photo metadata
`
 GET      /v1/photos/my/get?photo_id=
`
     Output: HTTP 200 MyPhoto

### Upload a photo 
`
 PUT      /v1/photos/my/upload?filename=&ll=&target_ll=
`

    Input: jpeg image
    Output: HTTP 200 MyPhoto - already uploaded, ll and filename updated.
            HTTP 201 MyPhoto - created
    Param: filename - source image filename
           ll - optional lon,lat of the uploaded photo
           target_ll - optional target lon, lat of the uploaded photo

    Resumable upload is not supported.

    Once a photo is uploaded and it has coordinates, the photo going to be moderated and published without any further questions and approvements.
    The photo without coordinates is not moderated until the coordinates is set.

    The photo is visible in the owner personal account immediately after the upload.
    The photo owner may delete the photo before publication. The publication includes moderation and takes some time.
    Even published photos may be deleted any time layer.

    The photo may be rejected by the moderation system. It In this case it's not going to be published but is still visible in the owner personal account.

    Use cases for the upload photo handler:
        - Upload with attached lon/lat.
        - Upload a photo without lon/lat. Set lon/lat of the uploaded photo later.
        - Upload geotagged images from Disk.
        - Multiple upload. Only one by one.

Example:
`
curl -X PUT -H "Content-Type: image/jpeg" "http://core-pht-ugc.testing.maps.n.yandex.ru/v1/photos/my/upload?uid=1&filename=1.jpg&ll=37,55&format=text" --data-binary @- < ~/Desktop/pano2.jpg
`

### Delete an uploaded photo
`
 DELETE     /v1/photos/my/delete?photo_id=
`

Delete photo from personal account and prevent its publication.


Example:
`
curl -X DELETE "http://core-pht-ugc.testing.maps.n.yandex.ru/v1/photos/my/delete?photo_id=7"
`

### Update photo metadata
`
 PUT    /v1/photos/my/update?photo_id=
`
     Input: PhotoUpdate
     Output: HTTP 200 MyPhoto

