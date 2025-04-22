# Terminology

OAuth token

:    A string that allows the Yandex service be accessed on behalf of a specific user. In the context of the protocol usage, “OAuth token” can be shortened to “token”.

     Each OAuth token contains:

     - ID of the account that can be accessed.
    
     - ID of the application with access rights.
    
     - Set of rights (actions available to the application).
    

     Thus, the token shows what this application can do on behalf of a particular account.
     {% if audience == "internal" %}
     {% note info %}

     Inside Yandex, applications can request [depersonalized tokens](../reference/client-credentials.md) to access resources that don't belong to any Yandex account or are not accessible in any other way.

    {% endnote %}

    {% endif %}

OAuth app

:    Program, mobile app, or web service [registered](../tasks/register-client.md) in Yandex.OAuth.

     In {{ service }} documentation, OAuth apps are simply called "apps". Applications of other types are explicitly marked.

Rights

:    An action or set of actions on behalf of the user that are available over the OAuth protocol.

     {{ service }} tokens always specify the rights chosen by the developer when registering or configuring the app. For the same OAuth app, you can't get two working tokens with different rights at the same time.

Refresh token

:    An additional string issued with the OAuth token. The refresh token is used to update an OAuth token that is about to expire.

