# Get a parent department list

This request is used to get information about parent departments.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client id}/department
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`departments[]` | Department list. | String
`departments[]._id` | Department ID. | String
`departments[].name` | Department name. | String
`departments[].parent_id` | Parent department ID. | String


## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/client/233e725b0511459da7b38cb24f2d8fd7/department
...Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "departments": [
    { 
            "_id": "524ac5dcadf8410aa5f5217f44933970",
            "name": "Moscow office",
            "parent_id": null
    },
    {
            "_id": "233e725b0511459da7b38cb24f2d8fd7",
            "name": "Novosibirsk office",
            "parent_id": null

    }
  ] 
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.

