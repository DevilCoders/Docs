# Azure AD OAuth application

This application (registered in Azure as `sib-pre-oauthorize-app`) provides ability to obtain robot's OAuth refresh/access/openid tokens (and place them in yav vault) in exchange for **interactive** browser-driven authentication on behalf of approved robot (the robot must be assigned to application in Azure portal).
This application is currently configured to obtain tokens only for APIs necessary to access files in microsoft's cloud (sharepoint/onedrive).
Obtained (and stored in yav) refresh token may be used in any scripts. And must be regularly renewed (or it will expire in 90 days (default lifetime)). (you may check example: `sample-download-office365-file.py`)

## Why?

**scenario**: Somebody needs to run script authenticating to the Azure API (e.g. graph API, sharepoint API, Teams API, ...).
**requirements**: Authenticate against microsoft services using proper authentication methods: MSAL authentication. MSAL concept: everything is OAuth application.
**conditions**:
* yandex user/robot authentication flow is: Azure -> on-premise ADFS -> passport.yandex-team.ru. - The flow is **interactive only** => it is not quite sufficient for scripting tasks.
    * **workaround**: perform full interactive authentication flow and acquire refresh tokens (lifetime = 90 days). Scripts may non-interactively use refresh token and regularly renew the refresh token.
* we do not want to allow uncontrollable registration of new Azure applications, ruled by random people, used by random people/robots, impesonating random privileges, with unmanaged credentials (aka cloud-only robots).
    * **privileges delegation**: Microsoft doesn't provide proper privilege delegation model for 'application' identities (aka cloud-only robots) in its cloud applications (e.g. sharepoint).
        ex.: you may not delegate application access to a single file in some sharepoint's site.
* (does any other authentication flow exist?)

## deployment

* macros:           _SIB_AAD_OAUTH_APP_NETS_
* robot:            robot-authorize-app
* AAD app:          sib-pre-oauthorize-app
* arcadia:          https://a.yandex-team.ru/arc_vcs/security/aad-pre-oauthorize
* hostname:         https://aad-pre-oauthorize.sec.yandex-team.ru/
* oauth redirect:   https://aad-pre-oauthorize.sec.yandex-team.ru/getToken
* deploy:           aad-pre-oauthorize-app
    * secrets: `aad-pre-oauthorize-app` - `sec-01g1jmvx8x1e07nz76d160af9m`
    * env:
        * `REDIRECT_URI` (`https://aad-pre-oauthorize.sec.yandex-team.ru/getToken`)
        * `MY_ROBOT` (`robot-authorize-app`) - robot used by this application
        * `MY_ROBOT_UID` (`112............`) - robot's uid
        * `MY_ROOT_YAV_TOKEN` - robot's passport oauth token
        * `FLASK_SECRET_KEY` - something random

