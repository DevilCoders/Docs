# Edit department name

You can use this request to change the department name.

## Request syntax

```
PUT https://business.taxi.yandex.ru/api/1.0/client/{client ID}/department/{department ID}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

The data about the new department name is sent in the request body as a JSON file:

Field | Description | Format
----- | ----- | -----
`parent_id` | Parent department ID (`null` — for the root department). | String
`name` | Department name. | String


## Request example

```
PUT https://business.taxi.yandex.ru/api/1.0/client/233e...fd7/department/2f0....34c53
...Authorization: <OAuth token>


{
       "parent_id": "233e725b0511459da7b38cb24f2d8fd7",
       "name": "Some department"
}

```

## Response example

An example response to this request looks like this:

```no-highlight
{}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `400`: An unknown parameter or a parameter with an invalid value was passed in the request.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The specified record wasn't found.

