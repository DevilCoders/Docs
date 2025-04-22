# Order properties

Orders in Yandex.Routing are locations that should be visited by one or more vehicles in the optimal sequence, subject to restrictions.

To define orders, use the `orders` request field.

## Order ID

An order's number (ID) is a required attribute that is set in the <code>id</code> field.

You can use any unique number of an order from your accounting system.

In addition to the order ID, you can specify other order attributes from your accounting system:

- Recipient name in the <code>title</code> field.
- Description of the delivery destination (for example, address) in the <code>description</code> field.

{% note %}

Note that such fields as <code>title</code> and <code>description</code> are used for informational purposes rather than for route optimization.

{% endnote %}

## Order coordinates

You can specify the order delivery destination in [WGS84](https://wikipedia.org/wiki/WGS_84). The coordinates must correspond to the parking or stop location for order delivery. If your system specifies the delivery location using the address, you should perform [geocoding](https://tech.yandex.com/maps/geocoder/) (converting an address given in free format into geographical coordinates).

{% note %}

Note that coordinates like `0.0` won't be processed correctly and will result in an error when sending requests to the Router.

{% endnote %}

To determine the coordinates of an order, use the `location.point` field.

## Order delivery window

All orders must have a delivery window specified, that is a time interval when a vehicle or courier should arrive at the delivery address.

To set a window, use the `time_window` field.

A time window is set in [one of the following formats](properties-of-time-window.md#otnositelnyi-format-vremennykh-okon):

- `07:00:00 - 23:00:00`: A window that starts at 7:00 and ends at 23:00 of the current day.
- `2019-10-10T07:00:00+03:00/2018-10-10T23:00:00+03:00`: A window that is set for a specific date and time zone.

Depending on the window type, a courier is to deliver an order strictly within the specified interval (a **soft** window) or may violate the window with an additional penalty imposed (a **soft** window). For details, see [Hard and soft time windows](properties-of-time-window.md#zhestkie-i-miagkie-okna)

To manage hard time windows, use the `hard_window` field:

- `True`: A hard window.
- `False`: A soft window.

If you use a **soft** time window, you can additionally set penalties for violating the window:

- `penalty.out_of_time.fixed`: A fixed penalty for one-time late or early arrival.
- `penalty.out_of_time.minute`: A penalty per minute of late or early arrival.

When an order is to be delivered by a specific time, we don't recommend that you specify a window with the same upper and lower boundaries, especially if the window type is hard.

For example, if the order delivery time is strictly by 9:00, the Router will process the value `9:00:00 - 9:00:00` correctly, but in practice, the vehicle will arrive at such a location in advance. Therefore, we recommend that you specify a window in a more realistic range (for example, `8:30:00 – 9:00:00`). The narrower the order delivery windows, the more vehicles are required to complete those orders within the set timeframes. Therefore, a window should, as accurately as possible, reflect the real possibility of arriving at a given destination.

{% note %}

Please note that the service duration isn't taken into account when determining the fact of falling within a time window. For example, if a window is set as `10:00 - 16:00` and the service duration is 30 minutes, the arrival at the order location at `15:59` is considered timely.

{% endnote %}

## Order weight

For each order to be delivered, you can set its weight. This isn't mandatory, but is recommended to avoid overloading vehicles.

To set the weight of an order, use the `shipment_size` field. Just specify one of the attributes:

- `shipment_size.weight_kg`: Weight in kilograms or volume weight.
- `shipment_size.volume`: Dimensional weight. Set as the product of dimensions: length, width, and height. If the dimensions are unknown, you can set the volume value in a certain field and set other fields to 1.
- `shipment_size.units`: The number of units (pallets, boxes, or kegs) .

For more information about weight determination, see [Weight and volume](properties-of-weight.md).

When setting the order weight, you should specify the vehicle load capacity.

In a request, you should set the gross weight and volume of an order, especially when data about the tare weight may have a significant impact on routing results. If the gross weight is not explicitly known at the route planning stage, we recommend that you calculate it based on the specifics of goods to be transported. For example, if the average weight of a loaded pallet is 800 kg, the weight of the pallet itself is 20 kg, the weight specified in the order is 500 kg, and, at the time of planning, it's unknown how the cargo will be assembled at a depot, then, when setting a routing task, you can specify the weight in the order as follows: `500 kg + 20 kg * (500/800)`= `512.5 kg`. The number of cargo units is set as the ratio of the expected gross weight to the average weight of the pallet `512.5/800`, that is, 0.64 pallets. This is only one of the possible ways to make an approximate calculation.

{% note %}

If the weight, volume, or number of units per order exceeds the maximum capacity of a vehicle, this order falls into undistributed ones at the route planning stage: the Router treats an order as an indivisible unit. If there're large orders in the accounting system, we recommend that you divide them at the stage of uploading to the Router.

{% endnote %}

## Order delivery service duration

When planning routes, you can specify each order's service duration.

Two types of service duration are supported:

- `service_duration_s`: Time for order delivery to the recipient.
- `shared_service_duration_s`: Time for exchanging documents or parking.

{% note %}

Please note that if multiple orders are delivered to the address at the same time, the parking time is only counted once for the first order. For more information, see [Multi-orders](properties-of-orders.md).

{% endnote %}

### Example

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/e52ab293-f58d360b-4e8a3210-50685d37) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/e52ab293-f58d360b-4e8a3210-50685d37) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#e52ab293-f58d360b-4e8a3210-50685d37)

## Service duration for loading an order at a depot

In addition to the total depot service duration, the Router enables you to specify the duration of loading an individual order into a vehicle at the depot.
To set the order loading duration, use the `location.depot_duration_s` request field.

If the total service duration is set for the depot, it's added to the total duration of order loading into each vehicle. For more information, see [Depot service duration](properties-of-depot.md).

### Example 1

The example defines the service duration at the depot for each order.

{% note %}

Please note that the arrival time at the first order location corresponds to the time spent by the vehicle or courier at the depot + the time it takes to get to the first location.

{% endnote %}

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/eb51f402-656c73c5-cd8a4811-43e17544) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/eb51f402-656c73c5-cd8a4811-43e17544) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#eb51f402-656c73c5-cd8a4811-43e17544)

