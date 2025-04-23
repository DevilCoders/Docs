# Vehicle properties

In Yandex.Routing, orders can be delivered by regular vehicles or by couriers traveling on foot or by public transport. Vehicles and couriers have a common set of properties.

To define a vehicle or courier, use the `vehicles` request field.

## Vehicle ID

A vehicle's unique number (ID) is a required attribute that is set in the `id` field. The ID must be unique within a single request to the service.

You can also specify a vehicle's string ID from your accounting system. To do this, use the `ref` field.

## Vehicle or courier capacity

The Router enables you to set a vehicle's capacity to determine the maximum cargo weight or amount that the vehicle/courier can transport per route.

To set the vehicle or courier capacity, use the `capacity` field. Just specify one of the values:

- `capacity.weight_kg`: Weight in kilograms or volume weight.
- `capacity.volume`: Volume. Set as the product of length, width, and height. If the dimensions are unknown, you can set the volume value in a certain field and set other fields to 1.
- `capacity.units`: The number of units (pallets, boxes, or kegs).

For more information about weight determination, see [Weight and volume](properties-of-weight.md).

{% note %}

Please note that if the order weight is set in kilograms or as a volume weight, the vehicle capacity must be set in the same units. Similarly, if the order weight is set as the number of seats, the vehicle capacity must specify the maximum number of seats in each vehicle.

{% endnote %}

Additionally, you can set the maximum load of a vehicle as a percentage of the specified load capacity. To do this, use the `limits` request field:

- `limits.volume_perc`: A percentage of the value specified in `capacity.volume`.
- `limits.weight_perc`: A percentage of the value specified in `capacity.weight_kg`.
- `limits.unit_perc`: A percentage of the value specified in `capacity.units`.

To indicate that overload is allowed relative to a given value, specify a value greater than 100. To reserve some load capacity, for example, for possible inaccuracies in the estimation of order dimensions, specify a value less than 100. For example, a value of 110 allows for a 10% overload and a value of 90 allows for a maximum load of 90% of the specified load capacity.

The vehicle capacity (based on the `limits`) is a strict constraint that won't be violated. Note that, when calculating the vehicle load, the system takes into account orders for pickup and delivery. For more information, see [Pickup and delivery](properties-of-orders.md).

{% note %}

You can use the vehicle capacity to indirectly manage the number of orders that should get into it. For example, if you set the volume per order to 1 unit (regardless of the actual size of the order) and the vehicle capacity to 10 units, then each vehicle will be assigned no more than 10 orders.

{% endnote %}

### Example

There're two vehicles with a load capacity of 1.5 tons (Vehicle 1) and 3 tons (Vehicle 2) and three orders for delivery with a weight of 1 ton, 1.2 tons, and 1.4 tons, respectively.

{% note %}

When optimizing routes, the 1-ton order gets into Vehicle 1 and the 1.2-ton and 1.4-ton orders get into Vehicle 2.

{% endnote %}

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/f8cc2d06-f547a712-4e6779f3-ed4d4358) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/f8cc2d06-f547a712-4e6779f3-ed4d4358) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#f8cc2d06-f547a712-4e6779f3-ed4d4358)

## A vehicle's departure from a location other than a depot

By default, vehicles and couriers start their route from a depot, but sometimes they need to start a route from a different location (such as a building or parking spot). As a rule, this task is suitable for planning the routes of sales representatives, service engineers, and other specialists who provide services rather than deliver goods.

The main way to implement this requirement is to use the `vehicle.visited_locations` property. To do this, in the `locations` field, set a courier's starting point and, in the `visited_locations` field, specify the ID of this point and the start time from it for the courier.

### Example

In the example below, two vehicles start their routes not from depots, but from the locations specified by the `visited_locations` property.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/e923b663-3c8d25cf-ddbb472d-2ccba1de) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/e923b663-3c8d25cf-ddbb472d-2ccba1de) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#e923b663-3c8d25cf-ddbb472d-2ccba1de)

## Return to a depot at the end of the working day

By default, a vehicle or courier starts and finishes a route at a depot.

If the vehicle doesn't need to return to the depot after all the orders are completed, use the `vehicle.return_to_depot = false` option.

### Return to an arbitrary location at the end of a route

If you need to take into account the distance between the last order location and the courier's parking place or, for example, home address, you can do the following:

- Create a point with the `garage` type (the `locations[].type` field). This point will only be used as a route ending point.

- For a courier who needs to return "home" or to the "parking spot" at the end of the working day, specify the ID of this point in the `vehicle.finish_at` field.

