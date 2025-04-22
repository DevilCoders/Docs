# Introduction

The Yandex Other-Day Delivery API provides an option to place an order for another day using HTTP requests: use delivery with classic pickup from your depot and delivery to the end recipient. In addition, you can drop off items at certain dropoff points or deliver to pickup points.

![Diagram](https://yastatic.net/s3/doc-binary/src/dev/logistics/en/delivery-api/files/scheme-0.png)

Before getting started with the API, get a Bearer token in your [account](https://yango.delivery/account) (the "Profile" section) or use the test token  `AgAAAADzeAQMAAAPeISvM_9LUkxCijQoFXOH5QE` and the test host [https://b2b.taxi.tst.yandex.net/api/b2b/platform/offers/create](https://b2b.taxi.tst.yandex.net/api/b2b/platform/offers/create).

When running requests against the production environment, use the host [https://b2b-authproxy.taxi.yandex.net](https://b2b-authproxy.taxi.yandex.net) and the production station `platform_station_id`.

Create a claim and track the order status using the API, as per the [status model](status-model.md).

<!--If you have any issues, please contact your Yandex Delivery manager or [support](https://yandex.ru/dev/logistics/delivery-api/doc/troubleshooting/troubleshooting.html). -->

## Integration materials {#integration}

If you use third-party software to integrate with Yandex Delivery services, please review our [integration examples](https://yastatic.net/s3/doc-binary/src/dev/logistics/en/delivery-api/files/YandexDeliveryNDDAPI_postman_collection_en.zip) run in Postman. You can download the file and use it to debug and edit queries.

Сlick on the collection to add your Bearer token (a token with the prefix `Bearer`). After that, you can test all the added queries and, if necessary, generate ready-to-use code in the most popular programming languages.

<a class="doc-c doc-c-button doc-c-button_theme_action doc-c-button_size_m doc-c-button_js_inited doc-c-link doc-c-link_type_external doc-c-i-bem doc-c-link_js_inited" href="https://yastatic.net/s3/doc-binary/src/dev/logistics/en/delivery-api/files/NDD_EN.pdf" target="_blank"><span class="doc-c-button__text">Guide for "Other-Day Delivery"</span></a>

<a class="doc-c doc-c-button doc-c-button_theme_action doc-c-button_size_m doc-c-button_js_inited doc-c-link doc-c-link_type_external doc-c-i-bem doc-c-link_js_inited" href="https://yastatic.net/s3/doc-binary/src/dev/logistics/en/delivery-api/files/YandexDeliveryNDDAPI_postman_collection_en.zip" target="_blank"><span class="doc-c-button__text">Ready-made examples of Postman integration</span></a>

