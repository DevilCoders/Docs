# The user enters the code in the app

Some apps (such as console apps or those installed on Smart TVs) may not be able to [get the confirmation code from the URL](auto-code-client.md). In this case, the user should get the code from Yandex.OAuth and enter it in the app.

Getting a token in exchange for the code entered by the user:

1. The app opens the [{{ service }} page](#get-code) in the browser, where the user can allow access to their data.
    
    If the browser isn't available on the device where the app is installed, the user will have to open the URL on their computer. To make it more user-friendly, provide a QR code or a short link.
    
1. The user goes to the page that opens, or uses a short link and allows access for the app.
    
1. {{ service }} outputs a confirmation code. (For this, specify the URL `https://oauth.yandex.ru/verification_code` in the **Callback URL** app property.)
    
1. The app sends a [POST request with the code](#get-token).
    
1. {{ service }} returns a token in the [response body](#token-body).
    

{% note info "Tip" %}

You can get debug tokens for the app [manually](../tasks/get-oauth-token.md).

{% endnote %}


The token can be saved in the app and used for API requests until its [lifetime expires](../concepts/ya-oauth-intro.md). The token should be available only to your app, so we don't recommend saving it in browser cookies, open configuration files, and so on.

## Getting a confirmation code {#get-code}

1. The app should direct the user to {{ service }} at the following URL:
    
    ```no-highlight
    https://oauth.yandex.com/authorize?
    response_type=code
    & client_id=<app ID>
    [& device_id=<device ID>]
    [& device_name=<device name>]
    [& redirect_uri=<redirect URL>]
    [& login_hint=<username or email address>]
    [& scope=<requested required rights>]
    [& optional_scope=<requested optional rights>]
    [& force_confirm=yes]
    [& state=<arbitrary string>]
    ```
    
    ### Required parameters {#required}

    Parameter | Description
    ----- | -----
    `response_type` | Expected response. When you request the confirmation code, specify the “code” value.
    `client_id` | Application ID. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties).

    ### Advanced parameters {#advanced}

    #|
    || `device_id` | Unique ID of the device the token is requested for. To ensure uniqueness, just generate a [UUID]{% if lang == "en" %}(https://en.wikipedia.org/wiki/Universally_unique_identifier){% endif %} once and use it every time a new token is requested from this device.
    
    {% if audience == "internal" %}
    
    To learn how these IDs are obtained for Yandex mobile apps, see the page on Wiki: [https://wiki.yandex-team.ru/YandexMobile/Server/AccountsBinding/](https://wiki.yandex-team.ru/YandexMobile/Server/AccountsBinding/)
    
    {% endif %}
    
    The ID must be from 6 to 50 characters long. Only printable [ASCII]{% if lang == "en" %}(https://en.wikipedia.org/wiki/ASCII){% endif %} characters are allowed (with codes from 32 to 126).
    
    {% note info "Attention" %}
    
    An app can have up to 20 tokens linked to a user's devices. If {{ service }} issues a new device token for the app, the oldest token stops working.
    
    {% endnote %}

    Learn more about tokens for individual devices at [Token for a device](../concepts/device-token.md). ||
    || `device_name` | The name of the device to show users. Up to 100 characters.
    
    For mobile devices, we recommend passing the device name specified by the user. If a name is missing, the name can be taken from the device model, OS name and version, and so on.
    
    If the `device_name` parameter is sent without the `device_id` parameter, it is ignored. {{ service }} can only issue a regular token that is not linked to a device.
    
    If the `device_id` parameter is sent without the `device_name` parameter, the token is marked as issued for an unknown device in the user interface. ||
    || `redirect_uri` | The URL to redirect the user to after they allow or deny access to the app. By default, the first Callback URI specified in the app settings is used (**Platforms** → **Web services** → **Callback URI**).
    
    The parameter value can only contain URLs listed in the app settings. If the match isn't exact, this parameter is ignored. ||
    || `login_hint` | Explicit indication of the account the token is requested for. The Yandex account username, as well as the Yandex.Mail or Yandex.Mail for Domain address, can be passed in the parameter value.
    
    This parameter allows you to help the user log in to Yandex with the account that the app needs access to. When {{ service }} receives this parameter, it checks the user's authorization:
    
    - If the user is already logged in with the appropriate account, {{ service }} just asks for access permission.
    - If the user isn't logged in with the appropriate account, they see the Yandex login form where the login field is filled in with the parameter value. Remember that the token won't necessarily be requested for the specified account: the user can erase the pre-filled username and log in with any other.
      
    If this parameter indicates a nonexistent account, {{ service }} will only be able to inform the user. The app will have to request the token again. ||
    || `scope` | A list of access rights currently required by the application, separated by a space. Rights must be requested from the list defined when registering the application. To see the allowed rights, go to [https://oauth.yandex.com/client/&lt;client_id&gt;/info]{% if lang == "en" %}(https://oauth.yandex.com/client/%3Cclient_id%3E/info){% endif %}, specifying the app ID instead of <client_id>.
    
    If the `scope` and `optional_scope` parameters aren't passed, the token will be issued with the rights specified when registering the app.
    
    This parameter allows you to get a token only with the rights currently required by the app.
    
      {% note info "Note" %}
    
      All access rights are requested at once via the `scope` and `optional_scope` parameters, are considered optional, and are not required for the app to function. The user decides which requested optional rights to grant.
    
      {% endnote %} ||
    || `optional_scope` | A list of optional access rights, separated by a space, that aren't required for the app functionality. Optional rights are requested in addition to the rights specified in the `scope` parameter. Optional rights must be requested from the list defined when registering the application. To see the allowed rights, go to [https://oauth.yandex.com/client/&lt;client_id&gt;/info]{% if lang == "en" %}(https://oauth.yandex.com/client/%3Cclient_id%3E/info){% endif %}, specifying the app ID instead of <client_id>.
    
    If the `scope` and `optional_scope` parameters aren't passed, the token will be issued with the rights specified when registering the app.
    
    The user decides which requested optional rights to grant. The token will be issued with the rights specified in the `scope` parameter, and the rights selected by the user from the list specified in the `optional_scope` parameter.
    
    This parameter can be used, for example, if the app needs an email to register the user, and access to the portrait is preferred, but not required.
    
      {% note info "Note" %}
    
      All access rights requested at once via the `scope` and `optional_scope` parameters are considered optional.
    
      {% endnote %} ||
    || `force_confirm` | Indicates that the user must request permission to access the account (even if the user already allowed access to this app). After receiving this parameter, Yandex.OAuth will prompt the user to allow access to the application and choose the Yandex account.
    
    The parameter is processed if its value is “yes”, “true”, or “1”. If any other value is set, the parameter is ignored. ||
    || `state` | The status bar that {{ service }} returns without changes. The maximum allowed string length is 1024 characters.
    
    Can be used, for example, to protect against [CSRF attacks]{% if lang == "en" %}(https://en.wikipedia.org/wiki/Cross-site_request_forgery){% endif %} or identify the user the token is requested for. ||
    |#    
    
1. When a user allows access to their data, {{ service }} outputs a confirmation code. The lifetime of this code is 10 minutes. After this time, the code must be requested again.
    
![](../_images/code.png)

## Exchanging a confirmation code for a token {#get-token}

The app sends the code as well as its ID and password in a POST request.

```no-highlight
POST /token HTTP/1.1
Host: oauth.yandex.com
Content-type: application/x-www-form-urlencoded
Content-Length: <request body length>
[Authorization: Basic <encoded string `client_id:client_secret`>]

   grant_type=authorization_code
 & code=<confirmation code>
[& client_id=<app ID>]
[& client_secret=<app password>]
[& device_id=<device ID>]
[& device_name=<device name>]
```

### Required parameters {#required-1}

Parameter | Description
----- | -----
`grant_type` | The method used to request the OAuth token. If you use a confirmation code, specify the “authorization_code” value.
`code` | Confirmation code received from {{ service }}. The lifetime of this code is 10 minutes. After this time, the code must be requested again.

### Advanced parameters {#advanced-1}

#|
|| Parameter | Description ||
|| `client_id` | Application ID. Available in [application properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties). The app ID and password must be passed either in the request parameters or in the [Authorization header](#auth-header). ||
|| `client_secret` | App password. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties). The password and app ID must be passed either in the request parameters or in the [Authorization header](#auth-header). ||
|| `device_id` | ID of the device that the token is requested for.If the ID was specified in the [device_id](#device-id) parameter when requesting a confirmation code, the `device_id` and `device_name` parameters are ignored when requesting a token. ||
|| `device_name` | The name of the device the token is requested for. If the `device_id` parameter was passed when requesting the confirmation code, the `device_id` and `device_name` parameters are ignored when requesting the token. ||
|#

You can also send the app ID and password in the `Authorization` header by encoding the `<client_id>:<client_secret>` string with the Base64 method. If {{ service }} receives the `Authorization` header, the `client_id` and `client_secret` parameters in the request body are ignored.

## Format of response with token {#token-body-title}

{{ service }} returns the OAuth token, refresh token, and their lifetime in JSON format:

```javascript
200 OK
Content-type: application/json

{
  "token_type": "bearer",
  "access_token": "{{ access-token }}",
  "expires_in": 124234123534,
  "refresh_token": "{{ refresh-token }}",
  "scope": "login:info login:email login:avatar"
}
```

Property | Description
----- | -----
`token_type` | Type of token issued. Always takes the “bearer” value.
`access_token` | An OAuth token with the requested rights or with the rights specified when registering the app.
`expires_in` | Token lifetime in seconds. {% if audience == "internal" %}Not included in the response for tokens with unlimited lifetime.{% endif %}
`refresh_token` | A token that can be used to [extend the lifetime](refresh-client.md) of the corresponding OAuth token.
`scope` | Rights requested by the developer or specified when registering the app. The `scope` field is optional and is returned if OAuth provided a token with a smaller set of rights than requested.


The lifetime of the refresh token is the same as the OAuth token lifetime.

If a token couldn't be issued, the response contains a description of the error:

```javascript
{
  "error_description": "<error description>",
  "error": "<error code>"
}
```

Error codes:

- `authorization_pending`: The user didn't enter the confirmation code yet.
- `bad_verification_code`: The passed `code` parameter value isn't a 7-digit number.
- `invalid_client`: The app with the specified ID (the `client_id` parameter) wasn't found or is blocked. This code is also returned if the `client_secret` parameter passed an invalid app password.
- `invalid_grant`: Invalid or expired confirmation code.
- `invalid_request`: Invalid request format (one of the parameters isn't specified, specified twice, or isn't passed in the request body).
- `invalid_scope`: The app rights changed after the confirmation code was generated.
- `unauthorized_client`: The app was rejected during moderation or is awaiting moderation.
- `unsupported_grant_type`: Invalid `grant_type` parameter value.
- `Basic auth required`: The authorization type specified in the `Authorization` header is not `Basic`.
- `Malformed Authorization header`: The `Authorization` header isn't in `<client_id>:<client_secret>` format, or this string isn't Base64-encoded.

