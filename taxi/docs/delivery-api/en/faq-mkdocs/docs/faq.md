# FAQ

## General questions {#general}

1. **At what status does cancellation become paid?**

   Paid cancellation starts with `SORTING_CENTER_AT_START` status.

1. **At what point can I cancel my order?**

   You can cancel your order at any time before the parcels have been handed over to the recipient. To do this, use the method [Cancel claim](https://yandex.com/dev/logistics/delivery-api/doc/about/intro.html).

1. **What is platform_station_id?**

   `platform_station_id` is your depot's unique ID in the Yandex Delivery system. This ID can be used for your depot, for pickup points, and for dropoff points.

1. **How do I deliver an order to a pickup point?**

   To create a delivery order to a pickup point, create a claim using the regular [Create order](https://yandex.com/dev/logistics/delivery-api/doc/ref/part3/api_b2b_platform_offers_create_post.html) method. As `destination.platform_station`, transmit `platform_station_id` for the pickup point, which you can obtain by the method [getting a list of pickup and dropoff points]( https://yandex.com/dev/logistics/delivery-api/doc/ref/part2/api_b2b_platform_pickup-points_list_post.html).

   To get a list of pickup and dropoff points, find out the `geo_id` using the [getting the geo_id](https://yandex.com/dev/logistics/delivery-api/doc/ref/part2/api_b2b_platform_location_detect_post.html) method.

5. **What is geo_id?**

   `geo_id` is the unique ID of a locality.

   Large cities can include multiple values of `geo_id` depending on the address transmitted.

6. **What are `places` and `items`?**

   `items` are the items packed into `places` (boxes to be loaded into the vehicle at shipment).

1. **Do you support the "Chestny ZNAK" label?**

   Yes, we support the "Chestny ZNAK" label version 1.2. For this, in the `marking_code` field, transmit the GTIN (14 characters) and the serial number (13 characters). We also support transfer of the encrypted tail.

1. **Can I print my own label? What are your requirements for labels?**

   You can attach labels that you have printed yourself on packages. Make sure your label meets the following requirements:

   * The label must contain a unique barcode for each cargo place or barcode in the order.

   * The label must also contain:

     * Order number.

     * Name of online store.

     * Recipient's address.

     * Date and time of delivery.

     * Recipient's contact details.

   * The label must be easily scannable and of adequate size.

   * The label must be clearly visible and readable and must not be placed on the box edges.

   * When the box is deformed during the opening process, the label must maintain integrity.

   For your convenience, here's an example of a well-formatted [label]( https://yastatic.net/s3/doc-binary/src/dev/logistics/en/delivery-api/files/bar-codes.jpg).

1. **How do I find out delivery windows to another city?**

    To find out delivery windows, use the method [get delivery windows depending on the transmitted address](https://yandex.com/dev/logistics/delivery-api/doc/ref/part1/api_b2b_platform_offers_info_get.html).

1. **What is the minimum available pickup time after placing an order?**

    If you are planning a pickup for today and you plan to ship a new order, create such an order before the pickup time

1. **What is `operator_request_id`?**

   `operator_request_id` is the idempotence key, which is set on the client side and has a unique value for each confirmed order.

   Thus, for the new order claim to be created successfully, after confirming the order with one `operator_request_id`, you need to use a different key when creating the new order.

1. **In what format do I transmit the address? What are your address requirements?**

   Example of a valid address: 123 Main Street, Schenectady, NY, USA

   When transmitting addresses, please also keep in mind the following requirements:

   * Don't forget about commas.

   * Separate different parts of the same address with commas.

   * We don't use postal codes in addresses to avoid errors.

   * Do not specify the apartment number. Specify the apartment number in the field `destination.custom_location.details.room`.

1. **Is transmitting coordinates required when creating an order?**

    When creating an order, you can choose one of these parameters to transmit: address, coordinates, or `platform_station_id`.

1. **What do I do if my recipient is unsure which payment method they will use upon receipt?**

    When creating the claim, use `card` as the payment method. That way, if your recipient doesn't have a bank card on them or the transaction fails, they will still be able to pay for the package in cash.

1. **How do I enable pay-on-receipt? How does the insured value work and how do I enable it?**

    To enable pay-on-receipt for the order, fill out the `billing_info` field when [creating the order](https://yandex.com/dev/logistics/delivery-api/doc/ref/part3/api_b2b_platform_offers_create_post.html).

1. **What units do I transmit dimensions and costs in?**

    Volume is transmitted in cm³, dimensions — in cm, weight — in grams, and cost — in kopecks.

    The field `unit_price` (cost) is filled out per item.

1. **What format do I transmit a phone number in?**

    Phone numbers must be transmitted without a plus sign in the following format: `79123456789`.

1. **Do you have a test system? How do I run testing?**

    For your test requests, use the following host: [https://b2b.taxi.tst.yandex.net/](https://b2b.taxi.tst.yandex.net/).

    Sample request for the test host: [https://b2b.taxi.tst.yandex.net/api/b2b/platform/offers/create](https://b2b.taxi.tst.yandex.net/api/b2b/platform/offers/create).

    To make a request against our API, you need a token. Specify the token in the `Authorization` field with the `Bearer` prefix.

    Here's the test token for requests to the test host: `AgAAAADzeAQMAAAPeISvM_9LUkxCijQoFXOH5QE`.

    `platform_station_id` is the ID of your depot in our system (point A). For test requests, we have also created a test depot for you. Use this one: `7c4054cd-d768-4062-8f8d-d0c9b3c8c4e8`.

1. **How much time do I have to confirm my claim?**

    You have 10 minutes to [confirm the claim](https://yandex.com/dev/logistics/delivery-api/doc/ref/part3/api_b2b_platform_offers_confirm_post.html).

    If your service involves placing an order for a longer time, do not create a claim before receiving confirmation from the client. To return the available delivery windows to your client, use the method [get delivery windows](https://yandex.com/dev/logistics/delivery-api/doc/ref/part1/api_b2b_platform_offers_info_get.html). To pre-calculate the cost of delivery, you can use the method of [preliminary calculation of the delivery cost](https://yandex.com/dev/logistics/delivery-api/doc/ref/part1/api_b2b_platform_pricing-calculator_post.html).

1. **How do I get my own station?**

    Your personal manager will help you create your own station.

1. **How do I set up shipping from my station?**

    To set up shipping from your station, please contact your personal manager who will help you define the pickup schedule for your depot.

1. **Can I drop off orders at the sorting center myself?**

    This option is not supported. To get dropoff points, use the method [getting pickup and dropoff points](https://yandex.com/dev/logistics/delivery-api/doc/ref/part2/api_b2b_platform_pickup-points_list_post.html).

    You can deliver your order to the sorting center before 21:00.

    If you have custom needs for dropping off orders at the sorting center, you can coordinate the terms with your personal manager.

1. **What are the restrictions on the dimensions and weight of shipments?**

   * The order weight must not exceed 30 kg. If necessary, you can discuss special terms with your manager.

   * The sum of all the item's dimensions must not exceed 300 cm. An individual dimension must not exceed 110 cm.

1. **What are the restrictions on the insured value of shipments?**

    The maximum insured value of an item is 250,000 rubles.

1. **What time zone are you transmitting the time in? In which time zone should the time be transmitted when creating an order?**

    Time must be transmitted as GMT+0 in UNIX or UTC format. The response will also use GMT+0 time.

1. **What is a barcode and why do I need it? What are your requirements for barcodes?**

    A barcode is the unique ID of an item in your order. A barcode can include the following characters: lowercase and uppercase Latin letters from a to z, the characters `-`, `/`, `\`, `_`, and digits from 0 to 9. You can have several items with the same barcode in one order.

1. **What are your requirements for the phone number format?**

    The phone number must be specified without special characters, in the local format. Example: `7910123456`.

1. **What is an Acceptance Certificate? What do I need it for?**

    The Acceptance Certificate is a document confirming delivery of your items. To generate this document, use the method [getting an Acceptance Certificate](https://yandex.com/dev/logistics/delivery-api/doc/ref/part4/api_b2b_platform_request_get-handover-act_get.html). Moreover, for the orders you are going to ship, you can print out Acceptance Certificates yourself using your company's regular templates.

## Questions related to API method errors {#api}

1. **Not authorized request**

    You might see this error when you transmit an invalid token in the `Authorization` header.

    How can I tell if my token is invalid?

   - You need to update your token after you change your password in your Yandex Delivery account.

   - Make sure that you use the test token to make requests to the test host and use the production token to access the production host.

   - Make sure that the `Authorization` header contains a valid value in the format `Bearer YOUR_TOKEN`.

1. **Delivery window in the past**

    Check that the delivery window is in the future.

1. **Delivery window is too narrow**

    You might see this error if the delivery region doesn't support the window you are transmitting in the request. For example, some regions only support delivery from 9:00 to 18:00. That means that when you create an order with a window from 9:00 to 13:00, you'll see the `Delivery window is too narrow`error.

1. **Cannot deliver**

    if our system couldn't set a route to the recipient or the pickup point based on the specified parameters, you'll see the `Cannot deliver` error.

    To fix this error, make sure that:

   - You have transmitted a valid to-the-door delivery window using the method [create a claim](https://yandex.com/dev/logistics/delivery-api/doc/ref/part3/api_b2b_platform_offers_create_post.html).

   - For delivery to a pickup point or parcel locker, you specified time windows in the following format:

   ```json
    {
       "from": "2022-06-16",
       "to": "2022-06-16"
    }
   ```

    If the error persists, contact [support](https://yandex.com/dev/logistics/delivery-api/troubleshooting/troubleshooting.md).

1. **Dimensions should not exceed**

    The dimensions in your claim exceed the allowable ones. Please cross-check with our restrictions:

   - The weight of the order at delivery to the door or to a pickup point must not exceed 30 kg. If necessary, you can discuss special terms with your manager.

   - The sum of lengths of all the item's dimensions when delivered to the door or to the pickup point must not exceed 300 cm. An individual dimension must not exceed 110 cm.

   - When delivering to a parcel locker, the dimensions restrictions are 40×38×40 cm. The sum total of all dimensions must not exceed 118 cm.

1. **inconsistency billing details**

    This message may arise because of an error in estimating the cost of items on the Yandex side. To fix this error, check the units you use for item costs

1. **Incorrect station platform ID**

    Here is a list of reasons for this error:

   - The station that you transmitted in the request doesn't match the environment where the request is being created. For example, you transmitted a production station in your test request or a test station in your production request.

   - The station transmitted in the request is not assigned to the user running the request, or the station doesn't exist in the system.

1. **Incorrect JSON content. Please check the formatting**

    This is a technical error in parsing the request body. Check that the data is in valid JSON format.

1. **There is place with no items and There are items with no place**

    You might get such an error if you create an order with an empty cargo place or an item without a cargo place assigned. Each cargo place must have at least one item and each item must have a single cargo place assigned.

1. **Cannot parse ... info**

    This is a technical error in parsing the request body. Check that the data is in valid JSON format.

1. **There already was request with such code within this employer**

    `operator_request_id` — This is a unique parameter for each order. If you try to re-create an order with the same `operator_request_id`, you'll see the error `There already was request with such code within this employer`.

