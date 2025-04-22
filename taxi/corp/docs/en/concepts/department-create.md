# Create a new department

This request is used to create a record for a new department.

## Request syntax

```
POST https://business.taxi.yandex.ru/api/1.0/client/{client ID}/department/
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

The data for the new department is transferred in the request body as a JSON file:

Field | Description | Format
----- | ----- | -----
`parent_id` | Parent department ID (`null` — for the root department). | String
`name` | Department name. | String


## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`_id` | Department identification number. | String


## Request example

```
POST https://business.taxi.yandex.ru/api/1.0/client/233e725b0511459da7b38cb24f2d8fd7/department/
...
Authorization: <OAuth token>


{
       "parent_id": "233e725b0511459da7b38cb24f2d8fd7",
       "name": "Some department"
}
```

## Response example

An example response to this request looks like this:

```no-highlight
{
        "_id": "2f07049ecedb43b0b0be506071f34c53"
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `400`: An unknown parameter or a parameter with an invalid value was passed in the request.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `406`: A record with the specified parameters already exists.

