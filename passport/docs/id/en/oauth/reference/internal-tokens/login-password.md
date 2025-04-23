# Token in exchange for username and password

{% note info "Important" %}

The method described below isn't intended for general use. If you're sure that you need it, write to the [oauth@](mailto:oauth@yandex-team.ru) mailing list and tell us about your case.

{% endnote %}


{{ service }} allows you to exchange a Yandex username and password for the OAuth token of the account.

## App authentication {#app-auth}

In requests to {{ service }}, specify the ID and password generated when registering the app.

You can pass them in a request in different ways:

- In the `Authorization` header, in the `<client_id>:<client_secret>` line, encoded with the base64 method. In this case, you should specify the basic authorization method (`Basic`).
    
    Header example:
    
    ```no-highlight
    Authorization: Basic NDc2MDE4N2Q4MWJjNGI3Nzk5NDc2YjQycjUxMDM3MTM6ZjI1YmViZjk5MWZmNDE5ODkzZGIyNTU3MjhlNGUxZGU=
    ```
    
- In the POST request body, in the `client_id` and `client_secret` parameters. These parameters must be passed all at once.
    

If {{ service }} gets the `Authorization` header, the `client_id` and `client_secret` parameters in the request body are ignored.

## Request format {#cleartext}

Request requirements:

- The token request to Yandex.OAuth should be sent over HTTPS Protocol using the POST method.
    
- ![](../../_images/code.png)
    
- Each token request must pass the user's real IP address. By default the user's address is the `Remote-Addr` header value. If the request to Yandex.OAuth is sent through a proxy server or backend, the address should be passed in the `user_ip` parameter.
    
    Proxied requests should be sent to the following OAuth servers:
    
    - For external production services: `oauth-internal.yandex.ru`.
    
    - For internal production services: `oauth-internal.yandex-team.ru`.
    
    - For release candidates: `oauth-rc-internal.yandex.ru`.
    
    - For test versions: the main URL, `oauth-test.yandex.ru`.
    

Token request format by username and password:

```no-highlight
POST /token HTTP/1.1
Host: oauth.yandex.ru
X-Forwarded-For: 198.51.100.3
Content-type: application/x-www-form-urlencoded
Content-Length: `<`request body length`>`
[Authorization: Basic `<`encoded string client_id:client_secret`>`]

   grant_type=password
 & username=`<`login`>`
 & password=`<`password`>`
[& client_id=`<`app ID`>`]
[& client_secret=`<`app password`>`]
[& device_id=<device ID>]
[& device_name=<device name>]
[& x_meta=`<`string`>`]
[& x_captcha_key=`<`captcha key`>`]
[& x_captcha_answer=`<`entered captcha`>`]
[& x_captcha_scale_factor=`<`captcha display size`>`]
```
### Required parameters {#required}

#| 
|| **Parameter** | **Description** ||
|| `grant_type` | A method used to request a token.

To get a token in exchange for a username and password, specify the “password” value. ||
|| `username` | Yandex username. ||
|| `password` | Yandex account password in URL encoded format.

The password entry form must correctly process all characters that may be part of the Yandex account password. ||
|#

### Advanced parameters {#advanced}

