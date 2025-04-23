# Routes that are resistant to changes in delivery windows

Frequently, when a delivery is scheduled, a customer can't accept an order at the specified time for reasons beyond a courier's control. However, the customer still wants to get the order even if the delivery window is violated. With a perfectly planned route, this is impossible, since the courier has to go to the next location and delays lead to increasing problems with the delivery of subsequent orders.

In Yandex.Routing, you can build routes that are resistant to possible changes in delivery windows. In this case, orders are grouped closer to each other so that the courier could deliver another order and then get back. With this planning, routes are less optimal in terms of other parameters (such as distance, time, and number of vehicles), but more resistant to delivery window violations.

To plan routes like that, set the `options.proximity_factor` option to a value from 0 to 10, where 0 stands for no order grouping and 10 is maximum order grouping. Recommended values: From 0 to 0.6. Higher values can lead to excessive grouping of delivery points and severe route degradation.

### How it works

When building routes with the activated `options.proximity_factor` option, Yandex.Routing changes the sequence of points several times when calculating the optimal time and distance for a route, thus simulating changes in delivery windows using orders. In this case, the specified value works as a coefficient with which a penalty for a possible change in the route time or length is added to the solution. With this approach, the algorithm finds it more efficient to merge close points into one route, even though this may make the overall solution worse.

{% note %}

The use of the `options.proximity_factor` option usually degrades the rest of the solution metrics. There is always a downside to improving the customer service: you need to use more resources or make routes less optimal in terms of distance or total time. Therefore we recommend using this option only if you have the appropriate requirements.

{% endnote %}

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>

