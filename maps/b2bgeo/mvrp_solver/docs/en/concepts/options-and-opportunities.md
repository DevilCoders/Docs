# Reducing the risk of late arrivals

When finding a solution to a routing task, one of the priorities is to set routes that provide high-quality service to the end customer: ensure a courier's arrival in the specified time interval. This is especially relevant for customers with a large number of orders and narrow delivery windows: this problem is usually faced by online stores, delivery services, or suppliers of retail chains.

In Yandex.Routing, you can build routes in strict compliance with the order delivery window (see [Order delivery window](properties-of-orders.md)). However, there is often a need to set routes that are more pessimistic. When actually implementing them, a courier has an additional amount of time in case of unscheduled delays during the previous order delivery, unexpected traffic jams, and other contingencies.

To create routes like that, set the`options.minimize_lateness_risk` option to `true`.

### How it works

Yandex.Routing builds routes based on the forecast for the travel time between points on the road graph (for more information, see the article. It takes into account both the forecast and possible deviations from the predicted values. The `minimize_lateness_risk` parameter is responsible for factoring possible deviations in the resulting solution.

For example, an order's delivery window is from 8:00 to 9:00. A courier starts from the previous location at 7:30. The mathematical expectation of their trip duration is 81 minutes (conventionally, with a probability of 0.4 the courier will arrive in 75 minutes, with a probability of 0.4 – in 80 minutes, with a probability of 0.1 – in 90 minutes, and with a probability of 0.1 – in 100 minutes). This means that the system will schedule his arrival for 8:51.

However, for this trip, there is a probability of 0.1 that the courier will be 10 minutes late, that is, will arrive at 9:10.

If a possible deviation is outside the time window, it's taken into account in the final solution as a possible late arrival penalty for this order and, to calculate the penalty amount, the system uses the `locations.penalty.out_of_time.fixed` and `locations.penalty.out_of_time.minute` values, respectively.

For more information, see [Penalties for late arrival at an order location](properties-of-orders.md).

If the `minimize_lateness_risk` parameter is specified, these parameters are taken into account even when the order delivery window is hard and the `location.hard_window` option is set to `true`.

{% note %}

The use of the `minimize_lateness_risk` option, as a rule, degrades the rest of the solution metrics. There is always a downside to improving the customer service: you need to use more resources or make routes less optimal in terms of distance or total time. Therefore we recommend using this option only if you have the appropriate requirements.

{% endnote %}

The examples below show how the solution changes when using this option:

### Example 1

There are three orders with rather narrow and strict timeframes. The `minimize_lateness_risk` option is set to `false`. The algorithm plans 1 route with arrival at point 3 at 10:59, with a delivery window until 11:00.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/71b6824b-3c81522b-ad22756c-3cebfe0b) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/71b6824b-3c81522b-ad22756c-3cebfe0b) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#71b6824b-3c81522b-ad22756c-3cebfe0b)

### Example 2

Example 1, but with the `minimize_lateness_risk` option set to `true`.

The algorithm also plans 1 route, but the sequence of visiting points 2 and 3 differs. The route is now less optimal in terms of distance and travel time as compared to example 1. However, the courier has some extra time until the end of the order delivery window: the route involves less risk in terms of possible late arrival at the customer's address.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/add34c08-56c46c8f-624cce2c-35749300) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/add34c08-56c46c8f-624cce2c-35749300) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#add34c08-56c46c8f-624cce2c-35749300)

### Example 3

Example 2, but with much lower `locations.penalty.out_of_time.fixed` and `locations.penalty.out_of_time.minute` values as compared to the defaults.

The algorithm plans the same route as in Example 1. In this case, the algorithm had a choice: set a less optimal route that involves a lower risk in terms of possible late arrivals or set a more optimal route that involves a greater risk. Since the late arrival penalty amount is very small, the system chose the option with a more optimal route.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/2026c97b-88574e95-da251263-5038a623) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/2026c97b-88574e95-da251263-5038a623) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#2026c97b-88574e95-da251263-5038a623)

### Example 4

Example 2, but with much higher `locations.penalty.out_of_time.fixed` and `locations.penalty.out_of_time.minute` values as compared to the defaults.

The algorithm plans 2 routes, distributing orders across 2 vehicles: the amount of penalty for possible late arrivals exceeded the cost of using another vehicle.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/1d54a452-aed43d2d-cf779bc3-b5f0a338) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/1d54a452-aed43d2d-cf779bc3-b5f0a338) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#1d54a452-aed43d2d-cf779bc3-b5f0a338)

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>
