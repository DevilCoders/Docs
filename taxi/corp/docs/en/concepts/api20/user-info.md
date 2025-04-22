# Detailed user information

This request is used to get detailed information about the client's user.

## Request syntax

```
GET https://b2b-api.go.yandex.ru/integration/2.0/users/{user ID}
```

**Request headers**

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](../quickstart.md).

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`fullname` | The user's full name. | String
`nickname` | The user's short name. | String
`is_active` | Indicates that the user is active. An inactive user can't place an order and rides can't be ordered in their name. | Logical
`is_deleted` | Indicates whether the user was deleted. | Logical
`phone` | The user's phone number. | String
`email` | The user's email address. | String
`cost_centers_id` | ID of the cost center settings (if the client has new cost centers). Optional field. | String
`cost_center` | The name of the client's cost center. | String
`limits` | The limits on the amount a user can spend on services in a calendar month. | An array of elements that contains a separate element for each service.


Structure of the `limits` array element:

#|
||**Field:**|**Description:**|**Format:**||
|| `limit_id`|The limit on the amount that a user can spend on a specific service in a calendar month.| String||
||`service`|The service name. Acceptable values: `taxi`, `eats2`, `drive`.|String||
|#

## Request example

```
GET https://b2b-api.go.yandex.ru/integration/2.0/users/f65...c57d
...
Authorization: Bearer <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "fullname": "Ilya Ivanov",
  "nickname": "IIlya",
  "is_active": true,
  "is_deleted": false,
  "phone": "+75551234567",
  "email": "",
  "cost_centers_id": "123...fef",
  "cost_center": "some cost center"",
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
- `401`: The [OAuth token](../quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.

