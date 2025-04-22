# Photo Backoffice internal backend

## Production endpoint:
http://core-pht-bk.maps.yandex.net

## Testing endpoint:
http://core-pht-bk.common.testing.maps.yandex.net

## Request requirements
Every request must be performed with TVM `ServiceTicket` and `UserTicket`.
Every handler supports `format=protobuf/text/json`. Text/json are not supposed to be used in production environment. Default is protobuf.
Every updating request returns http header `X-Ya-Sync-Token`. The header must be included in any further requests.

## Response codes general principles
| HTTP code | Response | Explanation |
|---|---|---
| 200 Ok | proto or empty ||
| 201 Created | proto ||
| 400 Bad Request |  | Request parameters malformed |
| 401 Unauthorized |  | No valid user ticket |
| 403 Forbidden |  | User does not have access to this object |
| 404 Not Found |  | photoId or handler not found |
| 409 Conflict |  | concurrent update for the same object |
| 500 Internal Server Error |  | Contact developers |

# Handlers

# Get photo by id
`
    GET     /v1/photos/get?photo_id=
`
    Output: HTTP 200 Photo

# Approve or reject photo
`
    POST    /v1/photos/approve?photo_id=
    POST    /v1/photos/reject?photo_id=
`
    Output: HTTP 200 Photo
    Param: photo_id


# Update photo
`
 POST      /v1/photos/update?photo_id=
`
     Input: PhotoUpdate
     Output: HTTP 200 Photo
     Param: photo_id - photo in status APPROVED or PUBLISHED

# Find photos by status
`
    GET    /v1/photos/find[?author_public_id=][&status=][&base_id=][&before_limit=][&after_limit]
`
    Output: HTTP 200 Photos
    Param: author_public_id - find photos of user with given public_id
           status - find photos with given status
           base_id, before_limit, after_limit - pagination parameters

    Filter examples:
    * load photos of user USER: `/v1/photos/find?author_public_id=USER`
    * load photos with status STATUS: `/v1/photos/find?status=STATUS`

    Either `before_limit` or `after_limit` must be specified.
    Forbidden to request more than 1000 photos.
    Pagination examples:
    * load first N photos: `/v1/photos/find?after_limit=N`
    * load last N photos: `/v1/photos/find?before_limit=N`
    * load A photos after photo with id X (does not include X):
    `/v1/photos/find?base_id=X&after_limit=A`
    * load B photos before photo with id X (does not include X):
    `/v1/photos/find?base_id=X&before_limit=B
    * load A+B+1 photos around photo with id X (includes X):
    `/v1/photos/find?base_id=X&after_limit=A&before_limit=B

# Start release review
`
    POST   /v1/releases/start_review[?max_photos=1000]
`
    Output: HTTP 200
    Param: max_photos - maximum number of photos, that could be in RELEASE_REVIEW status
                        optional, 1000 is default and maximum

    Status of all APPROVED photos is changed to RELEASE_REVIEW.
    Could be called multiple times to add more photos.
    These photos can be fetched using `/v1/photos/find?status=RELEASE_REVIEW&after_limit=1000` and reviewed
    `max_photos` can be used to guarantee fetching without pagination

# Finish release review
`
    POST /v1/releases/finish_review
`
    Output: HTTP 200

    Status of all RELEASE_REVIEW photos is changed to RELEASE_APPROVED.
    Should be called after rejecting all bad photos from release review.


# Ban photo upload for user
`
    POST /v1/users/ban?public_id=&reason=[&ban_days=]
`
    Param: public_id - public_id of user to block photo upload
           reason - private explanation of ban
           ban_days - number of days until ban expires


# Unban photo upload for user
`
    POST /v1/users/unban?public_id=&reason=
`
    Param: public_id - public_id of user to unblock photo upload
           reason - private explanation of unban

