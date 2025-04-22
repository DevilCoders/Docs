# Delete a user

This request is used to delete a client's user.

## Request syntax

```
DELETE https://business.taxi.yandex.ru/api/1.0/client/{client ID}/user/{user ID}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`_id` | The user's ID number. | String


## Request example

```
DELETE https://business.taxi.yandex.ru/api/1.0/client/a2d...d09/user/620d2bsdfdebc8341b3471
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
        "_id": "620d2bsdfdebc8341b3471"
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The record with the specified parameters wasn't found.

