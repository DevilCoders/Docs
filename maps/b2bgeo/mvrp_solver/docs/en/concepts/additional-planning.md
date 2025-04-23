# Additional route planning

Often, you have a task to plan a route when some of the orders are already distributed across vehicles and this distribution needs to be maintained. This happens, for example, when you need to create an order-picking task for a depot, but don't know some of the orders yet. Or when the couriers are already en route and, while they're on the way, you receive `pickup` orders that one of the couriers will have to pick up. In general, an additional planning task occurs when it isn't possible to solve the routing task completely within one iteration and it has to be carried out in parts, with the transfer of the previous iteration results to the next planning.

Basically, additional planning is required in two situations:

1. Some orders are already distributed across routes and there are undistributed delivery orders, **but the vehicles haven't left the depot yet**.
1. Additional orders are received (such as `pickup` orders), **but the vehicles have already left the depot**.

In both cases, it's necessary to maintain the distribution of already scheduled orders and additionally distribute new (unassigned) orders across vehicles that have free time/space.

## How it works

In each situation, it's important to know whether to maintain the sequence of already distributed orders. If yes, use the `vehicles.visited_locations` property. Otherwise, use the `vehicles.planned_route` property.

### In situation 1 (the vehicles haven't left yet)

To make a request, you need to know:

- Distributed orders for each vehicle.
- New orders received since the last planning.

In the new request for additional planning, in the `planned_route` (`visited_locations`) field, specify the IDs (`locations` or `id`) of distributed orders (from the previous planning iteration) for each vehicle.

### In situation 2 (the vehicles have already left)

To make a request, you need to know:

- Distributed orders for each vehicle.
- The location of each vehicle at the time of additional planning (this can also be the location of the last completed order or the next order in the sequence).
- A list of completed orders.
- New orders received since the last planning.

In the new request for additional planning:

1. For each vehicle, in the `planned_route` (`visited_locations`) field, specify the IDs (`locations` or `id`) of orders that are already distributed (from the previous planning iteration), but **not yet completed at the time of additional planning **.
1. Add "dummy" orders to the list of orders, which correspond to each vehicle's current locations. This can be omitted if the current location is that of the last completed order or the next order in the sequence.
1. For each vehicle, in the `visited_locations` field, specify as the first element the ID of the current location and the start time from this point.

{% note %}
For vehicles that were not used previously, you need to set the correct departure parameters: either change the start time of the vehicle shift or specify the current location at the depot in the `visited_locations` field.
{% endnote %}

1. Remove the completed orders from the list of orders (considering item 2: if the last completed order's location is used as the current location, you don't need to remove it).

### General considerations

The initial distribution of orders, after which additional planning is required, should be carried out so that the vehicles have free time/space left (otherwise, you can't fit additional orders in). To do this, you can reduce the vehicle shift time, use the `balanced_groups` option or set load restrictions (specify a smaller capacity for vehicles).

{% note %}
All the additional restrictions imposed in the first iteration to artificially load the vehicles not to their full capacity, should be removed **during additional planning**.
{% endnote %}

You can use tags to prevent adding orders to some favorite vehicles.

## Basic task

In the task, there are 70 orders and 9 available couriers and the `balanced_groups` option is used for balancing.

We get 5 couriers in the solution.

Planning result:

| Courier | Number of locations | Sequence of orders |
| ---------- | -------------------- | ----------------------------------------------------------------- |
| Courier 1 | 14 | 45, 31, 58, 24, 52, 54, 39, 47, 19, 30, 43, 28, 29, 49 |
| Courier 3 | 17 | 18, 37, 38, 17, 2, 59, 34, 35, 26, 32, 20, 69, 5, 50, 15, 21, 6 |
| Courier 4 | 14 | 44, 16, 53, 70, 27, 64, 65, 40, 60, 4, 63, 33, 56, 48 |
| Courier 6 | 11 | 46, 11, 1, 10, 8, 41, 14, 12, 13, 22, 9 |
| Courier 7 | 14 | 3, 23, 51, 55, 42, 36, 68, 66, 61, 25, 7, 67, 57, 62 |

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/ee6652-335b23cc-29bb8b3c-eadc2731) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/ee6652-335b23cc-29bb8b3c-eadc2731) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#ee6652-335b23cc-29bb8b3c-eadc2731)

Next, let's discuss various methods of additional planning relative to the basic task.

### Example 1

Additional planning at the depot **with a change** in the sequence of orders in the routes.

In the request, we set 110 orders (40 of them are new relative to the basic task) and 9 available couriers. For 5 couriers, specify the distribution from the basic task in `planned_route`. In addition, use the `balanced_groups` option for balancing.

We get 7 couriers in the solution.

Planning result:

