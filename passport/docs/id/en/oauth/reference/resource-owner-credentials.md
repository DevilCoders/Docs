# Getting tokens inside Yandex

{% note info "Important" %}

The methods listed below are not intended for general use. If you're sure that you need one of them, write to the [oauth@](mailto:oauth@yandex-team.ru) mailing list and tell us about your case.

{% endnote %}

For Yandex services and apps, there are additional ways to get OAuth tokens:

- [In exchange for a session_id cookie](internal-tokens/sessionid.md).
    
- [In exchange for a username and password](internal-tokens/login-password.md).
    
- [In exchange for an OAuth token](internal-tokens/xtoken.md) with the **X-Token issue** right. This method is used only for mobile apps and is implemented via [Account Manager](https://wiki.yandex-team.ru/yandexmobile/accountmanager).
    
    By default, the right to receive X-tokens is hidden for all Yandex.OAuth users. You can request access to it in the [oauth@](mailto:oauth@yandex-team.ru) mailing list. After that, you can select this right on the app settings page.
    
- [Without user authentication](client-credentials.md). This way you can only get a depersonalized token for authorization of internal Yandex server apps.
    

