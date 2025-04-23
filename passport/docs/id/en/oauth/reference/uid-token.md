# Getting a token by user UID

{% note warning %}

The method described below isn't intended for general use. If you're sure that you need it, write to the [oauth@](mailto:oauth@yandex-team.ru) mailing list and tell us about your case.

{% endnote %}


In exceptional cases, tokens can be obtained using a user's UID. This method is available only from the Yandex network and is protected by permissions that can be requested in the [oauth@](oauth@yandex-team.ru) mailing list.

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
    
- ![](../_images/code.png)
    
- Each token request must pass the user's real IP address. By default the user's address is the `Remote-Addr` header value. If the request to Yandex.OAuth is sent through a proxy server or backend, the address should be passed in the `user_ip` parameter.
    
    Proxied requests should be sent to the following OAuth servers:
    
    - For external production services: `oauth-internal.yandex.ru`.
    
    - For internal production services: `oauth-internal.yandex-team.ru`.
    
    - For release candidates: `oauth-rc-internal.yandex.ru`.
    
    - For test versions: the main URL, `oauth-test.yandex.ru`.
    

Request format:

```no-highlight
POST /token HTTP/1.1
Host: oauth.yandex.ru
X-Forwarded-For: 198.51.100.3
Content-type: application/x-www-form-urlencoded
Content-Length: `<`request body length`>`
[Authorization: Basic `<`encoded string client_id:client_secret`>`]

   grant_type=assertion
   assertion=`<`user UID`>`
[& client_id=`<`app ID`>`]
[& client_secret=`<`app password`>`]
[& x_meta=`<`string`>`]
```

### Required parameters {#required}

Parameter | Description
----- | -----
`grant_type` | A method used to request a token. To get a token by UID, specify the “assertion” value.
`assertion` | UID of the user to issue the OAuth token for.

### Advanced parameters {#advanced}
-----
`client_id` | Application ID. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/client/my){% endif %} (click the app name to open its properties). This parameter is required if the [Authorization header](#app-auth) wasn't specified in the request.
`client_secret` | App password. Available in the [app properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties). This parameter is required if the [Authorization header](#d14e31) wasn't specified in the request.
`x_meta` | A text string that can be added to the OAuth token. This string is returned each time the token is checked in the Black box (the [oauth](http://doc.yandex-team.ru/blackbox/reference/method-oauth.xml) method). The maximum string size is 65,523 bytes.


## Response format {#response}

Yandex.OAuth returns the response in a JSON document.

#### The token is successfully issued

The token is returned along with its lifetime if limited:

```javascript
{
  "access_token": "{{ access-token }}",
  "token_type": "bearer",
  "expires_in": 124234123534
 }
```

Key | Description
----- | -----
`access_token` | An OAuth token with the requested rights or with the rights specified when registering the app.
`token_type` | Type of token issued. Always takes the “bearer” value.
`expires_in` | Token lifetime in seconds. {% if audience == "internal" %}Not included in the response for tokens with unlimited lifetime.{% endif %}


#### An error occurred

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

## Error codes {#error-table}

Common codes and error descriptions are shown in the table:

#|
|| HTTP response code | Error code | Description ||
|| 400 | invalid_request | Invalid request format (for example, a required parameter isn't specified). ||
|| 400 | invalid_grant | The UID specified in the [assertion](#assertion) parameter value isn't found or is not a number. ||
|| 400 | unsupported_grant_type | The passed `grant_type` parameter value isn't supported. ||
|| 400 or 401 | invalid_client | Returned in the following cases:
- The app with the specified ID wasn't found or is blocked.
- An invalid password was passed for the specified app ID.

The 401 HTTP response code is returned if the app ID and password were passed in the `Authorization` header. Otherwise, the 400 HTTP code is returned. ||
|| 401 | Basic auth required | The `Authorization` header specifies the authorization type other than “Basic”. ||
|| 401 | Malformed Authorization header | The `Authorization` header is generated incorrectly. ||
|| 400 or 401 | unauthorized_client | The app hasn't been approved by the moderator yet, or tokens for it can't be received with the specified `grant_type` parameter value.

The 401 HTTP response code is returned if the app ID and password were passed in the `Authorization` header. Otherwise, the 400 HTTP code is returned. ||
|#


