# Web app

Getting a token for a web app:

1. The app directs the user to the [{{ service }} page](#request-url), where they can allow access to their data.
    
1. The user allows access to the app.
    
1. {{ service }} redirects the user to the URL specified in the {{ callback-url }} field during [registration](../tasks/register-client.md). The token data is passed to the redirect URL after the # character.
    
    The server environment may not pass this part of the URL to the web app. In this case, you can retrieve data from the URL [with JavaScript](#js), or receive tokens with the [confirmation code](auto-code-client.md).
    
1. The app gets the [redirect URL](#response-url) and retrieves the token.
    

{% note info "Tip" %}

You can get debug tokens for the app [manually](../tasks/get-oauth-token.md).

{% endnote %}


The token can be saved in the app and used for API requests until its [lifetime expires](../concepts/ya-oauth-intro.md). The token should be available only to your app, so we don't recommend saving it in browser cookies, open configuration files, and so on.

## URL for requesting the token {#request-url}

The app should direct the user to {{ service }} at the following URL:

```no-highlight
https://oauth.yandex.com/authorize?
   response_type=token
 & client_id=<app ID>
[& device_id=<device ID>]
[& device_name=<device name>]
[& redirect_uri=<redirect address>]
[& login_hint=<user name or email address>]
[& scope=<requested required rights>]
[& optional_scope=<requested optional rights>]
[& force_confirm=yes]
[& state=<arbitrary string>]
[& display=popup]
```

### Required parameters {#required}

Parameter | Description
----- | -----
`response_type` | Expected response. The token request should contain the “token” value.
`client_id` | Application ID. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties).


### Advanced parameters {#advanced}

#|
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

{% endnote %}||
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

Can be used, for example, to protect against [CSRF attacks]{% if lang == "en" %}(https://en.wikipedia.org/wiki/Cross-site_request_forgery){% endif %}  or identify the user the token is requested for. ||
|| `display` | Indicates a lightweight layout (without standard Yandex navigation) for the [access permission page](../concepts/ya-oauth-intro.md).

You should request a lightweight layout, for example, if you want to display a permission page in a small pop-up window.

Only the “popup” value is processed. Other values are ignored. ||
|#


## The {{ service }} response {#response-url}

The token data is passed in the redirect URL after the # character.If the server environment doesn't allow the app to get this part of the URL, you can extract the data [with JavaScript](#js) or get tokens with the [confirmation code](console-client.md).

Token URL format:

```no-highlight
{{ callback }}#
   access_token=<new OAuth token>
 & expires_in=<token lifetime in seconds>
 & token_type=bearer
[& state=<state parameter value in the request>]
[& scope=<access rights>]
      
```

Parameter | Description
----- | -----
`access_token` | The OAuth token with the requested rights or with the rights specified when registering the app.
`expires_in` | Token lifetime in seconds. {% if audience == "internal" %}Not included in the response for tokens with unlimited lifetime.{% endif %}
`token_type` | Type of token issued. Always takes the “bearer” value.
`state` | The `state` parameter value from the original request, if this parameter was passed.
`scope` | Rights requested by the developer or specified when registering the app. The `scope` field is optional and is returned if OAuth provided a token with a smaller set of rights than requested.


If the token could not be issued, then {{ service }} adds the error code and description to the URL. The description is in the language of the OAuth domain that the request was sent to: for example, for `oauth.yandex.com`, the text will be returned in {% if lang == "en" %}English{% endif %}.

Format of the URL with error information:

```no-highlight
{{ callback }}#
   error=<error code>
 & error_description=<error description>
[& state=<state parameter value in the request>]
```

Error codes:

- `access_denied`: The user denied access to the app.
- `unauthorized_client`: The app was rejected during moderation or is awaiting moderation. Also returned if the app is blocked.

## Extracting URL data with JavaScript {#js}

The URL part after the # character is available in the `document.location.hash` JavaScript property.

For example, you can get the token like this:

```javascript
var token = /access_token=([^&]+)/.exec(document.location.hash)[1];
```

