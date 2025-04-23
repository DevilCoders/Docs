# Track an order

This request is used to get the order status and location of the car assigned to the order.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client ID}/order/{order ID}/progress
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

#|
||**Field** | **Description** | *Format*||
||`status` | The order status. Possible values:
- `search`: The order is created, searching for a driver.
- `driving`: A driver was found and is driving to the pickup location.
- `waiting`: The driver arrived and is waiting for the employee.
- `transporting`: The employee is in the car and is on the way.
- `complete`: The order was completed successfully.
- `cancelled`: The order was cancelled by the client or the employee.
- `failed`: The order is cancelled by the taxi company because the driver can't complete it.
- `expired`: The status of the order is unknown. This status can be returned if the taxi company didn't send the order status data in time.
- `scheduling`: The order was created, the driver search will start shortly before pickup.
- `scheduled`: The order was created, a driver was assigned and will pick up the employee at the agreed time. An order with this status can be changed. | String||
||`vehicle` | Information about the car if one was assigned to your order. | Object||
||`location` | The coordinates of the car. | String||
|#

## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/client/a2d...d09/order/8b8...432/progress
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
    "status": "finished",
    "vehicle": {
        "location": [55.749884, 37.589688]
    }
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.

