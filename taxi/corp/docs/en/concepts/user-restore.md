# Restore a user

This request is used to restore a client's deleted user.

## Request syntax

```
PUT https://business.taxi.yandex.ru/api/1.0/client/{client ID}/user/{user ID}/restore
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

User data is passed in the request body in JSON format:

#|
||**Field** | **Description** | **Format**||
||`email` | The user's email address. | String||
||`fullname` | The user's full name. | String||
||`department_id` | Department identification number. | String||
||`nickname` | The user's short name. | String||
||`role` | A block with information about the user's role. The role can be specified in the following ways:
- Using the [existing role ID](role-create.md#role-id-desc).
- Using a new user role description. Role description fields are the same as in the [Create a new role](role-create.md) request (except the [name](role-create.md#name-desc) field). | Object||
||`role_id` | The user role ID number. | String||
||`classes` | A list of classes available to the user. Pass this field if the `role_id` parameter in the `role` block was omitted. | Array||
||`limit` | The limits on the amount a user can spend on rides in a calendar month. | String||
||`phone` | The user's phone number. | String||
||`is_active` | Indicates that the user is active. An inactive user can't place an order and rides can't be ordered in their name. | Logical||
||`cost_center` | The name of the [client's cost center](cost-center-create.md). | String||
|#


## Response field description

If the request is successful, an empty 200 response is returned.

## Example requests

Request specifying an existing role:

```
PUT https://business.taxi.yandex.ru/api/1.0/client/a2...d09/user/3caa3587675b49deb62e3286b753b05e
...
Authorization: <OAuth token>
        
    {
        "email": "example-mail@example-company.ru",
        "fullname": "Ilya Ivanov",
        "department_id": "233e725b0511459da7b38cb24f2d8fd7",
        "nickname": "IIlya",
        "role": {
            "role_id": "620d2b39bb154e3ebe5debc8341b3471"
        },
        "phone": "+75551234567",
        "is_active": false,
        "cost_center": "some cost center"
    }
      
```

Request specifying a new role:

```
POST https://business.taxi.yandex.ru/api/1.0/client/a2...d09/user/
...
Authorization: <OAuth token>

    {
        "email": "example-mail@example-company.ru",
        "fullname": "Ilya Ivanov",
        "department_id": "233e725b0511459da7b38cb24f2d8fd7", 
        "nickname": "IIlya",
        "role": {
            "limit": 10000,
            "classes": ["econom"],
            "restrictions": [
                {
                    "days": ["mo", "we", "sa"],
                    "start_time": "00:00:00",
                    "end_time": "23:59:00",
                    "type": "weekly_date"
                }
            ],
            "geo_restrictions": [
                {
                    "source": "geo_restriction_id1", 
                    "destination": "geo_restriction_id2";
                },
                {
                    "source": "geo_restriction_id3";
                }
            ]
        },
        "phone": "+75551234567",
        "is_active": false,
        "cost_center": "some cost center"
    }

```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.

