# Delete a department

This request is used to delete an entry with a department name.

## Request syntax

```
DELETE https://business.taxi.yandex.ru/api/1.0/client/{client id}/department/{department id}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Request example

```
DELETE  https://business.taxi.yandex.ru/api/1.0/client/233e....8fd7/department/2f07...71f34c53

...Authorization: <OAuth token>

```

## Response example

An example response to this request looks like this:

```no-highlight
{}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The record with the specified parameters wasn't found.

