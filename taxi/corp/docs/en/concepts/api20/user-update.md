# Update user data

This request is used to update information about a client's user.

{% note info %}

We strongly recommend not changing the user's phone number. Instead, [create a new user](user-create.md).

{% endnote %}


## Request syntax

```
PUT https://b2b-api.go.yandex.ru/integration/2.0/users/{user ID}
```

**Request headers**

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](../quickstart.md).

User data is passed in the request body in JSON format:

#|
||**Field** | **Description** | **Format** | **Required**||
||`fullname` | The user's full name. | String | Yes||
||`phone` | The user's phone number. | String | Yes||
||`is_active` | Indicates that the user is active. An inactive user can't place an order and rides can't be ordered in their name. | Logical | Yes||
||`cost_centers_id` | ID of the cost center settings (if the client has new cost centers). Optional field.
If you don't include this field in the request, the main cost center will be assigned to the user (if the client has new cost centers). | String | Yes||
||`is_deleted` | Indicates an [archived user](user-archive.md). | Logical | No||
||`nickname` | The user's short name. | String | No||
||`cost_center` | The default name of the client's cost center. | String | No||
||`limits` | The limits on the amount a user can spend on services in a calendar month. | An array of elements that contains a separate element for each service. | No||
|#


Structure of the `limits` array element:

#|
||**Field:**|**Description:**|**Format:**|**Required:**||
||`limit_id`|The limit on the amount that a user can spend on a specific service in a calendar month.|String|Yes||
||`service`|The service name. Acceptable values: `taxi`, `eats2`, `drive`.| String|Yes||
|#

## Response field description

If the request is successful, an empty 200 response is returned.

## Request example

```
POST https://b2b-api.go.yandex.ru/integration/2.0/users/f65...c57d
...
Authorization: Bearer <OAuth token>

    {
        "fullname": "Ilya Ivanov",
        "phone": "+79990000000",
        "is_active": true,
        "nickname": "IIlya",
        "cost_centers_id": "123...fef",
        "cost_center": "some cost center", 
        "limits":[
            { 
                "limit_id": "abcdef_taxi",
                "service": "taxi" 
            },
            {
                "limit_id":"abcdef_eats",
                "service":"eats2"
            },
            {
                "limit_id":"abcdef_drive",
                "service":"drive"
            }
        ]   
     }
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `400`: An unknown parameter or a parameter with an invalid value was passed in the request.
- `401`: The [OAuth token](../quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.