### Example 2

In this example, the service duration at the depot for each order is 5 minutes and the total depot service duration is 10 minutes: all in all, the vehicle will spend 25 minutes loading.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/3d233d80-68338168-c65bd61f-7d6e5548) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/3d233d80-68338168-c65bd61f-7d6e5548) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#3d233d80-68338168-c65bd61f-7d6e5548)

## Pickup and delivery

In general, orders are loaded to vehicles at the depot and delivered to the recipient addresses.

If an order's pickup at the customer's address and then its delivery to another address (Pickup and Delivery) is required, you should define the order type.

To do this, use the`location.type` field with the following values:

- `pickup`: Picking up an order at a certain address.
- `delivery`: Delivering an order to a certain address (default).

If you set the `pickup` type, the following rules apply:

- If **you set ** the `location.delivery_to` field that contains the `id` of another order, the delivery is made to the address of that order.
- If the field `location.delivery_to` **is empty**, the order is delivered to the depot at the end of the route.

Yandex.Routing also supports mixed pickup and delivery when both regular delivery orders and pickup/delivery orders are included in the request.

{% note %}

Please note that the sequence of placing pickup and delivery orders en route only depends on the vehicle's load capacity and the order delivery windows.

There may be other locations between the order pickup and its delivery to another address, if the vehicle's load capacity allows for that and if this route is more profitable.

Yandex.Routing doesn't support a delivery immediately after pickup with other locations ignored.

{% endnote %}

{% note %}

Please note that if there're multiple orders for a cargo's `pickup` at the same address, in rare cases, the pickup can be performed by more than one vehicle or courier.

This can be justified in terms of reducing the total cost of delivery.

{% endnote %}

## Multi-orders

When planning routes, there may be cases when multiple orders must be delivered to the same address, for example, to the same apartment building or business center.

If orders have overlapping delivery windows and the same delivery address, Yandex.Routing merges such orders so that they are carried out by a single vehicle as one large order or divides them into several multi-orders, depending on what's more profitable.

{% note %}

If you want to be sure that all orders located at the same address are merged into one multi-order, set the option `options.merge_multiorders = true`.

Enabling the multi-order merge option ensures that a multi-order only appears on a single route, provided that the capacity of a vehicle or courier allows that.

{% endnote %}

When merging orders, the time for delivering documents or parking is counted once for a group of orders if they are handled as a multi-order.

For each order, you can set the service duration as two values:

- `location.shared_service_duration_s`: Time for document delivery or parking.
- `location.service_duration_s`: Time for order delivery.

For regular orders that are located at different addresses, the service duration is counted in a route as follows:

<img src="https://courier.yandex.ru/vrs-doc/multiorders-11_en.png" class="text--img" width="620px" />

When merging orders into a multi-order, the service duration for parking is counted only once:

<img src="https://courier.yandex.ru/vrs-doc/multiorders-21_en.png" class="text--img" width="620px" />

### Example

In the example, three orders with different delivery times are set and the option to merge multi-orders is activated.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/7b105ca6-bc024f63-ef6577ea-9e3c03df) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/7b105ca6-bc024f63-ef6577ea-9e3c03df) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#7b105ca6-bc024f63-ef6577ea-9e3c03df)

## Penalties for late arrival at an order location

This penalty is added to the total cost of a route if an order is scheduled for delivery, but the delivery occurs earlier or later than the specified delivery window.

{% note %}

Note that this behavior is only possible if you set a *soft* time window. If a *hard* time window is violated, the order is automatically marked as uncompleted and excluded from all routes.

{% endnote %}

A penalty for untimely delivery makes it more likely that the most important orders are delivered without delay at the expense of the less important ones.

To manage the timeliness of order delivery in the Router, use the `location.penalty.out_of_time` field consisting of two components:

