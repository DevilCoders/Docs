# List of orders

This request is used to get information about all of a client's orders.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client ID}/order? 
limit=<number of records>
&skip=<number of records to skip>
&sorting_field=<field to sort by>
&sorting_direction=<sorting direction>
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

The request may contain the following optional arguments:

- `limit`: The number of records to output. If this parameter is omitted, information about the first 100 records is returned.
    
- `skip`: The number of records to skip. If this parameter is omitted, information starting from the first record is returned.
    
- `sorting_field`: The name of the field to sort by.
    
- `sorting_direction`: The sorting direction. The following values are permitted:
    - `1`: Sort in ascending order.
    - `-1`: Sort in descending order.
    

## Response field description

Responses may contain the following fields:

#|
||**Field** | **Description** | **Format**||
||`items` | A list of the client's orders. | Array||
||`status` | The order status block. Contains the following fields:
- `simple`
- `full`
- `description` | Object||
||`simple` | Simplified order status. Possible values:
- `active`: The order is active (searching for a driver, the driver arrived, the order is being fulfilled).
- `delayed`: The order is postponed (the order won't be fulfilled in the near future).
- `finished`: Final status (the order is cancelled, completed, or its status won't change). | String||
||`full` | Detailed order status. Possible values:
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
||`description` | Order status description. Possible values:
- «Taxi is on the way.»
- «Your taxi will arrive in N minutes.»
- «Fulfilling order.»
- Empty string. Returned if the order was completed. | String||
||`due_date` | The time when the ride should be completed. Value format: `YYYY-MM-DDThh:mm:ss(±hhmm)`. | String||
||`corp_user` | A block with information about users on the ride. | Object||
||`user_id` | The client's user ID. | String||
||`cost_with_vat` | The cost of the ride including VAT. | String||
||`finished_date` | The actual end time of the ride. Value format: `YYYY-MM-DDThh:mm:ss(±hhmm)`. | String||
||`source` | The pickup address block. | Object||
||`fullname` | Full address of the pickup point. | String||
||`cost` | The ride cost. | Number||
||`cost_center` | The name of the [client's cost center](cost-center-create.md). | String||
||`_id` | The order ID. | String||
||`class` | The ride class. | String||
||`sorting_direction` | The sorting direction. Possible values:
- `1`: Sort in ascending order.
- `-1`: Sort in descending order. | Number||
||`amount` | The number of records found. | Number||
||`limit` | The number of records returned. | Number||
||`skip` | The number of records skipped. | Number||
||`sorting_field` | The field to sort by. | String||
|#

## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/client/a2...d09/order/?limit=3
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "items": [
    {
      "status": {
        "simple": "finished",
        "full": "complete",
        "description": ""
      },
      "due_date": "2016-12-16T14:36:00",
      "corp_user": {
        "user_id": "faf968ec87174da2970c034903256ef3"
      },
      "cost_with_vat": "309.16",
      "finished_date": "2016-12-16T14:45:50",
      "source": {
        "fullname": "Russia, Moscow, Polina Osipenko st., 18/2"
},
      "cost": 262.0,
      "cost_center": "",
      "_id": "4971bcb610224d729728253c8bcb6201",
      "class": "econom"
    },
    {
      "status": {
        "simple": "finished",
        "full": "cancelled",
        "description": ""
      },
      "due_date": "2016-04-28T12:16:00",
      "corp_user": {
        "user_id": "a975c091f1e74b8f9e1c23b5189bafee"
      },
      "source": {
"fullname": "Russia, Moscow, Timur Frunze st."
      },
      "cost_center": "some cost center",
      "_id": "44d359d466944e38ab43353eb8552f48",
      "class": "econom"
    }
  ],
  "sorting_direction": -1,
  "amount": 127,
  "limit": 100,
  "skip": 0,
  "sorting_field": "due_date"
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `400`: An unknown parameter was passed in the request.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.

