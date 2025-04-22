# Debug token

Applications that use OAuth can be tested using debug tokens. To get them, open [Yandex.OAuth]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} in the browser with the required parameters. Debug tokens, like all others, can always be [revoked](../reference/token-invalidate.md). To get a token manually:
  1. When [registering](register-client.md) or editing an app, click the **Substitute URL for development** link in the **Platforms** → **Web services** → **Callback URI** field.
  1. Log in to Yandex with the user account the app should request access to.
  1. Click the following link:`https://oauth.yandex.com/authorize?response_type=token&client_id=<app ID>`
     The ID is available in the [application properties]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (click the app name to open its properties).
  1. If you didn't allow access to this application or the lifetime of the issued token expired, you'll be redirected to confirm access. Click **Allow** to confirm the issuing of the token.

Yandex.OAuth redirects you to the token page, adding the token data after the # character:

```javascript
https://oauth.yandex.ru/verification_code#
    access_token=<new OAuth token>
  & expires_in=<token lifetime in seconds<codeph>
```

Parameter | Description 
------ | ------
`access_token` | An OAuth token with the requested rights or with the rights specified when registering the app.
`expires_in` | Token lifetime in seconds. {% if audience == "internal" %}Not included in the response for tokens with unlimited lifetime.{% endif %}

If the token couldn't be issued, the OAuth server adds an error code to the URL:

```javascript
https://oauth.yandex.ru/verification_code#
    error=<error-code>
```

Error codes: 
  - `access_denied`: The user denied access to the app.
  - `unauthorized_client`: The app was rejected during moderation or is awaiting moderation. Also returned if the app is blocked.

#### Related information: 
  - [Authorization procedure](../concepts/ya-oauth-intro.md#authorization-scheme)
  - [Registering an app](register-client.md)
