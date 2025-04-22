# Requesting user information

When you request information about a user, the Yandex ID API returns all the data that the OAuth token specified in the request has permissions for.

A request for information about a Yandex user is formed like this:

{% list tabs %}

- Recommended method

  ```no-highlight
  GET https://login.yandex.ru/info?
  [  format=json | xml | jwt]
  [& jwt_secret=<Secret key>]
  & with_openid_identity=1 | yes | true]

  Authorization: OAuth <OAuth token>
  ```

- Insecure method

  In this method, the OAuth token is sent in the GET request parameter and can be saved openly in the browser history or in the access    logs of any intermediate host. The saved OAuth token may be used by a hacker.
  
  ```no-highlight
  GET https://login.yandex.ru/info?
  [  format=json | xml| jwt]
  [& with_openid_identity=1 | yes | true]
  [& oauth_token=<OAuth token>]
  ```
{% endlist %}

Request parameters:

#|
|| **Parameter** | **Value** | **Description** ||
|| `format` | xml / json/ jwt | Format for returned data. 

Possible values:
  - "json" — Returns a JSON document. This value is used by default if the parameter is not specified in the request.
  - "xml" — Returns an XML document.
  - "jwt" — Returns a [JSON Web Token](../concepts/jwt.md). ||
|| `jwt_secret` | <Secret_key> | The secret that will be used to sign JWT. If the parameter is not passed, the OAuth app's client_secret will be used instead. 
We recommend that you do not pass this parameter. ||
|| `with_openid_identity` | 1 / yes / true | Whether to request OpenID identities that the user could have obtained from Yandex. The list is included in the [response](response.md) in the JSON array or XML element `openid_identities`.

To request identities, set the value to “1”, “yes”, or “true”. If any other value is set, the parameter is ignored.

This parameter is used when [migrating from Yandex OpenID](../concepts/openid-migrate.md) to the Yandex ID API. ||
|| `oauth_token` | <OAuth token> | An OAuth access token that gives permission to access the user's account data using the Yandex ID API. The contents of the [response](response.md) depend on the permissions that are granted by the OAuth token specified in the request.

The OAuth token must be specified in the request in one of the following ways:
- In the `Authorization` HTTP header, each time the Yandex ID API is called, specifying the token type before its value (recommended method): `Authorization: OAuth <OAuth token>`
- In the `oauth_token` parameter value (insecure method, not recommended): `oauth_token=<OAuth token>` ||
|#

