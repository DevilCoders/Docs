# Getting started

To start working with Yandex Taxi:

1. Get a token for sending API requests.
    1. Log in to your [Yandex Taxi Corporate Client Dashboard](https://business.taxi.yandex.ru/) with the username and password you were issued.
    1. Click your username in the upper-right corner of the Dashboard. A block with your account information opens.
    1. In the **API Token** block, click **Get**. This redirects you to oauth.yandex.ru.
    1. At oauth.yandex.ru, click **Allow**. You will be redirected to the Yandex Taxi Corporate Client Dashboard.
    1. You can find your OAuth token under **API token** in the account information block.
    
1. API Tokens are valid for a limited time and then expire. Use the [Update OAuth token](oauth-refresh.md) request to get the lifetime of your token.
    
    - If the token lifespan is about to expire, run the [Update OAuth token](oauth-refresh.md) request again. This renews the token expiration date and you can continue using your current token.
    - If the token expires, get a new token in the [Yandex Taxi Corporate Client Dashboard](https://business.taxi.yandex.ru/).
    
    {% note info "Note" %}
    
    If the token is lost, contact [Yandex ID](https://passport.yandex.ru) to reissue it.
    
    {% endnote %}
    
1. Use the OAuth token in all API requests. Pass the token in the header:
    #### In the API version 1.0
    `Authorization: <token value>`
    #### In the API version 2.0
    `Authorization: Bearer <token value>`
    
    {% note info "Note" %}
    
    To work with the API 1.0, use the host `https://business.taxi.yandex.ru`, and to work with the API 2.0, use the host `http://b2b-api.go.yandex.ru`.
    
    {% endnote %}
    
1. For most requests, you have to specify a client ID (`client_id`). To get this value, use the [Client information](auth.md) request.
1. [Enter cost center information](cost-center-create.md).
1. Create [user roles](role-create.md).
1. Add user accounts:
    #### In the API version 1.0
    [Create a user](user-create.md)
    #### In the API version 2.0
    [Create a user](api20/user-create.md)
    

## Ordering a ride {#section_gyz_b4t_5hb}

After you receive the token and add information about your users, you can use the Yandex Taxi API to order rides.

The ordering procedure is as follows:

1. [Learn the price and conditions of your upcoming ride and get an offer](route-stats.md).
1. Create a [draft order](order-create.md).
1. If necessary, [change the order details](order-change.md).
1. Pass the order [for processing](processing.md).
1. If necessary, [cancel the order](order-cancel.md).

