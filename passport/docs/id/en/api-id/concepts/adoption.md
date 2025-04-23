# Connecting to the Yandex ID API

To use the Yandex ID API in a web application, you need to:

- [Register](../../oauth/tasks/register-client.md) your application on [Yandex.OAuth]{% if lang == "en" %}(https://oauth.yandex.com/){% endif %}.
- Implement receiving and processing OAuth tokens in the application.
- Provide an interface for users to log in via Yandex.

## Registering an application on Yandex.OAuth {#oauth-register}

Login via Yandex requires that you obtain an OAuth access token for each new user. To get OAuth tokens, websites and applications must be registered on [Yandex.Oauth]{% if lang == "en" %}(https://oauth.yandex.com){% endif %} in the [Create new client]{% if lang == "en" %}(https://oauth.yandex.com/client/my){% endif %} section.

To learn more about this process, go to [Registering an application](../../oauth/tasks/register-client.md) in the documentation for Yandex.OAuth.

## Obtaining OAuth tokens {#oauth-receive}

To get an OAuth token, follow the [instructions for web applications](../../oauth/reference/web-client.md). You can display the link as a button with the Yandex logo (see [Sample buttons](../reference/buttons.md)).

The received token must be specified in every call to the Yandex ID API, either in the `Authorization` header or in the value of the `oauth_token` HTTP parameter.

You should request an OAuth token for every new user of your website or application who logs in via Yandex.

## Overview of the OAuth protocol {#oauth-general}

The Yandex implementation of the OAuth protocol is described in the [API documentation](../../oauth/concepts/about.md).

To work with the protocol, you can use any of the available [libraries for various programming languages](http://oauth.net/code/).

