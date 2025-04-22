# Planned vehicle route

In some cases, when planning routes, a logistician can assign orders to a specific vehicle for their own reasons. If you simply upload this route to the Router, orders in it can be redistributed among other vehicles to optimize their routes. To explicitly bind an order to a specific vehicle, use the `planned_route` parameter.

In this case, the selected orders are linked to the vehicle and are delivered in any case (even in violation of strict delivery constraints). However, the delivery sequence can be changed to optimize the route.

## Additional route planning

## Additional features

## Example 1

This example shows two requests that illustrate the use of the `planned_route` parameter in the event of [additional planning](additional-planning.md).

### Basic request

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/ee6652-335b23cc-29bb8b3c-eadc2731) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/ee6652-335b23cc-29bb8b3c-eadc2731) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#ee6652-335b23cc-29bb8b3c-eadc2731)

### Request with additional orders

[API request](https://courier.yandex.ru/vrs/api/v1/log/request/cf7e6770-555a439e-57105d49-2dc93e73) ⋅ [API response](https://courier.yandex.ru/vrs/api/v1/result/cf7e6770-555a439e-57105d49-2dc93e73) ⋅ [Open on the map](https://courier.yandex.ru/mvrp-map#cf7e6770-555a439e-57105d49-2dc93e73)

## Example 2

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>

