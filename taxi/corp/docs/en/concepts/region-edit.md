# Edit a region

This request edits an existing ride region for a client.

## Request syntax

```
PUT https://business.taxi.yandex.ru/api/1.0/client/{client ID}/geo_restrictions/{region ID}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

New data for the ride region is passed in the request body in JSON format:

#|
||**Field** | **Description** | **Format**||
||`name` | Name. | String||
||`geo_type` | Geo restriction type. Currently only "circle" is supported. | String||
||`geo` | Geo restriction description. Contains the following fields:
- `center`: The coordinates of the center point.
- `radius`: The distance from the center (in meters). | Object||
|#

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`_id` | Ride region ID. | String


## Request example

```
PUT https://business.taxi.yandex.ru/api/1.0/client/7498c21b09a04172bd41472f6a7c0af3/geo_restrictions/b45efcaa04014fff997c2683ef91f0de
  {
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
```

## Response example

An example response to this request looks like this:

```no-highlight
  {
      "_id": "b45efcaa04014fff997c2683ef91f0de"
  }
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `400`: An unknown parameter or a parameter with an invalid value was passed in the request.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The specified record wasn't found.