When handling the task, all vehicles or couriers that have the `finish_at` property specified will return to the specified point. If the return to depot option is enabled (`vehicle.return_to_depot = true`), a route is set so that a courier or vehicle first visits the depot and then goes to the parking spot.

### Example

The example below uses two vehicles with different load capacities and four orders with different weights. Both vehicles are involved in delivery due to weight restrictions. Vehicle 2 shouldn't return to the depot after the last order is delivered.

{% note %}

Note that in the Router's response, vehicle 2 completes the route at the last order location.

{% endnote %}

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/e9f73cbf-e48a5a6f-51e1658d-44946119) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/e9f73cbf-e48a5a6f-51e1658d-44946119) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#e9f73cbf-e48a5a6f-51e1658d-44946119)

## Multiple vehicle trips per day

By default, a vehicle or courier starts and ends their route at the depot, that is, completes exactly one route during the working day (shift).

If a vehicle may return to the depot at any time of the work shift to take additional orders, use the `vehicle.max_runs` option: the maximum number of trips during the work shift.

### Example

The example below uses one vehicle with a limited capacity of 2 tons and three orders with a weight of 0.8 tons. The vehicle is allowed to make two trips, meaning it may return to the depot after completing two orders to take and deliver one more.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/1b6d35f9-abf3c24b-f3f31e7f-f7c0821e) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/1b6d35f9-abf3c24b-f3f31e7f-f7c0821e) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#1b6d35f9-abf3c24b-f3f31e7f-f7c0821e)

## Vehicle or courier work shifts

You can define one or more work shifts for a vehicle. To set shifts, use the `vehicle.shifts` field.

A shift is a range of time during which a vehicle is allowed to operate. The shift duration includes the loading time at the depot, the time en route, and the order service duration.

You can also limit the maximum shift duration.

Shifts are optional: if they aren't explicitly defined, each vehicle runs exactly one shift within a time window that matches the [depot time window](properties-of-depot.md).

To use one or more shifts, define the following fields in Excel:

- `shifts.0.time_window`: A [time window](properties-of-time-window.md) that corresponds to the vehicle operating hours.
- `shifts.0.hard_window`: An [indicator of a hard time window](properties-of-time-window.md#zhestkie-i-miagkie-okna).
- `shifts.0.service_duration_s`: Time between shifts (in seconds). For example, the time required for replacing the driver, exchanging documents, and so on.
- `shifts.0.penalty.out_of_time.minute`: A shift's [time window](properties-of-time-window.md) violation penalty (per minute).
- `shifts.0.penalty.out_of_time.fixed`: A shift's [time window](properties-of-time-window.md) violation penalty (one-time).

{% note %}

Note that to set multiple shifts, you need multiple fields in Excel with an increasing numeric index.

For example, `shifts.0.time_window` refers to the first shift, while `shifts.1.time_window` refers to the second one.

{% endnote %}

### Example

A request to the Router specifies one vehicle with three shifts (morning, day, and evening ones), and three orders, of which one has the delivery time in the morning and two in the evening.

{% note %}

Please note that the Router's response will only use the morning and evening shifts, since there are no orders for delivery during the day shift.

{% endnote %}

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/5167e27-10164864-7999bac5-1a48e8a1) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/5167e27-10164864-7999bac5-1a48e8a1) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#5167e27-10164864-7999bac5-1a48e8a1)

## Cost of a vehicle or courier

For each vehicle in a request to the Router, you can specify different components of the cost per use. An optional request field named `vehicle.cost` is used to set the cost of a vehicle or courier.

In the Router, you can define the following basic cost components:

- `cost.fixed`: Fixed cost of using the vehicle.
- `cost.hour`: Cost per hour.
- `cost.km`: Cost per kilometer.
- `cost.location`: Delivery cost per location.
- `cost.run`: Cost per trip.

In this case, the cost at which the algorithm selects the optimal routing option is used. This is not the rate that is actually charged for using the vehicle, but rather the algorithm settings.

{% note %}

Note that the vehicle cost components are already set by default. To use custom values, contact your Yandex.Routing account manager.

{% endnote %}

## Vehicle tags

When you define a vehicle or courier in a request to the Router, you can assign order compatibility rules (or tags) to them.

Compatibility rules may be required if a vehicle has special equipment that is necessary to fulfill a particular order (for example, an isothermal van for transporting food).

Vehicle and order compatibility rules (vehicle tags) are set in the following fields:

- `vehicle.tags`: The vehicle properties that **can partially** match the properties required to fulfill the order.
- `vehicle.excluded_tags`: The vehicle properties that **must not** match the properties required to fulfill the order.

To [set order tags](properties-of-orders.md), use the `location.tags` request field.

{% note %}

