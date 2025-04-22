# Revoke a token

Yandex.OAuth revokes tokens in the following cases:

- The token was revoked by the user on the [Third party clients]{% if lang == "en" %}(https://passport.yandex.com/profile/access){% endif %} page. When the OAuth token is revoked, the corresponding refresh token is revoked automatically.
    
- The token expired.
    
- The app owner changed the requested rights or deleted the app. In this case, all tokens ever issued to this app are revoked.
    
- The user performed an action that revokes all OAuth tokens and refresh tokens ever issued for the account:
    
    - Changed password.
    
    - Turned [two-factor authentication]{% if lang == "en" %}(https://help.yandex.com/passport/authorization/twofa.xml){% endif %} on or off.
    
    - Successfully restored access to the account.
    
    - Clicked **Log out of all computers** in [Yandex ID]{% if lang == "en" %}(https://passport.yandex.com/passport?mode=passport){% endif %} or some other service.
    

## Revoking tokens in the app {#revoking-token}

The app can revoke OAuth tokens that were [issued for a specific device](../concepts/device-token.md) with a request to {{ service }}.

To implement logging out of an account for regular tokens, you can delete the corresponding tokens from local storage. A deleted token can't be restored via {{ service }}, the app will have to request access again.

In this case, nothing will change for the user on the [Third party clients]{% if lang == "en" %}(https://passport.yandex.com/profile/access){% endif %} page. A token issued to the application is considered active until it is revoked in any of the ways listed above.

