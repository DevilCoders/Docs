# Detailed role information

This request provides detailed information about a user's role.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client ID}/role/{role ID}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

#|
||**Field** | **Description** | **Format**||
||`name` | The name of the employee's role. | String||
||`putable` | Indicates if the user can place an order from the app. `false` means that users with this role can only order taxis through managers. | Logical||
||`classes` | A list of available classes. | Array||
||`limit` | The limits on the amount a user can spend on rides in a calendar month. | Number||
||`deletable` | Indicates if the role can be deleted. | Logical||
||`_id` | The role ID. | String||
||`department_id` | Department identification number. | String||
||`no_specific_limit` | Indicates that this role doesn't have a limit on the total ride cost. Possible values:
- `true`: There is no limit. The value passed in the `limit` parameter won't be used.
- `false`: There is a limit.

Optional field. | Logical||
||`restrictions` | A block with information about the role restrictions. | Array of objects||
||`type` | The restriction type. Possible values:
- `weekly_date`: Restrictions on days of the week.
- `range_date`: Restrictions by date. | String||
||`days` | Days of the week when ride orders are available. Possible values:
- `mo`: Monday.
- `tu`: Tuesday.
- `we`: Wednesday.
- `th`: Thursday.
- `fr`: Friday.
- `sa`: Saturday.
- `su`: Sunday.

This field is only used for `weekly_date` type restrictions. | Array of strings||
||`start_time` | The time when the order becomes available. Value format: `HH:MM:SS`.

This field is only used for `weekly_date` type restrictions. | String||
||`end_time` | The time when the order will no longer be available. Value format: `HH:MM:SS`.

This field is only used for `weekly_date` type restrictions. | String||
||`start_date` | The date when the order becomes available.

Value format: `YYYY-MM-DDThh:mm:ss`||

||`end_date` | The date when the order will no longer be available.

Value format: `YYYY-MM-DDThh:mm:ss`

This field is used only for `range_date` type restrictions. | String||
||`geo_restrictions` | A block that contains information about non-restricted ride regions. | Array of objects||
||`geo_restrictions.source` | Starting ride region ID.

If the field is left empty, then any region is allowed.

At least the `source` or `destination` field must be filled in. | String||
||`geo_restrictions.destination` | Ending ride region ID.

If the field is left empty, then any region is allowed.

At least the `source` or `destination` field must be filled in. | String||
||`geo_restrictions.is_bidirectional` | Indicates that rides can go in either direction.
Possible values:
- `true`: Rides are allowed in both directions.
- `false`: Rides are allowed only from the starting region to the ending region.

Optional field.

Default value: `false`. | Logical||
|#

## Request example

```
GET business.taxi.yandex.ru/api/1.0/client/a2...d09/role/1e0...fbd
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "name": "Test role",
  "putable": false,
  "classes": [
    "vip",
    "minivan",
    "econom",
    "business",
    "comfortplus"
  ],
  "limit": 0,
  "deletable": false,
  "_id": "1e0202a78f894ad38127aecf31140fbd",
  "department_id": "233e725b0511459da7b38cb24f2d8fd7",
  "restrictions": [
         {
             "type":"weekly_date",
             "end_time":"22:00:00",
             "start_time":"23:59:00",
             "days":["mo","tu","fr"]
         }
     ],
  "geo_restrictions": [
         {
             "source": "geo_restriction_id1", 
             "destination": "geo_restriction_id2"
         },
         {
             "source": "geo_restriction_id3"
         }
     ]
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.

