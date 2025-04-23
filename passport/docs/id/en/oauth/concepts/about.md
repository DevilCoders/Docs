# OAuth 2.0 Protocol

The OAuth 2.0 protocol allows applications to work with Yandex services on behalf of the user. Access to each app is explicitly restricted by the rights set at the registration. For the basic principles of OAuth, as well as the protocol features in Yandex, see [OAuth implementation in Yandex](ya-oauth-intro.md).

OAuth authorization is supported by [Yandex.Disk]{% if lang == "en" %}(https://tech.yandex.com/disk/){% endif %}, [Yandex.Webmaster]{% if lang == "en" %}(https://tech.yandex.com/webmaster/){% endif %}, [Yandex.Metrica]{% if lang == "en" %}(https://tech.yandex.com/metrika/){% endif %}, and other services.

## How do I use OAuth?

To start using the protocol, you need to:

1. [Register](../tasks/register-client.md) your app in {{ service }}.
    
1. Receive the token in one of two ways:
    
    - Extract the token from the URL hash (the part of the URL after the # character).
    
      This method is described in the instructions for [mobile](../reference/mobile-client.md), [desktop](../reference/desktop-client.md), and [web apps](../reference/web-client.md).
    
    - Request a token in exchange for a confirmation code. You can use a confirmation code to work with apps that aren't adapted to the URL:
    
      - If it's important to receive the token in the response body and not in the URL, request a [code that can be exchanged for a token](../reference/auto-code-client.md).
      - If it's difficult to access the redirect URL in the app, request the [code output for the user in Yandex.OAuth](../reference/console-client.md).
      - If it's difficult to enter a code on the device, you can [ask the user to enter the code in Yandex.OAuth](../reference/simple-input-client.md).
    
{% if audience == "internal" %}
{% note info "Note" %}

You can use [additional ways](../reference/resource-owner-credentials.md) to get OAuth tokens for Yandex services and apps.

{% endnote %}

{% endif %}
You can test OAuth applications using [debug tokens](../tasks/get-oauth-token.md).

