# Device token

Yandex.OAuth allows you to request a token for an app on a specific device. To do this, specify the device ID and its name in the request for a token or confirmation code (the `device_id` and `device_name` parameters described in the request formats in this document). The user can see this name on the [access control page]{% if lang == "en" %}(https://passport.yandex.com/profile/access){% endif %} in Yandex ID. If you only specify an ID without a name, the token will be marked as issued for an unknown device.

{% note info "Attention" %}

An app can have up to 20 tokens linked to a user's devices. If {{ service }} issues a new device token for the app, the oldest token stops working.

{% endnote %}

## Revoking a token on a specific device {#device-token-revoke}

A token issued for a specific device can be revoked with a request to {{ service }}, for example, to ensure that the user logs out of the account.

To revoke a token, send it to {{ service }} with the app ID and password.

### App authentication {#app-auth}

In requests to {{ service }}, specify the ID and password generated when registering the app.

You can pass them in a request in different ways:

- In the `Authorization` header, in the `<client_id>:<client_secret>` line, encoded with the base64 method. In this case, you should specify the basic authorization method (`Basic`).
    
    Header example:
    
    ```no-highlight
    Authorization: Basic NDc2MDE4N2Q4MWJjNGI3Nzk5NDc2YjQycjUxMDM3MTM6ZjI1YmViZjk5MWZmNDE5ODkzZGIyNTU3MjhlNGUxZGU=
    ```
    
- In the POST request body, in the `client_id` and `client_secret` parameters. These parameters must be passed all at once.
    

If {{ service }} gets the `Authorization` header, the `client_id` and `client_secret` parameters in the request body are ignored.

### Request format {#cleartext}

The request should be sent over HTTPS using the POST method.

Token revocation request format:

```no-highlight
POST /revoke_token HTTP/1.1
Host: oauth.yandex.ru
Content-type: application/x-www-form-urlencoded
Content-Length: `<`request body length`>`
[Authorization: Basic `<`encoded string client_id:client_secret`>`]

   access_token=<revoked token>
[& client_id=`<`app ID`>`]
[& client_secret=`<`app password`>`]
```

### Required parameter

Parameter | Description
----- | -----
`access_token` | The OAuth token you want to withdraw.

### Advanced parameters

Parameter | Description 
----- | -----
`client_id` | Application ID. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties). This parameter is required if it wasn't specified in the [authorization header](#app-auth) request.
`client_secret` | App password. Available in [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties).This parameter is required if it wasn't specified in the [authorization header](device-token.md#app-auth) request.


### Response format {#response}

Yandex.OAuth returns the response in a JSON document.

{% list tabs %}

- The token was successfully revoked or was already invalid

  The response is returned with the 200 HTTP code and the following body:

  ```javascript
  {
    "status": "ok"
  }
  ```

- An error occurred

  If the request failed, the response is returned with the HTTP error code and its description:

  ```javascript
  {
    "error_description": "Client not found",
    "error": "invalid_client"
  }
  ```
  Key | Description
  ----- | -----
  `error_description` | The error description is written in natural language.
  `error` | Error code. The list of possible codes is shown in the table below.

{% endlist %}

### Error codes {#error-table}

#|
|| **HTTP response code** | **Error code** | **Description** ||
|| 400 | invalid_request | Invalid request format (for example, a required parameter isn't specified). ||
|| 400 | invalid_grant | The passed token doesn't belong to the specified application. ||
|| 400 or 401 | invalid_client | 
Returned in the following cases:
- The app with the specified ID wasn't found or is blocked.
- An invalid password was passed for the specified app ID.

The 401 HTTP response code is returned if the app ID and password were passed in the `Authorization` header. Otherwise, the 400 HTTP code is returned. || 
|| 400 | unsupported_token_type | The token cannot be revoked because the device ID wasn't specified when requesting this token (the `device_id` parameter).

If the token can't be revoked, you can just delete it from local storage so that the app loses access to the user's data. ||
|#

