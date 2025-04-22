# The user enters the code in Yandex.OAuth

On some devices (such as TVs), entering a confirmation code may be inconvenient. In this case, you can ask the user to enter the code on the [Device authorization]{% if lang == "en" %}(https://oauth.yandex.ru/device){% endif %} page.

Steps for getting a token in this case:
1. The app requests two codes: `device_code` for the device and `user_code` for the user. The lifetime of these codes is 10 minutes. After this time, the codes must be requested again.
    
1. The app simultaneously:
    
    - Prompts the user to enter `user_code` on the [Device authorization]{% if lang == "en" %}(https://oauth.yandex.ru/device){% endif %} page.
    - Starts requesting an OAuth token periodically by passing `device_code`.
    
1. The user enters the correct code before its lifetime expires.
    
1. Yandex.OAuth returns a token in response to the next app request.

{% note info "Tip" %}

You can get debug tokens for the app [manually](../tasks/get-oauth-token.md).

{% endnote %}


The token can be saved in the app and used for API requests until its [lifetime expires](../concepts/ya-oauth-intro.md). The token should be available only to your app, so we don't recommend saving it in browser cookies, open configuration files, and so on.

## Requesting confirmation codes {#get-codes}

The application must request confirmation codes using the HTTP POST method

```no-highlight
POST /device/code
Host: oauth.yandex.com
client_id=<app ID>
[& device_id=<device ID>]
[& device_name=<device name>]
[& scope=<requested required rights>]
```
### Required parameter {#required}

Parameter | Description
----- | -----
`client_id` | Application ID. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties).

### Advanced parameters {#advanced}

#|
|| **Parameter** | **Description** ||
|| `device_id` | Unique ID of the device the token is requested for. To ensure uniqueness, just generate a [UUID]{% if lang == "en" %}
(https://en.wikipedia.org/wiki/Universally_unique_identifier){% endif %} once and use it every time a new token is requested from this device.

{% if audience == "internal" %}

To learn how these IDs are obtained for Yandex mobile apps, see the page on Wiki: [https://wiki.yandex-team.ru/YandexMobile/Server/AccountsBinding/](https://wiki.yandex-team.ru/YandexMobile/Server/AccountsBinding/)

{% endif %}

The ID must be from 6 to 50 characters long. Only printable [ASCII]{% if lang == "en" %}
(https://en.wikipedia.org/wiki/ASCII){% endif %} characters are allowed (with codes from 32 to 126).

{% note info "Attention" %}

An app can have up to 20 tokens linked to a user's devices. If {{ service }} issues a new device token for the app, the oldest token stops working.

{% endnote %}

Learn more about tokens for individual devices at [Token for a device](../concepts/device-token.md). ||
||`device_name` | The name of the device to show users. Up to 100 characters.

For mobile devices, we recommend passing the device name specified by the user. 

If a name is missing, the name can be taken from the device model, OS name and version, and so on.

If the `device_name` parameter is sent without the `device_id` parameter, it is ignored. {{ service }} can only issue a regular token that is not linked to a device.

If the `device_id` parameter is sent without the `device_name` parameter, the token is marked as issued for an unknown device in the user interface. ||
|| `scope` | A list of access rights currently required by the application, separated by a space. Rights must be requested from the list defined when registering the application. To see the allowed rights, go to [https://oauth.yandex.com/client/&lt;client_id&gt;/info]{% if lang == "en" %}(https://oauth.yandex.com/client/%3Cclient_id%3E/info){% endif %}, specifying the app ID instead of <client_id>.

If the `scope` and `optional_scope` parameters aren't passed, the token will be issued with the rights specified when registering the app.

This parameter allows you to get a token only with the rights currently required by the app.

{% note info "Note" %}

All access rights are requested at once via the `scope` and `optional_scope` parameters, are considered optional, and are not required for the app to function. The user decides which requested optional rights to grant.

{% endnote %} ||
|#

## Response with confirmation codes {#response}

{{ service }} returns the code for the user and the information for the token request:

```javascript
HTTP 200 OK

Content-type: application/json

{
  "device_code": "3e2a5a5c0e02439aa78a23442721848c",
  "user_code": "h5nbcr6c",
  "verification_url": "https://oauth.yandex.ru/device",
  "interval": 5,
  "expires_in": 300
}
```

Property | Description
----- | -----
`device_code` | The code to request the OAuth token in the next step.
`user_code` | The code the user should enter to allow access to their data.
`verification_url` | URL of the page where the user should enter the code from the `user_code` property.
`interval` | The minimum interval with which the app must request the OAuth token. If requests come more often, Yandex.OAuth may respond with an error.
`expires_in` | Code pair lifetime. After this period, a token for them can't be received and the procedure needs to be started again.


## Entering the user code {#entering}

The user should enter the code from the `user_code` property on the page at the URL from the `verification_url` property. If the code is entered correctly, Yandex.OAuth suggests allowing or denying access for the app.

Example of such a page:
![](../_images/oauth-device.png)

## Requesting a token with the device code {#get-token}

The app sends the device code as well as its ID and password in a POST request.

```no-highlight
POST /token HTTP/1.1
Host: oauth.yandex.com
Content-type: application/x-www-form-urlencoded
Content-Length: <request body length>
[Authorization: Basic <encoded string `client_id:client_secret`>]

   grant_type=device_code
   code=<device code obtained with the previous request>
[& client_id=<app ID>]
[& client_secret=<app password>]
```
### Required parameters {#required-1}

#|
|| **Parameter** | **Description** ||
||`grant_type` | The method used to request the OAuth token. 

If you use a confirmation code, specify the “authorization_code” value.||
||`code` | Confirmation code received from {{ service }}. The lifetime of this code is 10 minutes. After this time, the code must be requested again. ||
|#

### Advanced parameters {#advanced-1}

#|
|| **Parameter** | **Description** ||
|| `client_id` | Application ID. Available in [application properties]{% if lang == "en" %}https://oauth.yandex.com/{% endif %} (click the app name to open its properties).

The app ID and password must be passed either in the request parameters or in the [Authorization header](#auth-header). ||
||`client_secret` | App password. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties).

The password and app ID must be passed either in the request parameters or in the [Authorization header](#auth-header). ||
|#

You can also send the app ID and password in the `Authorization` header by encoding the `<client_id>:<client_secret>` string with the Base64 method. If {{ service }} receives the `Authorization` header, the `client_id` and `client_secret` parameters in the request body are ignored.

## Response with OAuth token {#token-body-title}

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

