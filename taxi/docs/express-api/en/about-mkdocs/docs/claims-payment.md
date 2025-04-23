# Payment upon receipt

When receiving the cargo, the user receives a payment link via [Yandex&#160;Checkout](https://kassa.yandex.ru/).

Payment upon receipt works in one of two modes:

- Without fiscalization.
- With fiscalization via Yandex&#160;Checkout.

Learn more about creating claims with payment upon receipt in the operation [Creating claims with multiple route points](../ref/basic/IntegrationV2ClaimsCreate-docpage) and in the [Yandex&#160;Checkout API](https://kassa.yandex.ru/developers/api#intro).

The mode of operation is determined by the type of Yandex&#160;Checkout connected and affects the fields required in requests.

## Authorization {#auth}

To perform operations, you must grant rights to the OAuth logistics application for this purpose:

1. Log in to your Yandex Delivery Corporate Client Account with the username and password you were issued.
2. On the **Profile** tab, click **Yandex&#160;Checkout Connect**. This button is only available if the manager has enabled this feature.
3. On the page that opens, select the desired account and give permissions.

Current Yandex&#160;Checkout connection status and fiscalization status are shown on the **Profile** tab.

