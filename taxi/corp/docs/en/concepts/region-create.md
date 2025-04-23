# Create a new region

This request creates a new region for a client's rides.

## Request syntax

```
POST https://business.taxi.yandex.ru/api/1.0/client/{client ID}/geo_restrictions
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

The data for the new region is transferred in the request body as a JSON file:

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
POST https://business.taxi.yandex.ru/api/1.0/client/7498c21b09a04172bd41472f6a7c0af3/geo_restrictions
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
- `400`: An unknown parameter or a parameter with an invalid value was passed in the request. For example, a record with the specified data already exists.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.