- `location.penalty.out_of_time.fixed`: A fixed penalty for late arrival (one-time), regardless of the length of delay.
- `location.penalty.out_of_time.minute`: A penalty per minute of untimely delivery (counted if the arrival at a location occurs both earlier and later than the set timeframe).

{% note %}

The above fields have default values that should be used as the starting values when you set custom priorities for order delivery.

If in doubt, contact Yandex.Routing analysts to determine the correct coefficients.

{% endnote %}

## Penalties for a failure to complete an order

For each order in a request to the Router, you can set a penalty for a failure to complete the order. If there's a shortage of  vehicles or couriers, individual locations may be excluded from all routes.

For example, if an order is to be delivered at a location that is at a great distance from the others, its delivery will lead to a several-hour delay for the other locations, this order may be excluded from the routes as uncompleted.

{% note %}

In the Router's response, uncompleted orders are placed in a separate field named `dropped_locations`.

{% endnote %}

This penalty is added to the total cost of the route if the order can't be scheduled for any of the set vehicles.

There are many reasons for a failure to include an order in a route, such as:

- The weight of the order exceeds the load capacity of any of the set vehicles.
- The total weight of orders exceeds the total load capacity of vehicles, so it's impossible to deliver the orders even with additional trips. Hence, there're undistributed orders in any case.
- This order isn't compatible with any of the set vehicles or the load capacity of the vehicles that are compatible with a certain set of orders is too small to accommodate all of them.
- It's not possible to deliver the order within the specified hard time window.
- It's impossible to deliver orders due to the strict restrictions on vehicle shifts.
- A narrow hard window for the depot and strict parameters for vehicles' return to the depot are set: as a result, the system plans a vehicle's return to the depot, while not having time to deliver the orders.
- Incorrect coordinates of an order that cause it to be geographically remote from other orders, so the system doesn't find it possible to complete this order.
- Planning a complicated task in low mode.
- And other.

In general, if one order has a penalty of 50 units and another one has a penalty of 5 units, the order with the 50-unit penalty is considered more important and is more likely to be included in planned routes.

To set a missing delivery penalty, use the Router's field named `location.penalty.drop`

{% note %}

Note the size of the default value for this field (1000000). To manage priorities, we recommend using a value of a similar or higher order.

If in doubt, contact Yandex.Routing analysts to determine the correct coefficients.

{% endnote %}

## Order and vehicle compatibility

When setting an order in a request to the Router, you can assign it a list of characteristics of the vehicle that should fulfill this order.

To define order tags (required vehicle characteristics), use a field named `location.required_tags`.

An order is considered compatible with a vehicle if any of the vehicle/order compatibility rules are met. The compatibility rules are defined when setting vehicles.

For more information about the compatibility rules, see [Vehicle tags](properties-of-vehicles.md).

## Incompatibility of orders

If you need to transport orders that can't be in one vehicle at the same time, the Router enables you to identify one or more incompatible order types. There are no predefined order types in the Router.

The following can be used as incompatible types:

- Incompatible cargoes that for objective reasons can't be transported in the same vehicle within the same trip.
- Incompatibility of different recipients with each other. For example: allocation of competitor products across different vehicles or separation by certain types of customers.
- Incompatibility of order geographical zones (for example, when it's necessary to always plan a certain direction/zone separately, regardless of route efficiency).

To set the order type, use a field named location.load_types. If necessary, you can specify multiple types for each order. To define incompatible orders, use the `incompatible_load_types` field. You can set a list of incompatible types in this field: when planning a route, orders are assigned to different vehicles if they have at least one incompatible type.

{% note %}

Order incompatibility is a strict constraint, meaning it can't be violated when using automatic routing. For example, if several incompatible orders are set for the same destination, the algorithm will plan a route assigning them to different vehicles. The use of order incompatibility types may result in nonoptimal routes. Therefore, you should only introduce really significant restrictions, which in practice are mandatory rules.

{% endnote %}

### Example 1

When transporting household chemicals, food, and flowers using the same vehicle fleet, in the `location.load_types` field, specify such cargo types as `chemicals`, `food`, and `flowers` for respective orders.

To ensure that household chemicals are never in the same vehicle with food or flowers, but that flowers and food can be transported together, set the following incompatibility rules:

| type | incompatible_load_types |
| ------------ | ------------------------- |
| chemicals | food, flowers |

In this example, we set 3 orders and assigned one of the 3 types to each of them. As a result, the algorithm planned 2 routes.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/5ae98af-d12eb2ef-e0f00f9f-983a9f8c) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/5ae98af-d12eb2ef-e0f00f9f-983a9f8c) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#5ae98af-d12eb2ef-e0f00f9f-983a9f8c)

### Example 2

In this example, we set 4 orders with cargo incompatibility and, additionally, geographical zone incompatibility specified.

As a result, all orders are incompatible with each other and the algorithm plans 4 routes despite the fact that 2 orders are sent to the same destination.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/e80d90d7-a97d2bb7-cf91abd7-c1059764) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/e80d90d7-a97d2bb7-cf91abd7-c1059764) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#e80d90d7-a97d2bb7-cf91abd7-c1059764)

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>
