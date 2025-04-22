# Basic definitions

To start planning routes, define a depot, vehicles, and orders for a single planning interval.

As a result of planning, you'll get the optimal vehicle routes and metrics for analyzing the results.

Let's take a look at the main properties of a depot, vehicles, and orders in a real-life use case.

You can learn more about the properties and special cases of optimization below in the chapters [Properties of time windows](properties-of-time-window.md), [Weight and volume properties](properties-of-weight.md), [Vehicle properties](properties-of-vehicles.md), and [Order properties](properties-of-orders.md).

## Depot

A depot is a point where all routes start and may end. At the depot, orders are loaded into vehicles. You can only specify one depot in a single request. The depot must have opening hours specified.
For details of the parameters, see [Depot properties](properties-of-depot.md).

The depot parameters are set in the `depot` field.

## Vehicles

Orders can be delivered by regular vehicles or by couriers traveling on foot or by public transport. Vehicles and couriers have a common set of properties.

The vehicle or courier parameters are set in the `vehicles` field.

## Vehicle load capacity

You can set the capacity or load capacity of a vehicle. It's recommended to specify them in a request. Otherwise, the Router may build routes with overloaded vehicles.

The capacity and load capacity parameters are set in the `vehicle.capacity` field.

## Orders

Orders are locations where a cargo must be delivered. For each order, you should specify its geographical coordinates and a time window.

The order parameters are set in the `locations` field.

## Order coordinates

The location of an order is set as geographical coordinates corresponding to the parking or stop location at the order address.

If your system specifies delivery locations using an address, you should perform [geocoding](https://tech.yandex.com.tr/maps/geocoder/) (convert the address from text to geographical coordinates).

The parameters of order coordinates are set in the `location.point` field.

## Order delivery window

Any order must have a time window specified: the time interval when a vehicle or courier should arrive at the order delivery address.

The time window parameters are set in the `location.time_window` field.

## Order service duration

For each order, you can specify the time required for its delivery to the customer. This time includes any operations that a vehicle or courier performs after arrival at the order location, until the time of departure for the next location, such as delivering the order to the customer.

The service duration (in seconds) is set in the `location.service_duration_s` field.

## Order weight

You can specify the weight of each order. It's optional, but recommended to avoid overloading vehicles.

The order weight is set in the `location.shipment_size` field.

## Routes

The service output is a route that is a sequence of order deliveries at destinations for each vehicle with a predicted time of arrival at each order location.

In the service response, the routes are specified in the `routes` field.

## Metrics

In addition to optimized routes, the service response contains metrics for analyzing the effectiveness of planning. For example, the total distance and time of routes, the number and absolute time of late arrivals, and so on.

Metrics are calculated for all routes combined and for each route separately. They are specified in the `metrics` response field.

## Route cost

Optimization reduces the cost of routes. The cost consists of the following components:

- The total vehicle cost (in RUB per kilometer, per hour, and per use of the vehicle).
- The amount of penalties for violation of business constraints (penalties for a failure to complete an order, for violation of time windows, and so on).

The cost is calculated for all routes combined and for each route separately. It's specified in the `metrics` response field.

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>
