# Region list

This request is used to receive information about all of a client's ride regions.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client ID}/geo_restrictions? 
limit=<number of records>
&offset=<number of records to skip>
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

The request may contain the following optional arguments:

- `limit`: The number of records to output. If this parameter is omitted, information about the first 100 records is returned.
    
- `offset`: The number of records to skip. If this parameter is omitted, information starting from the first record is returned.
    

Records in a response are sorted by the date and time of the latest update.

## Response field description

Responses may contain the following fields:

#|
||**Field**|**Description**|**Format**||
||`_id` | ID. | String||
||`name` | Name. | String||
||`geo_type` | Geo restriction type. Currently only "circle" is supported. | String||
||`geo` | Geo restriction description. Contains the following fields:
- `center`: The coordinates of the center point.
- `radius`: The distance from the center (in meters). | Object||
|#


## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/client/7498c21b09a04172bd41472f6a7c0af3/geo_restrictions?limit=50
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
    "limit": 50,
    "offset": 0,
    "items": [
      {
        "_id": "008157832119489bb7379f39fbdc6917",
        "geo": {
          "center": [
            72.368212,
            54.989342
          ],
          "radius": 500
        },
        "geo_type": "circle",
        "name": "Office 1"
},
      {
        "_id": "b45efcaa04014fff997c2683ef91f0de",
        "geo": {
          "center": [
            37.642639,
            55.734894
          ],
          "radius": 200
        },
        "geo_type": "circle",
"name": "Office 2"
}
    ]
  }
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `400`: An unknown parameter was passed in the request.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.