#| 
|| **Parameter** | **Description** ||
|| `client_id` | Application ID. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/client/my){% endif %} (click the app name to open its properties).This parameter is required if it wasn't specified in the [authorization header](#app-auth) request. ||
|| `client_secret` | App password. Available in [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties). This parameter is required if it wasn't specified in the authorization header request. ||
|| `device_id` | Unique ID of the device the token is requested for. To ensure uniqueness, just generate a [UUID]{% if lang == "en" %}(https://en.wikipedia.org/wiki/Universally_unique_identifier){% endif %} once and use it every time a new token is requested from this device.

{% if audience == "internal" %}

To learn how these IDs are obtained for Yandex mobile apps, see [the page on Wiki](https://wiki.yandex-team.ru/YandexMobile/Server/AccountsBinding/).

{% endif %}

The ID must be from 6 to 50 characters long. Only printable [ASCII]{% if lang == "en" %}(https://en.wikipedia.org/wiki/ASCII){% endif %} characters are allowed (with codes from 32 to 126).

{% note info "Restriction" %}

An app can have up to 20 tokens linked to a user's devices. If {{ service }} issues a new device token for the app, the oldest token stops working.

{% endnote %} 

Learn more about tokens for individual devices at [Token for a device](../../concepts/device-token.md). ||
|| device_name | The name of the device to show users. Up to 100 characters.

For mobile devices, we recommend passing the device name specified by the user. If a name is missing, the name can be taken from the device model, OS name and version, and so on.

If the `device_name` parameter is sent without the `device_id` parameter, it is ignored. {{ service }} can only issue a regular token that is not linked to a device.

If the `device_id` parameter is sent without the `device_name` parameter, the token is marked as issued for an unknown device in the user interface. ||
|| `x_meta` | A text string that can be added to the OAuth token. This string is returned each time the token is checked in the Black box (the [oauth](http://doc.yandex-team.ru/blackbox/reference/method-oauth.xml) method).

The maximum string size is 65,523 bytes. ||
|| `x_captcha_key` | Captcha ID.

{{ service }}  can ask the user to enter a captcha to prevent password guessing. For this, the `x_captcha_url` and `x_captcha_key` keys are included in the [answer](#login-password/response) 

The captcha ID should be passed in the repeated request along with the correct captcha answer (the `x_captcha_answer` parameter). ||
|| `x_captcha_answer` | Answer to captcha entered by the user.

Must be passed along with the captcha ID (the `x_captcha_key` parameter). ||
|| `x_captcha_scale_factor` | The size of the captcha image to generate for the user if they need to enter a captcha. Yandex.OAuth uses [nbg queue](https://wiki.yandex-team.ru/yandex-captcha/types/). 

Supported values:
- 2: 400×120 pixels.
- 3: 600×180 pixels.

The default size is 200×60 pixels. ||
|#

## Response format {#response}

Yandex.OAuth returns the response in a JSON document.

{% list tabs %}

- The token is successfully issued

  The token is returned along with its lifetime if limited:

  ```javascript
  {
    "access_token": "{{ access-token }}",
    "token_type": "bearer",
    "expires_in": 124234123534
   }
  ```

  Key | Description 
  ------ | ------
  `access_token` | An OAuth token with the requested rights or with the rights specified when registering the app.
  `token_type` | Type of token issued. Always takes the “bearer” value.
  `expires_in` | Token lifetime in seconds. {% if audience == "internal" %}Not included in the response for tokens with unlimited lifetime.{% endif %}

- An error occurred

  If the request failed, the response is returned with the HTTP error code and its description:

  ```javascript
  {
    "error_description": "Client not found",
    "error": "invalid_client"
  }
  ```

  Key | Description 
  ------ | ------
  `error_description` | The error description is written in natural language.
  `error` | Error code. The list of possible codes is shown in the table below.

- You need to enter a captcha

  When {{ service }} gets a token request by username and password, it may require a captcha. In this case, the response includes a link to the captcha image and its ID:

  ```javascript
  {
    "x_captcha_url": "http://u.captcha.yandex.net/image?key=30UPr3JdmuyfOww6elhKJb9l30CcKHRt",
    "x_captcha_key": "30UPX3JdmuyDOww4elhKJt9l30CcKHRt",
    "error_description": "CAPTCHA required",
    "error": "invalid_client"
  }
  ```

    Key | Description 
  ------ | ------
  `x_captcha_url` | Link to the captcha image to show to the user. The value entered by the user must be passed to Yandex.OAuth in the repeated request, in the [x_captcha_answer](#x-captcha-answer) parameter.
  `x_captcha_key` | Captcha ID. Send the ID to Yandex.OAuth in the repeated request to indicate which captcha the user entered. The [x_captcha_key](#x-captcha-key) parameter should be used for this.
  `error_description` | The error description is written in natural language.
  `error` | Error code. The list of possible codes is shown in the table below.

{% endlist %}

## Error codes {#error-table}

#|
|| **HTTP response code** | **Error code** | **Description** ||
|| 400 | invalid_request | Invalid request format (for example, a required parameter isn't specified). ||
|| 400 | invalid_grant | The username/password pair didn't pass authentication. || 
|| 400 | unsupported_grant_type | The passed `grant_type` parameter value isn't supported. ||
|| 400 or 401 | invalid_client | Returned in the following cases:

- The app with the specified ID wasn't found or is blocked.
    
- An invalid password was passed for the specified app ID.
    
The 401 HTTP response code is returned if the app ID and password were passed in the `Authorization` header. Otherwise, the 400 HTTP code is returned. || 
|| 401 | Basic auth required | The `Authorization` header specifies the authorization type other than Basic”. ||
|| 401 | Malformed Authorization header | The `Authorization` header is generated incorrectly. || 
|| 400 or 401 | unauthorized_client | The app hasn't been approved by the moderator yet, or tokens for it can't be received with the specified `grant_type` parameter value.

The 401 HTTP response code is returned if the app ID and password were passed in the `Authorization` header. Otherwise, the 400 HTTP code is returned. || 
|| 403 | 403 | 

Returned in the following cases:

- Captcha entry required (`error_description="CAPTCHA required"`).
    
    The response includes a link to the captcha image and its ID.
    
- The passed captcha answer is incorrect for the specified ID (`error_description="Wrong CAPTCHA answer"`).
    
- The password must be changed for the specified account (`error_description="Password change required"`).
    
- Password expired (`error_description="Expired password"`).
    
    The error can only occur for accounts subscribed to SID 67. ||
|#



