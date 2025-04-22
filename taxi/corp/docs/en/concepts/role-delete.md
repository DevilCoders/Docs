# Delete a role

This request is used to delete a record of a user role.

## Request syntax

```
DELETE https://business.taxi.yandex.ru/api/1.0/client/{client ID}/role/{role ID}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

If the request is successful, it returns an empty 200 response.

## Request example

```
DELETE https://business.taxi.yandex.ru/api/1.0/client/a2...d09/role/a94...abf
...
Authorization: <OAuth token>
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The specified record wasn't found.

