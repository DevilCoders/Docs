# Depot properties

A depot in Yandex.Routing is a point where all routes start and may end.
If you have couriers who need to start their route from a location other than a depot, read the instructions in [A vehicle's departure from a location other than a depot](properties-of-vehicles.md).

To define orders use the `depot` request field.

## Depot ID

A depot's unique number (ID) is a required attribute that is set in the `id` field. The ID must be unique within a single request.

You can use any unique depot number from your accounting system.

{% note %}

Please note that the depot ID must not match the order IDs.

{% endnote %}

## Depot coordinates

In Yandex.Routing, you can set the depot location as geographical coordinates in the [WGS84](https://wikipedia.org/wiki/WGS_84) system, corresponding to the depot address point. If your system specifies the depot location using the address, you should perform [geocoding](https://tech.yandex.com.tr/maps/geocoder/) (converting an address given in free format into geographical coordinates).

Note that coordinates like `0.0` won't be processed correctly and will result in an error when sending requests to the Router.

To set the depot coordinates, use the `point` field.

## Depot time window

The depot defined in the request must have a time window that specifies the depot's operating hours.

To set them, use the `time_window` field.

A time window is set in [one of the following formats](properties-of-time-window.md#otnositelnyi-format-vremennykh-okon):

- `07:00:00 - 23:00:00`: A window that starts at 7:00 and ends at 23:00 of the current day.
- `2019-10-10T07:00:00+03:00/2018-10-10T23:00:00+03:00`: A window that is set for a certain date and time zone.

Depending on the window type, vehicles that should end their route at the depot may return there strictly before the end of the depot opening hours (a **hard** window) or may violate this constraint (a **soft** window). For details, see [Hard and soft time windows](properties-of-time-window.md#zhestkie-i-miagkie-okna)

To manage hard time windows, use the `hard_window` field:

- `True`: A hard window.
- `False`: A soft window.

If you use a **soft** time window, you can additionally set penalties for violating the window:

- `penalty.out_of_time.minute`: A penalty per minute of late arrival or early departure.
- `penalty.out_of_time.fixed`: A fixed penalty for one-time late arrival or early departure.

A departure from the depot is also possible before the time window start. This case is discussed in detail in [Flexible vehicle start time](properties-of-depot.md).

{% note %}

When setting a time window for the depot, consider the cases when a vehicle needs to return to the depot. If the vehicle doesn't have time to return to the depot and the time window set for the depot is hard, some orders may be uncompleted. If in doubt, it's better to specify the depot operating hours for the entire planning time and make them flexible.

{% endnote %}

## Depot service duration

In the Router, you can set the total service duration for the depot, which is the time that any vehicle or courier should spend at the depot:

- `depot.service_duration_s`: Time before the start of each trip.
- `depot.finish_service_duration_s`: Time before the end of each trip.

You can use the total depot service duration to take into account the time required for paperwork per driver or to average the time for loading the vehicle.

{% note %}

You can set an order-specific loading time at the depot. For more information, see [Service duration for loading an order at a depot](properties-of-orders.md).

{% endnote %}

### Example 1

Set the service duration of 10 minutes at the start and end of any route at the depot that opens at 07:00:00.

In the created route, the time of arrival at the first order location will be 07:34:15, provided that it takes 00:24:15 to get there. So the vehicle spent 10 minutes at the depot before starting the trip.

At the end of the route, the time of arrival at the depot is 08:07:43. 10 minutes of service duration is added to this time. This is reflected in the metric of the total duration of the entire route.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/e1fc8462-4795c1ab-de2ddc83-65db91af) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/e1fc8462-4795c1ab-de2ddc83-65db91af) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#e1fc8462-4795c1ab-de2ddc83-65db91af)

### Example 2

In this example, there are three orders and each order takes 100% of the vehicle's capacity. Therefore three separate trips are planned. You can see that the depot.service_duration_s and depot.finish_service_duration_s values are added at the start and end of each trip, respectively.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/6124b3fc-95d19804-3cac3658-f42350c4) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/6124b3fc-95d19804-3cac3658-f42350c4) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#6124b3fc-95d19804-3cac3658-f42350c4)

## Flexible start time

By default (`depot.flexible_start_time` is FALSE), vehicles start their route from the depot immediately after it opens (or the vehicle shift starts) and once the orders are loaded.

If you set the value to TRUE, a vehicle's departure from the depot can be scheduled not from the depot window or vehicle shift start time boundary, but for a later time.

Examples:

1. The vehicle shift starts at 09:00 and the depot starts working at 08:30. The `depot.flexible_start_time` parameter is set to `FALSE`. When planning, the system takes into account that any route assigned to this vehicle must start at 09:00, even if the first order's window is from 13:00 to 14:00 and it takes the vehicle no more than 15 minutes to get from the depot to this order location.
2. The vehicle shift starts at 09:00 and the depot opens at 08:30. The `depot.flexible_start_time` parameter is set to `TRUE`. If the first order's window is from 13:00 to 14:00 and it takes the vehicle no more than 15 minutes to get from the depot to this order location, the route planner can schedule the courier's departure from the depot not for 09:00, but for a later time (for example, 12:30), if this doesn't violate any other constraints.

## Depot capacity

In certain cases, you need to limit the maximum speed of loading vehicles at the depot. To do this, use the `depot.throughput` request field.

The depot capacity is set in weight units that can be processed by the depot in one hour:

- `throughput.kg_per_hour`: Depot capacity (kg/hr).
- `throughput.units_per_hour`: Depot capacity, units/hr (pallets, boxes, or kegs).

When setting the capacity, it isn't optimized: the capacity acts as a limit that shouldn't be exceeded.

If the time of loading at the depot is specified for each order, the system considers it in addition to the order weight, when checking the capacity limit.

### Example

The example below defines a depot with the same service duration at the start and end of a route (for example, the time required for exchanging documents), and different loading times for each order at the depot.

{% note %}

Please note that the time of arrival at the first order location corresponds to the total time at the depot equal to 960 seconds + the time it takes to get to the first order location.

{% endnote %}

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/ae86b55c-98db6331-e42f6ea3-73e86d8f) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/ae86b55c-98db6331-e42f6ea3-73e86d8f) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#ae86b55c-98db6331-e42f6ea3-73e86d8f)

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>
