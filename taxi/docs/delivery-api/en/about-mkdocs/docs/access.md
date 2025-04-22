# API access

## Production access {#prod-access}

All requests to the Yandex &#160;Other-Day Delivery&#160; API are sent to the host `https://b2b-authproxy.taxi.yandex.net`.

Example of a request to the production host: `https://b2b-authproxy.taxi.yandex.net/api/b2b/platform/offers/create`.

{% note info "Attention." %}

Obtained a Bearer token in your [account](https://yango.delivery/account) (the "Profile" section).

The Bearer token's validity period is unlimited. However, if you change the password for the [Corporate Client Dashboard](https://yango.delivery/account/), your Bearer token is invalidated and you need to get it again.

{% endnote %}

Use the Bearer token in all requests. Pass the token in the `Authorization` header:

```html
Authorization: Bearer <OAuth token>
```

## Test access {#test-access}

All requests to the Yandex &#160;Other-Day Delivery&#160; API are sent to the host `https://b2b.taxi.tst.yandex.net`.

Example of a request to the test host: `https://b2b.taxi.tst.yandex.net/api/b2b/platform/offers/create`.

Use the following Bearer token for test requests: `AgAAAADzeAQMAAAPeISvM_9LUkxCijQoFXOH5QE`.

Use the following `platform_station_id` for test requests: `7c4054cd-d768-4062-8f8d-d0c9b3c8c4e8`.

## Getting an OAuth token {#get-oauth-token}

1. Log in to your [Corporate Client Dashboard](https://yango.delivery/account) using your username and password.

1. Click the tab [Company profile](https://yango.delivery/account/settings/).

1. Under **API Token**, click **Get**.

1. On the page [https://oauth.yandex.ru](https://oauth.yandex.com), click **Allow**.

1. You can find your OAuth token in the Corporate Client Dashboard in Yandex&#160;Delivery, on the **Company profile** tab under **API access token**.

1. Create a claim and track the order status via the API under the claim processing procedure.

## Any questions? {#questions}

Answers to frequently asked questions are collected in the [FAQ section](https://yandex.com/dev/logistics/delivery-api/doc/faq/faq.html).

<!--For all questions related to integration, methods, and operation of the Yandex API&#160;Other-Day Delivery&#160;, [contact support](https://yandex.ru/dev/logistics/delivery-api/doc/troubleshooting/troubleshooting.html). -->

