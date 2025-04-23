# Core Pht Proxy

Maps photos public proxy for avatars images. Allow to upload and download ugc photos.

Personal photos request must have passport cookie authorization. Public photos are available without an autorization.

## HTTP codes

| HTTP code | Response | Explanation |
|---|---|---
| 200 Ok | proto ||
| 400 Bad Request |  | Request parameters malformed |
| 401 Unauthorized |  | No valid cookie |
| 403 Forbidden |  | User does not have access to this object |
| 404 Not Found |  | Database object or handler not found |
| 500 Internal Server Error |  | Contact developers |

## Upload API

### Upload a photo.
`
 PUT      /v1/photos/my/upload?filename=&ll=
`
    Input: jpeg image
    Output: HTTP 200 MyPhoto - already uploaded, ll and filename updated.
            HTTP 201 MyPhoto - created
    Param: filename - source image filename
           ll - optional lon,lat of the uploaded photo

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
curl -v --cookie "Session_id=.." -X PUT -H "Content-Type: image/jpeg" "http://core-pht-proxy.maps.yandex.ru/v1/photos/upload?filename=1.jpg&ll=37,55&format=tet" --data-binary @- < ~/Desktop/pano2.jpg
`

### Download unpublished photo
GET /v1/photos/my/download?photo_id=&size_name=
    photo_id - photo id
    size_name - orig, XL, XS, M, XXXL, 5XL .. etc

    200 Ok request returns a valid jpeg image.
Example:
`
curl -v --cookie "Session_id=.." "http://core-pht-proxy.maps.yandex.ru/v1/photos/my/download?"
`

### Download published photo
GET /v1/photos/download?photo_id=&size_name=
    photo_id - photo id
    size_name - orig, XL, XS, M, XXXL, 5XL .. etc

    200 Ok request returns a valid jpeg image.
Example:
`
curl -v "http://core-pht-proxy.maps.yandex.ru/v1/photos/my/download?"
`
no cookies autorization required, image is published and allowed without and authorization

