# Get information about a department

This request is used to get information about a department.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client id}/departament/{department id}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`_id` | Department ID. | String
`name` | Department name. | String
`parent_id` | Parent department ID (`null` — for the root department). | String


## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/client/233e...fd7/department/2f0...f34c53
...Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
        "id": "524ac5dcadf8410aa5f5217f44933970",
        "name": "Moscow office",
        "parent_id": null
 }
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.

