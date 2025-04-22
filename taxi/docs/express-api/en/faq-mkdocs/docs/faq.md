# FAQ

## Using the claim {#claim}

### General questions {#claim-general}

#### 1. Why are some requests made to v2 and some to v1? {#claim-general-v}

For some operations, there are two versions of the API: `v1` and `v2`. `v2` is more up-to-date. That's why if a method has a counterpart in `v2`, we recommend that you use `v2`.

The outdated fields and deprecated methods are marked as `[DEPRECATED]`.

### Create claim {#claim-create}

#### 2. What is request_id? Why can the method return information about a previously created claim? {#claim-create-request_id}

The `request_id` parameter is a unique claim ID, a so-called idempotency token: its value helps to distinguish one claim from others.

Each newly created claim must have its own `request_id` different from the previous ones. If you use an old `request_id`, the method will return the data about an old order regardless of the request body. You may use a previous `request_id` only if you want to retry creating a claim rejected with `5xx` server errors.

`request_id` may include alphanumeric and other characters. To ensure that the values are unique, we recommend that you use `UUID` and its derivative formats.

#### 3. How do you choose the service class and vehicle type? {#claim-create-client_requirements}

If you passed the weight and dimensions of the cargo in the request, the system will automatically select a relevant vehicle.

You can also select the service class and options yourself. To do this, pass the relevant values in the `client_requirements` parameter:

* **Service class** (`taxi_class`):
  * "Courier": `courier`
  * "Express": `express`
  * "Cargo": `cargo` For the `cargo` class, you must also specify the **Cargo type** (`cargo_type`):
     * "Small van": `van`
     * "Medium van": `lcv_m`
     * "Large van": `lcv_l`
* **Number of loaders** (`cargo_loaders`): 1 or 2 (the `integer` type)
* **Additional options** (`cargo_options`):
  * "Thermobag": `thermobag`
  * "Only courier with a car": `auto_courier`

If the system detects that the items to be delivered do not meet the criteria of the selected vehicle (for example, the cargo is too large or the load capacity is exceeded), besides the status `ready_for_approval`, the response will include a warning with the code `not_fit_in_car`.

**Parcel weight:**

* "Courier" (`courier`): up to 10 kg
* "Express" (`express`): up to 20 kg
* "Cargo" (`cargo`):
  * "Small van": up to 300 kg
  * "Medium van": up to 700 kg
  * "Large van": up to 1400 kg

**Parcel dimensions (LxWxH):**

* "Courier" (`courier`): up to 0.80 m × 0.50 m × 0.50 m
* "Express" (`express`): up to 1.00 m × 0.60 m × 0.50 m
* "Cargo" (`cargo`):
  * "Small van": up to 1.70 m × 0.96 m × 0.90 m
  * "Medium van": up to 2.60 m × 1.30 m × 1.50 m
  * "Large van": up to 3.80 m × 1.80 m × 1.80 m

#### 4. How do I make a deferred order for a specific time? {#claim-create-due}

By default, when you create a claim, the courier is called ASAP (the `due` field is not passed). If you need to create a deferred order, use the `due` field to pass the desired date and time of courier arrival at point A (to pick up the parcel).

#### 5. Is it mandatory to pass the item's price and its currency? {#claim-create-cost}

The item's price fields `items[].cost_value` and currency fields `items[].cost_currency` are required, and you can't create a claim without filling them out. If you don't know the price, you can pass `"cost_value": "0"`, `"cost_currency": "RUB"`.

#### 6. Is it mandatory to pass the dimensions and weight of the item? {#claim-create-size}

If you use vehicle auto-detection (the `taxi_class` field is not set), you must pass the dimensions and weight of the item.

If the `taxi_class` field is entered, you may omit the item's dimensions and weight. However, we recommend that you set the dimensions and weight of the item in this case, accounting for the restrictions in the fields `items[].size` and `items[].weight` to avoid errors in selecting the means of transportation.

Dimensions are specified in meters and weight in kilograms.

#### 7. What format do I use to pass a phone number? {#claim-create-phone}

Phone numbers are passed in the format "+7XXXXXXXXXX".

#### 8. Is it mandatory to pass coordinates? {#claim-create-coordinates}

This field is mandatory. You need to pass correct coordinates, since the route point is created based on the coordinates. Be sure to pass coordinates (the `route_points[].address.coordinates[]` field) in the order [долгота, широта], otherwise you'll get an error on claim evaluation.

#### 9. How do I specify the sequence of point visits? {#claim-create-visit order}

The field `route_points[].visit_order` sets the sequential number of a route point. The item's pickup location must be point 1. The next point for item delivery is point 2, and so on. The last point (return point) is added automatically and is identical to the departure point by default, but you can redefine it.

#### 10. How do I pass additional information to the driver? {#claim-create-comment}

We recommend that you pass a text comment to the driver so that they can find the sender and recipient faster. You can pass information for the driver in the general order comment (`comment`) or point-specific comments (`route_points[].address.comment`).

To find the examples of comment texts, see the [documentation](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsCreate.html).

#### 11. How do I specify the code for the courier to quote at the warehouse to pick up the order?{#claim-create-warehouse-code}

You can pass the code using a comment to a point with the type `source` (or `source_point` in v1). The courier will see the comment messages for all the points only after they become your performer.

#### 12. How does the sender know the order to hand over to the courier? How does the driver know specific delivery points for all orders? Where do I specify my internal order number? {#claim-create-order}

