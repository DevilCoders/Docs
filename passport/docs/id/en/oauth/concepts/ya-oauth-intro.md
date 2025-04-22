# OAuth implementation at Yandex

Yandex services use tokens to authorize applications. Each token is a digit-letter sequence in which the following information is encrypted:

- ID of the account that can be accessed.
    
- ID of the application with access rights.
    
- Set of rights (actions available to the application).
    

The general rules for using Yandex OAuth tokens are described below.


## Authorization procedure {#authorization-scheme}

Applications request tokens the following way:
![](../_images/authorization.png)

1. The application directs the user to the OAuth server. On the page that opens, the OAuth server can allow the application to access the requested account data. The app can request:
    
    - All access rights specified when registering the app. In this case, the user can only allow or deny all requested accesses at once.
    - Only the access rights currently needed from the list defined when the application was registered. In this case, the user can also allow or deny only all requested accesses at once.
    - The access rights that are currently needed from the list defined when the application was registered, and optional rights from the same list that aren't required. For example, portrait access can be optional. In this case, the user can allow all requested necessary accesses at once and choose which of the requested optional accesses to allow.
    
1. The user allows access to their data, and the OAuth server redirects it to the address chosen by the developer.
    
    The issued token (or the code to get it) is included in the redirect URL. If the user denied access or an error occurred, the URL includes the error description.
    {% if audience == "internal" %}
    {% note info %}
    
    You can also receive a token using a [session cookie](../reference/internal-tokens/sessionid.md), [username and password](../reference/internal-tokens/login-password.md), as well as the [X token](../reference/internal-tokens/xtoken.md). If possible, try to avoid obtaining an OAuth token with a username and password because this data must be requested from the user.
    
    {% endnote %}
    
    {% endif %}
1. The application includes the token received in the request to the Yandex service that supports OAuth.
    

The received token can be saved in the app and used for requests until its lifetime expires.


## Token lifetime {#ttl}

The token lifetime is the period during which the token can be used for authorization. The maximum lifetime depends on the rights selected when [registering the application](../tasks/register-client.md#scope):

Eternal token

:    Never expires and can be revoked only by the user.

     When registering the app, the "infinite" lifetime is displayed.

Renewable token

:    Expires after a few months, but is renewed every time you log in with this token.

     When registering the app, the minimum lifetime is displayed, for example, “at least 1 year”.

Restricted token

:    Expires after the time set for the corresponding access rights.

     If several such rights were selected when registering the app, the token is set to the lowest lifetime limit. Let's say access rights to Yandex.Metrica are issued for 1 year, and the rights to use Yandex.Mail office are issued for 180 days. This means that the access token for both Yandex.Metrica and Yandex.Post Office will be valid for up to 180 days.


## Revoking the token {#token-recall}

The user can revoke any OAuth tokens issued for their account:

- To revoke tokens issued for an account, the user needs to change the password or [log out on all computers]{% if lang == "en" %}(https://yandex.com/support/passport/faq.html#faq__glogout){% endif %}.
- To revoke tokens issued for a specific application, the user can deny access to it on the [Access control]{% if lang == "en" %}(https://passport.yandex.com/profile/access){% endif %} page.

The app can revoke its own token if it was issued [for a specific device](device-token.md).

All cases of revocation are listed on the [Token revocation](../reference/token-invalidate.md) page.


## User interface {#interface}

Page where the user can allow access to the application ([first step](#step-1) authorization), contains the application name and a list of requested rights:

![](../_images/accept.png)

When the user clicks one of the buttons, the OAuth server redirects them to the address specified as the [Callback URI](../tasks/register-client.md#web).

