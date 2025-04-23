# List of classes

This request is used to get information about all available classes.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/class? 
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
    
- `lat`: Latitude. This parameter is used to specify the region that classes are requested for.
    
- `lon`: Longitude. This parameter is used to specify the region that classes are requested for.
    

## Response field description

Responses may contain the following fields:

#|
||**Field** | **Description** | **Format**||
||`items` | A list of classes. | Array||
||`_id` | Class ID. | String||
||`name` | The name of the class. | String||
||`amount` | The number of records found. | Number||
||`sorting_direction` | The sorting direction. Possible values:
- `1`: Sort in ascending order.
- `-1`: Sort in descending order. | Number||
||`sorting_field` | The field to sort by. | String||
|#

## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/class?lat=55.76&lon=37.65
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "items": [
    {
      "_id": "vip",
      "name": "Business"
    },
    {
      "_id": "business",
      "name": "Comfort"
    },
    {
      "_id": "comfortplus",
      "name": "Comfort+"
    },
    {
      "_id": "minivan",
      "name": "Minivan"
    },
    {
      "_id": "econom",
      "name": "Economy"
    }
  ],
  "amount": 5,
  "sorting_direction": 1,
  "sorting_field": "name"
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `400`: An unknown parameter or a parameter with an invalid value was passed in the request.
- `403`: The client doesn't have sufficient rights to execute this request.