| Courier | Number of locations | Sequence of locations relative to the basic task |
| ---------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Courier 1 | 16 | Two orders added:<br/>45, 31, 58, 24, 52, **87**, 54, 39, **100**, 47, 19, 30, 43, 28, 29, 49 |
| Courier 2 | 14 | New route |
| Courier 3 | 18 | One order added:<br/>18, 37, 38, 17, 2, 59, 34, 35, 26, 32, 20, 69, **104**, 5, 50, 15, 21, 6 |
| Courier 4 | 19 | Five orders added, the sequence has changed greatly:<br/>_27_, _64_, _65_, _40_, **99**, _60_, _4_, _53_, _70_, 44, 16, **102**, 63, 33, **85**, 56, **88**, 48, **84** |
| Courier 6 | 14 | Three orders added, the sequence has changed:<br/>46, **80**, 11, **71**, _12_, 10, 8, _1_, **83**, _14_, _41_, 13, 22, 9 |
| Courier 7 | 16 | Two orders added, minor changes in the sequence:<br/>3, 23, **79**, 51, _42_, _55_, 36, 68, 66, 61, 25, 7, 67, **108**, 57, 62 |
| Courier 8 | 13 | New route |

{% note %}

The orders planned in the basic task remained assigned to the same couriers, but:

- The couriers from the basic solution have new orders added **across other points en route**.
- The couriers from the basic solution have the previously planned order sequence changed.
- Two new routes added.

{% endnote %}

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/cf7e6770-555a439e-57105d49-2dc93e73) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/cf7e6770-555a439e-57105d49-2dc93e73) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#cf7e6770-555a439e-57105d49-2dc93e73)

### Example 2

Additional planning at the depot **without changes** in the sequence of orders in the routes.

In the request, we set 110 orders (40 of them are new relative to the basic task) and 9 available couriers. For 5 couriers, specify the distribution from the basic task in `visited_locations`. In addition, use the `balanced_groups` option for balancing.

We get 7 couriers in the solution.

Planning result:

| Courier | Number of locations | Sequence of locations relative to the basic task |
| ---------- | -------------------- | ---------------------------------------------------------------------------------------------------- |
| Courier 1 | 17 | Three orders added:<br/>45, 31, 58, 24, 52, 54, 39, 47, 19, 30, 43, 28, 29, 49, **106, 93, 101** |
| Courier 3 | 17 | Unchanged route:<br/>18, 37, 38, 17, 2, 59, 34, 35, 26, 32, 20, 69, 5, 50, 15, 21, 6 |
| Courier 4 | 18 | Four orders added:<br/>44, 16, 53, 70, 27, 64, 65, 40, 60, 4, 63, 33, 56, 48, **84, 96, 85, 88** |
| Courier 6 | 14 | Three orders added:<br/>46, 11, 1, 10, 8, 41, 14, 12, 13, 22, 9, **80, 71, 79** |
| Courier 7 | 15 | One order added:<br/>3, 23, 51, 55, 42, 36, 68, 66, 61, 25, 7, 67, 57, 62, **108** |
| Courier 8 | 15 | New route |
| Courier 9 | 14 | New route |

{% note %}

The orders planned in the basic task remained assigned to the same couriers, but:

- The couriers from the basic solution have new orders added **at the end of the route**.
- Two new routes added.

{% endnote %}

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/c7e01f43-b49d7ac8-7526c777-c43b1545) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/c7e01f43-b49d7ac8-7526c777-c43b1545) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#c7e01f43-b49d7ac8-7526c777-c43b1545)

### Example 3

Additional planning when the vehicles/couriers have already left the depot (**without changing** the sequence of orders in the routes).

At the time of planning, we assume that 15 orders have been completed (3 orders for each of the 5 couriers from the basic task) and remove them from the additional planning task.

As a result, we set 100 orders in the request (40 new orders, 55 uncompleted orders from the basic task, and 5 courier starting points) and 9 available couriers. For 5 couriers, specify the distribution from the basic task in `visited_locations`. In addition, use the `balanced_groups` option for balancing.

We get 8 couriers in the solution (3 of them are new couriers that start from the depot).

Planning result:

| Courier | Number of locations\* | Sequence of locations relative to the basic task |
| ---------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Courier 1 | 12 | One order added:<br/>_45, 31, 58 (completed orders),_ 1001 (starting point), 24, 52, 54, 39, 47, 19, 30, 43, 28, 29, 49, **101** |
| Courier 2 | 10 | New route |
| Courier 3 | 14 | Unchanged route:<br/>_18, 37, 38 (completed orders),_ 1003 (starting point), 17, 2, 59, 34, 35, 26, 32, 20, 69, 5, 50, 15, 21, 6 |
| Courier 4 | 13 | Two orders added:<br/>_44, 16, 53 (completed orders),_ 1004 (starting point), 70, 27, 64, 65, 40, 60, 4, 63, 33, 56, 48, **84, 88** |
| Courier 6 | 11 | Three orders added:<br/>_46, 11, 1 (completed orders),_ 1006 (starting point), 10, 8, 41, 14, 12, 13, 22, 9, **80, 71, 79** |
| Courier 7 | 12 | One order added:<br/>_3, 23, 51 (completed orders),_ 1007 (starting point), 55, 42, 36, 68, 66, 61, 25, 7, 67, 57, 62, **108** |
| Courier 8 | 11 | New route |
| Courier 9 | 12 | New route |

\ * – excluding the completed ones and the starting point.

{% note %}

In this solution, all couriers start at 11:00 and new orders are added at the end of the route.

{% endnote %}

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/6435873e-cf57c514-36bd86b9-c4e6f300) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/6435873e-cf57c514-36bd86b9-c4e6f300) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#6435873e-cf57c514-36bd86b9-c4e6f300)

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>
