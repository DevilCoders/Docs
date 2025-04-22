# List of client's users

This request is used to get a list of a client's users.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client ID}/user?
department_id=<department ID> 
&limit=<number of records to output>
&skip=<number of records to skip>
&sorting_field=<field to sort by>
&sorting_direction=<sorting direction>
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

The request may contain the following optional arguments:

- `department_id`: ID of the department to filter employees by. If the value is `null`, the employees located in the root department are returned. If this parameter is omitted, all employees are returned, regardless of the department.
    
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
||`items` | A list of the client's users. | Array||
||`phone` | The user's phone number. | String||
||`role` | Block of information about the user role. | Object||
||`role_id` | The user role ID. | String||
||`cost_center` | The name of the [client's cost center](cost-center-create.md). | String||
||`nickname` | The user's short name. | String||
||`fullname` | The user's full name. | String||
||`department_id` | Department ID number. | String||
||`_id` | The user's ID. | String||
||`is_active` | Indicates that the user is active. An inactive user can't place orders and rides can't be ordered in their name. | Logical||
||`email` | The user's email address. | String||
||`spent` | The amount spent on orders for the current month. | Number||
||`sorting_field` | The field to sort by. | String||
||`sorting_direction` | The sorting direction. Possible values:
- `1`: Sort in ascending order.
- `-1`: Sort in descending order. | Number||
||`amount` | The number of records found. | Number||
||`limit` | The number of records returned. | Number||
||`skip` | The number of records skipped. | Number||
|#

## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/client/a2...d09/user
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "items": [
    {
      "phone": "+75551223455",
      "role": {
        "role_id": "1e0202a78f894ad38127aecf31140fbd"
      },
      "cost_center": "",
      "nickname": "",
      "fullname": "",
      "department_id": "233e725b0511459da7b38cb24f2d8fd7",
      "_id": "5a60b55b31b6437fae7991af44c0e087",
      "is_active": true,
      "email": "",
      "spent": 0
    },
    ...
    {
      "phone": "+79222222222",
      "role": {
        "role_id": "1e02r43d3d43dddrtt540fbd"
      },
      "cost_center": "",
      "nickname": "",
      "fullname": "test",
      "department_id": "233e725b0511459da7b38cb24f2d8fd7",  
      "_id": "686f8fc56c174dc08616f9563afc090a",
      "is_active": false,
      "email": "test@test.ru",
      "spent": 0
    }
  ],
  "sorting_direction": 1,
  "amount": 33,
  "limit": 100,
  "skip": 0,
  "sorting_field": "fullname"
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `400`: An unknown parameter or a parameter with an invalid value was passed in the request.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.

