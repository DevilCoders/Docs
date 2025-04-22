# Soft window for a courier shift

Sometimes it's necessary to extend a courier's working hours. At the same time, you still need to limit the maximum length of a shift and set a period that you should fall within. For example, there is a 14-hour window for couriers to perform deliveries (say, from 8:00 to 22:00), but each courier is allowed to work no more than 8 hours.

In Yandex.Routing, you can schedule shifts with hard time windows and the desired shift length. In this case, the length of a vehicle shift doesn't affect the working time start, it only affects the time that will be spent on completing orders. With this planning, the load that doesn't fit within the desired shift of a vehicle is distributed either to others or to the same vehicle, but with penalties imposed for exceeding the shift length.

### How it works

Yandex.Routing builds a route in a usual way, but all orders that can't be completed within the `max_duration_s` are added to the route with the penalty specified in the `shift.penalty.late` field, if it's specified, or in the `shift.penalty.out_of_time` field, if not. If the estimated order cost including penalties is higher than the cost of completing the order by another courier, the order is assigned to another courier.

For example, the length of a shift (the `shift.time_window` value) is strictly from 8:00 to 20:00. By default, a route is built to use the minimum number of couriers who work 12 hours. If you specify `max_duration_s = 8`, the load is distributed between the couriers and each of them works approximately 8 hours.

However, some couriers may still work more than 8 hours, because it's more cost-efficient to pay for extra hours than to have the order delivered by another courier.

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>

