# Load balancing option

Often, the main priority when planning routes is to achieve a relatively balanced distribution of orders across vehicles or couriers. For example, when you need to use all available resources, vehicles or couriers, in any case.

To ensure load balancing, the Router has an option named `balanced_groups`. Load balancing can be performed by route time, by the number of stops en route, or by both criteria at the same time.

## How it works

A balanced group is a property of a vehicle shift. The group ID is specified in the `vehicles.shifts.balanced_group_id` field. The load balancing option works independently for each group.

The balancing parameters are set in the `options.balanced_groups` field. These include:

- Group ID (it's also used in the `vehicles.shifts.balanced_group_id` field).

- The amount of penalties for deviation from the average route time and number of stops: `options.balanced_groups.penalty.hour` and `options.balanced_groups.penalty.stop`, respectively.

{% note %}
The `options.balanced_groups.penalty.hour` and `options.balanced_groups.penalty.stop` attributes have default values.
{% endnote %}

### Special considerations

It's recommended to balance the load of vehicles that are initially in equal conditions. This may pertain to various parameters of a task: the duration and time of vehicle shifts, the density of orders for a specific group of vehicles, the load capacity, the tags, and so on. For vehicles that have different conditions, we recommend setting different balanced groups. For example:

1. Vehicles have different shift durations: some of them have an 8-hour shift and the other – a 6-hour shift. The load balancing for these vehicles should be performed separately, since their route times will initially differ and they will complete different number of orders for objective reasons.
1. Couriers work the morning and evening shifts (of the same duration) and are routed within the same request. Let's assume the number of orders in the morning and in the evening is uneven. Then it's necessary to balance the load of morning and evening couriers either separately or only by route time, as the average number of orders (and, accordingly, stops en route) for the courier working in the morning and the courier working in the evening will probably differ.
1. The same vehicles are used, but there are many orders in the city and few orders in the regions on different routes. This task can only be balanced by route time, because, most likely, vehicles that travel a long distance will be able to complete less orders.
1. Vehicles of different load capacity are used. They usually deliver a different number of orders, so you need to either set different balanced groups for different load capacity or balance the load of the vehicles only by route time (the second option is preferable).

{% note %}

With balancing, you usually get routes that are less optimal in terms of the overall metrics of the solution (by the "Distance"/"Route time" final indicator) and sometimes in terms of the number of vehicles involved. When penalties for unbalanced load increase, a more balanced solution is obtained at the expense of route optimality.

{% endnote %}

The load balancing option balances routes within a single specific planning task you run. If the task is to balance the load on resources for an extended period of time (for example, within a month), it should be implemented outside the Router, through a separate process. In this process, couriers are assigned to routes based on the accumulated value that is being balanced against. For example, let couriers accumulate the total working time. After planning routes on a given day, the courier who has the minimum accumulated value (the total working time) is assigned the longest route, and vice versa. Balancing will thus be performed not within a specific day, but over a certain period. Moreover, on this particular day, routes may be optimal, even though unbalanced.

## Example 1

There are 52 orders and 3 couriers in the task. Solution to the task without balancing.

Planning result:

| Courier | Number of stops en route | Distance, km | Route time |
| ----------- | ---------------------------------- | ------------ | ---------------- |
| Courier 1 | 19 | 50 | 10:49 |
| Courier 2 | 17 | 47.4 | 09:50 |
| Courier 3 | 16 | 35.8 | 09:04 |
| **Total** | **52** | **133.1** | **29:43** |

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/f8104987-98abd9b7-85ba65f9-cdacfbc8) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/f8104987-98abd9b7-85ba65f9-cdacfbc8) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#f8104987-98abd9b7-85ba65f9-cdacfbc8)

## Example 2

We have the same task as in Example 1, but it's supplemented as follows:

- Activate the load balancing option.
- Set a single balanced group.
- Use the default amount of penalties for unbalanced routes.

Planning result:

| Courier | Number of stops en route | Distance, km | Route time |
| ----------- | ---------------------------------- | ------------ | ---------------- |
| Courier 1 | 17 | 54.1 | 09:56 |
| Courier 2 | 17 | 41.9 | 09:48 |
| Courier 3 | 18 | 48.7 | 10:05 |
| **Total** | **52** | **144.7** | **29:49** |

{% note %}

Routes are now more balanced in terms of the "Number of stops en route"/"Route time" indicator, but the overall metrics of the solution (the "Distance"/"Route time" final indicator) are now worse than in Example 1.

{% endnote %}

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/310cebd-b1d819bb-7dc6f7af-293fd377) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/310cebd-b1d819bb-7dc6f7af-293fd377) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#310cebd-b1d819bb-7dc6f7af-293fd377)

## Example 3

We have the same task as in Example 1, but it's supplemented as follows:

- Activate the load balancing option.
- Balance routes by route time only.
- Increase the amount of penalties for unbalanced routes relative to the default value.

Planning result:

| Courier | Number of stops en route | Distance, km | Route time |
| ----------- | ---------------------------------- | ------------ | ---------------- |
| Courier 1 | 17 | 47.5 | 10:09 |
| Courier 2 | 18 | 50 | 10:09 |
| Courier 3 | 17 | 52.5 | 10:09 |
| **Total** | **52** | **150** | **30:27** |

{% note %}

Couriers work the same amount of time now, but the overall metrics of the solution are even worse. The reason is that the algorithm based on increased penalties for unbalanced routes tries to find a solution that is not so much optimal as balanced.

{% endnote %}

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/725b0ff3-7b78f2e7-eacb2a8e-3d8afe1e) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/725b0ff3-7b78f2e7-eacb2a8e-3d8afe1e) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#725b0ff3-7b78f2e7-eacb2a8e-3d8afe1e)

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>
