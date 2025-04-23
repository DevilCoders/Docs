# API access

All requests to the Yandex Delivery API are sent to the host `https://b2b.taxi.yandex.net`.

The OAuth token of the corporate client is used to access the API.

The OAuth token's validity period is unlimited. However, if you change the password for the Corporate Client Dashboard, your OAuth token is invalidated and you need to get it again.

Use the OAuth token in all API requests. Pass the token in the `Authorization` header:

```html
Authorization: Bearer <OAuth token>
```

## Getting an OAuth token {#get-oauth-token}

1. Log in to your [Yandex Delivery Corporate Client Dashboard](https://yango.delivery/account) using your username and password.

1. Click the tab [Company profile](https://yango.delivery/account/settings/).

1. Under **API Token**, click **Get**.

1. On the page [https://oauth.yandex.ru](https://oauth.yandex.com), click **Allow**.

1. You can find your OAuth token in the Corporate Client Dashboard in Yandex Delivery, on the **Company profile** tab under **API access token**.

