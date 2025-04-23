# Detailed order information

This request is used to get information about a client's order.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client ID}/order/{order ID}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

The request may contain the following optional arguments:

- `show_cancel_text`: Indicates that the response will contain information about ways to cancel the order. Possible values:
    - `true`: Respond with cancellation information.
    - `false`: Respond without cancellation information. Default value.
    

## Response field description

Responses may contain the following fields:

#|
||**Field** | **Description** | **Format** ||
||`_id` | The order ID. | String||
||`status` | The order status block. Contains the following fields:
- `full`. | Object||
||`status.full` | The order status. Possible values:
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
||`due_date` | The time when the ride should be completed. Value format: `YYYY-MM-DDThh:mm:ss(±hhmm)`. | String||
||`finished_date` | The actual date when the ride was completed. Value format: `YYYY-MM-DDThh:mm:ss(±hhmm)`. | String||
||`performer` | A block with information about the person fulfilling the order. | Object||
||`car` | The name of the car. | String||
||`fullname` | The driver's name. | String||
||`phone` | The driver's phone number. | String||
||`corp_user` | A block with information about the user. | Object||
||`user_id` | The user's ID number. | String||
||`destination` | A block with information about the destination point. | Object||
||`fullname` | The full address. | String||
||`geopoint` | A block with location coordinates. The parameter format:``` [longitude,latitude] ``` | Array||
||`source` | A block with information about the departure point. | Object||
||`cancel_rules` | A block with order cancellation information. | Object||
||`can_cancel` | Indicates if the order can be canceled. | Logical||
||`message` | A text description of the cancellation rules. | String||
||`state` | The terms of canceling an order. Possible values:
- `free`: Free cancellation.
- `minimal`: Cancellation with payment only for the car arrival.
- `paid`: Cancellation with full payment for the ride. | String||
||`title` | The name of the cancellation rules. | String||
||`cost` | The ride cost. | Number||
||`class` | The ride class. | String||
||`cost_center` | The name of the [client's cost center](cost-center-create.md). | String||
||`created_by` | The name of the user who created the order. | String||
|#

## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/client/a2...d09/order/8b...e432?show_cancel_text=true
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
    "_id": "8b8de2e41d204f42b0a775b2edd6e432",
    "status": "finished",
    "due_date": "2016-03-24T21:37:17",
    "finished_date": "2016-03-24T21:47:17",
    "performer": {
        "car": "Volkswagen Caravelle brown А123ВЕ",
        "fullname": "Sergey",
        "phone": "+75551234567"
    },
    "corp_user": {
        "user_id": "88eaf8ef4d8b4d8384f6064da13a1680"
    },
    "destination": {
        "fullname": "Russia, Moscow, Bolshaya Nikitskaya st., 13",
        "geopoint": [
            "37.600296",
            "55.750379"
        ]
    },
    "source": {
        "fullname": "Russia, Moscow, Timur Frunze st., 11/8",
        "geopoint": [
            "37.5887876121",
            "55.734141752"
        ]
    },
    "cancel_rules": {
        "can_cancel": true,
        "message": "You can cancel the ride for free now. You may have to pay if you cancel after the taxi arrives",
        "state": "free",
        "title": "Free cancellation"
    },
    "cost": 540,
    "class": "econom",
    "cost_center": "some cost center",
    "created_by": "Manager Anna"
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.

