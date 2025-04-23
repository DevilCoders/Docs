# Switching from OpenID to the Yandex ID API

All OpenID identifiers with Yandex as the provider stopped working on August 10, 2015. To log in to other sites with your Yandex account, use the newer and more secure Yandex ID API.

## For users {#user}

Since August 10, 2015, you can log in on other websites using your Yandex account only if the website developer correctly switched over from OpenID. If you can't log in to a website with your Yandex account, contact the site's support service.

## For website developers and webmasters {#webmaster}

Users who log in to your website with a Yandex OpenID lost this capability on August 10. You can use the Yandex ID API to authenticate such users.

The API can also provide users access to old accounts that are associated with an OpenID. To do this, [enable the Yandex ID API](adoption.md) and then use the following method to process the logins:

1. If a user manually enters their Yandex OpenID, notify them that this login option is no longer available and offer to use their Yandex ID API instead. You can recognize Yandex identities by the URL domain: `yandex.ru` or `ya.ru`.
    
    If a user just clicks the button to log in via Yandex, use the Yandex ID API for authentication.
    
1. Request an OAuth token to access the user's data.
    
1. [Request](../reference/request.md) the necessary data via the Yandex ID API. Pass the `with_openid_identity` parameter to get the OpenID data that may belong to the user.
    
1. Search for each OpenID identity listed in the response in your database of accounts:
    
    - If no account with the received OpenID data was found, simply use the Yandex ID API to authenticate the user.
    
    - If you found the account, link it to the account ID in Yandex (the `id` element in the response from the Yandex ID API). Then use the API to authenticate the user.
    
    - If multiple accounts were found with the listed OpenID identities, ask the user to select one to use for authentication. Link the selected account to the account ID in Yandex, then use the Yandex ID API to authenticate the user.
    

This way, the user can log into your site via Yandex, and you can associate the data from the old OpenID account to the unique Yandex user ID when this becomes necessary.

