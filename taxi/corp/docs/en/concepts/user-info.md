# Detailed user information

This request is used to get detailed information about the client's user.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client ID}/user/{user ID}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

#|
||**Field** | **Description** | **Format**||
||`phone` | The user's phone number. | String||
||`role` | A block with information about the user's role. | Object||
||`department_id` | Department identification number. | String||
||`role_id` | The user role ID number. | String||
||`cost_center` | The name of the [client's cost center](cost-center-create.md). | String||
||`nickname` | The user's short name. | String||
||`fullname` | The user's full name. | String||
||`is_active` | Indicates that the user is active. An inactive user can't place an order and rides can't be ordered in their name. | Logical||
||`_id` | The user's ID number. | String||
||`email` | The user's email address. | String||
||`spent` | The amount spent on orders for the current month. | String||
|#

## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/client/a2...d09/user/f65...c57d
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "phone": "+75551234567",
  "role": {
    "role_id": "1e0202a78f894ad38127aecf31140fbd"
  },
  "department_id": : "233e725b0511459da7b38cb24f2d8fd7", 
  "cost_center": "some cost center"",
  "fullname": "Ilya Ivanov",
  "nickname": "IIlya",
  "_id": "f65556fd272f459b9ebc67b25756c57d",
  "is_active": true,
  "email": "",
  "spent": 0
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.

