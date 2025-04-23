# Client information

This request is used to get basic information about a client.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/auth
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`yandex_login` | The Yandex account name. | String
`role` | The role in the dashboard. For clients, the `client` value is returned. | String
`client_id` | The client's contract ID number. | String


## Request example

```
GET https://business.taxi.yandex.ru/api/auth
...
Authorization: <OAuth token>

```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "yandex_login": "example-company",
  "role": "client",
  "client_id": "a2...d09"
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The client is not authorized.

