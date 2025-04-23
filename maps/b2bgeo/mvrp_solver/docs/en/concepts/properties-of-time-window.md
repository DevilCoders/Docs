# Properties of time windows

When setting a routing task, you often need to limit the order delivery window, depot operating hours, or vehicle shift time.

To limit the time in the Router, use the `time_window` field, which is a text description of the time range.

You can set time windows in absolute and relative formats discussed in detail below.

## Relative format of time windows

This format of time windows contains no absolute date and is defined as a pair of time values. For example, `07:00:00 - 23:00:00` for a window that starts at 7:00 and ends at 23:00 of the current day.

For windows that start or end on the following day (or any day in the future), the specified time should be supplemented with the number of days relative to the current time (or to the date specified in the `options.date` field). For example, `07:00:00 - 1.03:00:00` for a window that starts at 7:00 of the current day and ends at 3:00 of the following day. Or `1.07:00:00 – 1.15:00:00` for a window that starts at 7:00 the next day and ends at 15:00 the next day: the number before the window's time determines the 24-hour period that this window belongs to. 0 is referred to the current day. In this case, you should set the offset before both the lower and upper boundaries of the time interval.

The upper boundary of the window must always be greater than or equal to the lower boundary. A window like `07:00:00` - `03:00:00` causes an error. This error is especially frequent when specifying windows that pass into the next day or windows that end at midnight. For example, the `10:00:00` - `00:00:00` window is treated as incorrect. You should specify `10:00:00` - `1.00:00:00` instead.

The service interprets the formats of windows with no date relative to the current date and GMT+3 (Moscow) time zone or to the date specified in the `options.date` field and the time zone specified in the `options.time_zone` field.

{% note %}

A window like `00:00:00` – `23:59:59` means a round-the-clock time window only in the first 24 hours. It's relevant for a depot window: if planning involves, for example, 2 days (the current and next one), to indicate the depot's round-the-clock operation during the planning period, specify `00:00:00` – `1.23:59:59`.

{% endnote %}

### Example

The example below defines the time zone (Moscow time) for a request and time windows for the depot and orders with no date specified. The route is built as of January 20, 2019 (or the current date if the  `options.date` field is omitted).

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/472d65e2-3f445fad-1059bbf3-e032ecb1) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/472d65e2-3f445fad-1059bbf3-e032ecb1) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#472d65e2-3f445fad-1059bbf3-e032ecb1)

## Absolute format of time windows

This format contains the full date and start and end time of a window in ISO-8601 format (for example, `2019-10-10T07:00:00+03:00/2018-01-10T18:00:00+03:00` for a window that starts at 7:00 and ends at 18:00 Moscow time).

{% note %}

Note that when using the absolute time format, you can specify multiple time zones. This can be useful when setting windows for order delivery on the border of time zones.

{% endnote %}

{% note %}

When setting time windows in absolute format, make sure you fill in the `options.date` field. In this case, the `options.time_zone` field defines the time zone to be used for order delivery windows in the Router's response.

{% endnote %}

### Example

In the example below, the time windows set for the depot, orders, and shifts are specified with the date and time zone in ISO8601 format. The route is built as of January 21, 2019, which is specified in each time window.

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/bf7a9ba3-67cc7871-a7ad07da-2c372054) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/bf7a9ba3-67cc7871-a7ad07da-2c372054) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#bf7a9ba3-67cc7871-a7ad07da-2c372054)

## Hard and soft time windows

A time window is a constraint to be met when building a route. For an order's time window, for example, this means a delivery to be made within the specified time range.

You can set *hard* and *soft* time windows.

A *hard* window is a constraint that must be met without violation. If it's violated when creating a route, an order is completely excluded from the route and gets into the `dropped_locations` field in the Router's response.

A *soft* window is a constraint that may be violated at a penalty cost that is proportional to the delay. If it's violated when creating a route, the order isn't excluded from the route, but will be delivered later or earlier.

To manage hard time windows, use the `hard_window` field:

- `True`: The window is a *hard* constraint.
- `False`: The window is a *soft* constraint.

In practice, the use of *soft* windows lets you:

- Balance late arrivals across multiple orders if the specified number of vehicles doesn't allow all orders to be delivered on time.
- Be late when returning to the depot if all orders need to be delivered within a day.
- Exceed the vehicle shift time if this late arrival is necessary and allowed by business processes.

When setting *soft* windows, the following penalties are imposed:

- Late arrival penalty, one-time (`penalty.out_of_time.fixed`, added to the cost of the route if there's a late arrival).
- Late arrival penalty, per minute (`penalty.out_of_time.per_minute`, added to the cost of the route for each minute of late arrival).

If your business process doesn't allow for late arrivals, we recommend the following:

- When initially setting a routing task, use *hard* windows.
- Afterwards, use *soft* windows with custom values of late arrival penalties (for example, it's allowed to arrive 1-5 minutes late).

## Where do I set time windows?

In the Router, you can set time windows for the following entities:

- Orders (`locations`): Allowed time of arrival at the order location.
- Depot (`depot`): Depot opening hours.
- Vehicle shift (`vehicles[].shift`): Allowed time range for a shift.

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>

