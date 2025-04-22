# Remove region

This request removes an existing ride region for a client.

## Request syntax

```
DELETE https://business.taxi.yandex.ru/api/1.0/client/{client ID}/geo_restrictions/{region ID}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`_id` | Ride region ID. | String


## Request example

```
DELETE https://business.taxi.yandex.ru/api/1.0/client/7498c21b09a04172bd41472f6a7c0af3/geo_restrictions/b45efcaa04014fff997c2683ef91f0de
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
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The specified record wasn't found.

