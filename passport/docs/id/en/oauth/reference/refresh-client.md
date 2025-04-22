# Updating a token

Getting a token in exchange for a refresh token:

1. The app sends a [POST request with the refresh token](#get-token).
    
1. {{ service }} returns a token and a new refresh token in the [response body](#token-body).
    

{% note info "Note" %}

The main token may not be updated if the remaining lifetime is long enough and there is no need to issue a new token. We recommend updating long-lived tokens every three months.

{% endnote %}


The token can be saved in the app and used for API requests until its [lifetime expires](../concepts/ya-oauth-intro.md). The token should be available only to your app, so we don't recommend saving it in browser cookies, open configuration files, and so on.

## Exchange of refresh token for OAuth token {#get-token}

The app sends a refresh token, as well as its ID and password in the POST request.

```no-highlight
POST /token HTTP/1.1
Host: oauth.yandex.com
Content-type: application/x-www-form-urlencoded
Content-Length: <request body length>
[Authorization: Basic <encoded string `client_id:client_secret`>]

   grant_type=refresh_token
 & refresh_token=<refresh_token>
[& client_id=<app ID>]
[& client_secret=<app password>]
```

### Required parameters {#required}

Parameter | Description
----- | -----
`grant_type` | The method used to request the OAuth token. If you use a refresh token, specify the “refresh_token” value.
`refresh_token` | Refresh-token received from {{ service }} together with the OAuth token. The tokens have the same lifetime.

### Advanced parameters {#advanced}

Parameter | Description
----- | -----
`client_id` | Application ID. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties). You can also pass the password and app ID in the [authorization header](#token-body-title).
`client_secret` | App password. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties). You can also pass the password and app ID in the [authorization header](#token-body-title).


You can also send the app ID and password in the `Authorization` header by encoding the `<client_id>:<client_secret>` string with the Base64 method.
 If {{ service }} receives the `Authorization` header, the `client_id` and `client_secret` parameters in the request body are ignored.

## Format of response with token {#token-body-title}

{{ service }} returns the OAuth token, refresh token, and their lifetime in JSON format:

```javascript
200 OK
Content-type: application/json

{
  "access_token": "{{ access-token }}",
  "refresh_token": "{{ refresh-token }}",
  "token_type": "bearer",
  "expires_in": 124234123534
}
```

Key | Description
----- | -----
`access_token` | An OAuth token with the requested rights or with the rights specified when registering the app.
`refresh_token` | A token that can be used to [extend the lifetime](refresh-client.md) of the corresponding OAuth token.
`token_type` | Type of token issued. Always takes the “bearer” value.
`expires_in` | Token lifetime in seconds. {% if audience == "internal" %}Not included in the response for tokens with unlimited lifetime.{% endif %}


If a token couldn't be issued, the response contains a description of the error:

```javascript
{
  "error_description": "<error description>",
  "error": "<error code>"
}
```

Error codes:

- `invalid_client`: The app with the specified ID (the `client_id` parameter) wasn't found or is blocked. This code is also returned if the `client_secret` parameter passed an invalid app password.
- `invalid_grant`: Invalid or expired refresh token. This code is also returned if the refresh token belongs to another application (doesn't match the passed client_id).
- `invalid_request`: Invalid request format (one of the parameters isn't specified, specified twice, or isn't passed in the request body).
- `unauthorized_client`: The app was rejected during moderation or is awaiting moderation.
- `unsupported_grant_type`: Invalid `grant_type` parameter value.
- `Basic auth required`: The authorization type specified in the `Authorization` header is not `Basic`.
- `Malformed Authorization header`: The `Authorization` header isn't in `<client_id>:<client_secret>` format, or this string isn't Base64-encoded.