Each route point has its own ID `route_points[].point_id`, which is an arbitrary integer. When populating the item's data, the values of the fields `items[].pickup_point` (item's pickup point) and `items[].droppof_point` (item's dropoff point) will be identical to the values `route_points[].point_id` for the pickup points and delivery points on the route.

You can pass the order number in the field `route_points[].external_order_id` of the claim creation method and copy it to the field `items[].extra_id`. In the `items[].extra_id` field, you may specify a different product ID you might have.

{% note warning %}

You can pass the internal order ID only in the block of fields for the array of point B (delivery point).

{% endnote %}

If the `external_order_id` is filled out, when picking up the order, the driver can see the order numbers and quote them to the sender.

You can use the general order comments and point-specific comments to provide any additional information you might need to pass.

#### 13. How do I specify special requirements for my claim? {#claim-create-cargo_options}

In the "Courier" class, you can choose thermal bag delivery and a courier with a car. To do this, pass `courier` in the `client_requirements.taxi_class` parameter and `thermobag` and/or `auto_courier` in the `client_requirements.cargo_options` parameter.

Learn more in the [documentation](https://yandex.com/dev/logistics/api/ref/estimate/IntegrationV1Tariffs.html).

#### 14. What are confirmation codes and how do they work? {#claim-create-confirmation}

A confirmation code is an electronic digital signature of the courier that certifies pickup, delivery, or return of the item.

**Confirmation at point A (store).** When the driver arrives at the point, they set the relevant status in their app (the `ready_for_pickup_confirmation` API status). Then the driver reports that they picked up the parcel. At this point, a code is automatically generated and delivered to the sender via SMS, account profile, or API. The sender must give the code to the driver. The driver enters the code into their app and departs to the recipient.

**Confirmation at point B (at the recipient).** Having arrived at the point, the driver reports arrival in their app (the `ready_for_delivery_confirmation` API status). Then the code is generated and sent to the recipient via SMS. The received code must be given to the courier so they can enter it in their app and close the order.

**Confirmation at the return point (if the product couldn't be handed over and the courier needs to return it)**. After the driver reports that they arrived at the point (the `ready_for_return_confirmation` API status), a code is generated and sent to the client via SMS, account profile, or API. The received code must be given to the courier so they can enter it in their app. When the driver enters the code, they can cancel the order as successfully returned.

The need for confirmation at a specific route point is governed by the `route_points[].skip_confirmation` field value. The default value is `false` (confirmation can't be skipped). You can switch this value to `true` to skip confirmation at this point.

### Claim evaluation {#claim-estimate}

#### 15. What is a price offer? {#claim-estimate-offer}

A price offer is the actual cost of a potential order. The offer is created when claim evaluation is completed successfully. Please note that a price offer is valid for about 10 minutes between the `ready_for_approval` and `accepted` statuses.

If the claim is not confirmed within 10 minutes, you need to resubmit your claim for evaluation. You can do it by using the [Edit claim](https://yandex.ru/dev/logistics/api/ref/claim-edit/IntegrationV2ClaimsEdit.html) method or by creating a new claim with a new `request_id`.

If you try to confirm a claim after the 10-minute offer expires, you'll get an error: the service will respond with code `200`, but the claim will soon switch to `failed`. You can find out the claim status using the methods for getting claim information.

#### 16. What does the claim version mean? {#claim-estimate-version}

A claim can run through multiple versions. A newly created claim has version 1. Each time you change the claim using the edit method, the version number increases by 1: 2, 3, and so on.

### Confirm claim {#claim-approve}

#### 17. How do I confirm the claim I created? {#claim-approve-approve}

To confirm your newly created claim, be sure that the claim passes evaluation successfully. Evaluation is run automatically and takes a few seconds. After that, the claim becomes `ready_for_approval` and you can confirm it. You can edit the claim status using the methods [Order change journal](https://yandex.com/dev/logistics/api/ref/claim-info/IntegrationV2ClaimsJournal.html) and [Get claim information](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html).

Be sure to confirm the claim within 10 minutes after it becomes `ready_for_approval`. To confirm the claim, use the [Confirm claim](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsAccept.html) method. Searching for a performer starts only after the claim is confirmed.

### Claim tracking {#claim-info}

#### 18. How will I get notified when my order status changes? {#claim-info-status}

You can get information about the current order status by using the methods [Get claim information](https://yandex.com/dev/logistics/api/ref/claim-info/IntegrationV2ClaimsBulkInfo.html) and [Journal of changes to the order](https://yandex.com/dev/logistics/api/ref/claim-info/IntegrationV2ClaimsJournal.html).

#### 19. How long does it take to find a courier? {#claim-info-courier}

It takes no more than 30 minutes to find a courier for an ASAP order.

#### 20. How do I get information about the driver? {#claim-info-driver}

You can get information about the driver in the `performer_info` section returned by the methods [Get claim information](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) and [Get information on multiple claims](https://yandex.com/dev/logistics/api/ref/claim-info/IntegrationV2ClaimsBulkInfo.html).

To get the driver's phone number, you can use the method [Get phone number to call the driver](https://yandex.com/dev/logistics/api/ref/performer-info/IntegrationV1DriverVoiceForwarding.html). To ensure personal data protection, the system uses redirect numbers. The number is valid throughout the claim lifecycle, that is, until the claim gets a final status.

### Cancel claim {#claim-cancel}

#### 21. How do I cancel my claim? {#claim-cancel-cancel}

To cancel a claim:

1. Use the method [Get claim information](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) (`available_cancel_state` field) to get the cancelation flag: paid or free.

1. Cancel the claim using the method [Cancel claim](https://yandex.com/dev/logistics/api/ref/cancel-and-skip-points/IntegrationV2ClaimsCancel.html). The claim switches to the `cancelled` status if the order was canceled before the driver arrived at point A (pickup point), or the `cancelled_with_payment` status if the driver already reported arrival, but didn't pick up the item yet.