Please note that order tags identify the vehicle characteristics that an order requires, whereas vehicle tags define the actual rules for compatibility of a particular vehicle with different orders.

{% endnote %}

Vehicle tags can be set as strings or regular expressions. Regular expressions are used to describe the more complex logic and vehicle/order compatibility rules.

Yandex.Routing uses the [POSIX Extended](https://ru.wikibooks.org/wiki/%D0%A0%D0%B5%D0%B3%D1%83%D0%BB%D1%8F%D1%80%D0%BD%D1%8B%D0%B5_%D0%B2%D1%8B%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F#%D0%A2%D1%80%D0%B0%D0%B4%D0%B8%D1%86%D0%B8%D0%BE%D0%BD%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%B3%D1%83%D0%BB%D1%8F%D1%80%D0%BD%D1%8B%D0%B5_%D0%B2%D1%8B%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F_%D0%B2_Unix) regular expression syntax. You can test regular expressions via [Regex101](https://regex101.com).

Below are some tag use cases.

### Example 1

Let's take a use case when a transportation company delivers food and drinks in small bulk quantities.
Some foodstuff must be delivered in isothermal trucks only.
At the same time, all drinks and some foodstuff can be delivered without refrigerators.
In addition, some customers can only accept a cargo if a vehicle is equipped with a tail lift.

To set these order constraints, specify the following tags in the `location.required_tags` field:

- `TAIL_LIFT`: For orders that can only be unloaded if a vehicle is equipped with a tail lift.
- `ISOTHERMAL_TRUCK`: For orders containing goods that require temperature-controlled transportation.
- `NORMAL_TRUCK`: For orders that do not require special conditions of transportation.

To set vehicle features, use the following tags in the `vehicle.tags` field:

- `TAIL_LIFT`: For vehicles equipped with a tail lift.
- `ISOTHERMAL_TRUCK`: For isothermal vehicles.
- `NORMAL_TRUCK`: For regular vehicles without an isothermal van.

{% note %}

Please note that a vehicle may have one or more tags or may not have them at all,
depending on its actual configuration. The same rule applies to order tags.

{% endnote %}

### Example 2

Let's take a use case when deliveries are carried out strictly across zones within a city. Moreover, there is
a rule that some vehicles are only allowed to carry out routes within specific zones.

To implement this scenario, set the correspondence between intracity orders and zones in the `location.required_tags` field.
Let's define 50 zones for different geographical areas with tags named `ZONE_1` ... `ZONE_50` and assign them to orders.

Next, we need to specify which zones a particular vehicle can work in.

For example, Vehicle 1 may be allowed to work in zones 20-30 and 30-39 and prohibited to work in any other zones:

- Set the `vehicle.required_tags` field value to `ZONE_((2|3)[0-9])$`.
- Set the `vehicle.excluded_tags` field value to `ZONE_([0-9]|[1][0-9]|[4-9][0-9])$`.

### Example 3

Let's take a use case when some orders have a constraint on a vehicle's body height.

For example, 2 meters, 2.3 meters, and 2.5 meters. Then they should have the appropriate tags: Max_200, Max_230, and Max_250.

For vehicles, tags are set in a more complex way, since a vehicle up to 2 meters high can deliver any orders, whereas a vehicle up to 2.8 meters high can only deliver some orders. That is, if you only use required_tags, then at a vehicle's height of:

- Up to 2 meters the vehicle.required_tags field will contain all the values Max_200, Max_230, and Max_250.
- 2 to 2.3 meters the vehicle.required_tags field will contain the values Max_230 and Max_250.
- 2.3 to 2.5 meters the vehicle.required_tags field will be set to Max_250.
- More than 2.5 meters, the vehicle.required_tags field will be empty.

## Vehicle priority

In a request to the Router, you can specify the priority of using certain vehicles. To specify the vehicle priority, use the `vehicle.priority` request field.

We recommend changing the priority value only if all vehicles have the same `vehicle.cost` value. In other cases, it's better to use the `vehicle.cost` ([Cost of a vehicle or courier](properties-of-vehicles.md)) to manage the vehicle use priority, since the priority is calculated as follows:

`The cost used in the algorithm = the cost of using the vehicle* 100 / vehicle.priority`

{% note %}

The default priority value is 100. If you want to specify some vehicles as higher priority, set them to a value greater than 100 (this will reduce their cost for the algorithm). Priority also works as a coefficient for all `vehicle.cost` components. If the cost of vehicles differs, setting the priority can make it difficult to analyze the routing results, so, in most cases, different costs are used in the `vehicle.cost` field to prioritize vehicles and to distinguish between your own/hired vehicles.

{% endnote %}

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>

