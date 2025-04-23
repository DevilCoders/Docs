# Assessing the economic benefits of implementation

Yandex.Routing optimizes a solution in terms of the "Cost including penalties" indicator.

The cost of couriers is set in the `Vehicle` table. Penalties are imposed for violations of planning constraints, such as late arrival at an order location, vehicle shift violation, and so on. Penalties have standard recommended values (set in the XLS template) that you can adjust depending on your requirements.

Following the instructions below, you can assess the economic benefits of using Yandex.Routing by your company. To do this, we'll calculate the cost of routes created by your logisticians, then build routes using the Yandex.Router, and compare the costs.

## Data preparation

Prepare routes per day planned by your logistician. We recommend that you choose the busiest day.

Order delivery addresses must be geocoded (in the format of geographical coordinates). If you need to perform geocoding, use maps or the [Geocoder API](https://tech.yandex.com/maps/geocoder/).

Collect information about the actual end time for each route on that day. If you know that there were accidents on any of the routes, exclude the time spent to handle them.

## Uploading routes created by your logistician

- Open the Planning interface of [Yandex.Routing](https://yandex.com.tr/courier/) and download the XLS template.

- Fill in the `Orders`, `Vehicles`, and `Depot` sheets with the information prepared at the previous step.

- Link orders to vehicles according to the plan made by your logisticians. To do this:
    - In the `Vehicles` table, enter the vehicle number in the `Vehicle properties` field.
    - In the `Orders` table, enter the vehicle number in the `Required vehicle properties` field.

- In the `Vehicles` table, specify all cost components.

- Run a task in `Low` mode to calculate the metrics of the solution proposed by your logistician. Calculation in this mode is a convenient way to quickly calculate the metrics of a ready-made solution.

{% note %}

Planning with the `Low` quality doesn't guarantee high-quality optimization. To get reliable results, use `Normal` or `High` mode.

{% endnote %}

Hurray! You've made your first calculation. In the resulting solution, pay attention to the Total line. It shows the total metrics of the solution.

## Selecting planning parameters

First of all, make sure the `Uncompleted orders` table is empty. If it contains any orders, it means that incompatible constraints are set.  The reason for a failure to complete an order is indicated in the last column of the table. Fix the issue in the original request and restart the task.

If the cost with penalties in the **Total** line is not equal to the cost without penalties, the logistician violates the task constraints (or the constraints are not strict). Most often, the logistician has more accurate information about the existing task constraints. To compare the solutions under equal conditions, specify the same constraints. Therefore, you need to extend the task constraints so that the penalties approach zero.

Route by route, compare the actual end time of the route with the end time calculated by the Routing service. If the time is the same, the value of the `Service duration` field (the `Orders` sheet) is set correctly.

If the driver actually returns earlier or later, change the `Service duration` value and restart the calculation.

As soon as the route end time in the Router coincides with the actual end time, register the detected `Service duration` and go to the next step.

Pay attention to the `Load` indicator. If you see overloads in the resulting solution, the logistician believes that this is acceptable. Select the acceptable overload value for all vehicles, such as 108%. And restart the task.

{% note %}

Pay attention to the number of late arrivals. If they are not a one-time exception, the logistician believes that they are acceptable. If there are minor delays, set the order's hard_window = `FALSE` in the request. If the logistician is more than an hour late, you should extend the time window.

{% endnote %}

If the solution proposed by the logistician contains other penalties, the logistician either violates something else or considers these constraints insignificant. Hover over the yellow triangle in the route row to see what constraints are violated. Set the appropriate constraints in the request to make sure there are no penalties.

## Automatic routing

Use the request created as a result of the "Data Preparation" step. Save the request parameters to make a comparison of manual and automated planning with the same constraints.

To perform automatic routing:

- In the `Orders` table, delete the tags with the vehicle numbers.
- In the `Vehicles` sheet, add ALL the available vehicles and their costs. The Router will select the vehicles that are optimal to use.
- Run the optimization task in `Normal` mode.
- Compare the solution of your logistician with the Yandex.Routing solution based on the `Cost with penalties` metric.

{% note %}

Contact your Yandex.Routing account manager to discuss the results. In your email, give a link to the solution of your logistician and a link to the solution provided by automatic routing.

{% endnote %}

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>
