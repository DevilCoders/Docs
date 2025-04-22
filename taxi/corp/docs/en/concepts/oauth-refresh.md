# Renew OAuth token

This request is used to prolong your [OAuth access token](quickstart.md) lifespan.

## Request syntax

```
POST https://business.taxi.yandex.ru/api/oauth/refresh
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`token_expires_at` | The renewed token expiration date. | String


## Request example

```
POST https://business.taxi.yandex.ru/api/oauth/refresh
...
Authorization: <OAuth token>

```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "token_expires_at": "2020-01-14T16:37:13+00:00",
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The client is not authorized.

