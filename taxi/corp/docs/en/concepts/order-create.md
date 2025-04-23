# Create a draft order

This request is used for creating a draft order.

{% note warning "Atteniton" %}

Sending this request doesn't initiate order processing.

{% endnote %}


To start processing an order, you must run the [Process an order](processing.md) request, passing the order ID that you received at the draft creation stage. This helps prevent duplicate orders in the event of a network error.

{% note warning "Atteniton" %}

You don't need to delete order drafts as they are erased automatically within 10 to 20 minutes.

{% endnote %}


## Request syntax

```
POST https://business.taxi.yandex.ru/api/1.0/client/{client ID}/order/
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

Order data is passed in the request body in JSON format. The field structure is provided in the [Example request](#req-ex) section.

#|
||Field | Description | Format||
||`comment` | The client's comment. | String||
||`fullname` | The client's first and last name. | String||
||`phone` | The client's phone number. | String||
||`due` | The date the order is completed. The time when a taxi should arrive at its first destination. Specified for delayed orders with a set arrival time. Value format: `YYYY-MM-DDThh:mm:ss(±hhmm)`. | String||
||`source` | A block with information about the departure point. Contains the following fields:

- `country`
- `fullname`
- `geopoint`
- `locality`
- `porchnumber`
- `premisenumber`
- `thoroughfare` | Object||
||`source.country` | The country. | String||
||`source.fullname` | The full address. | String||
||`source.geopoint` | The destination coordinates. The parameter format:``` [longitude,latitude] ``` | Array||
||`source.locality` | The town or location. | String||
||`source.porchnumber` | The entrance number. | String||
||`source.premisenumber` | The house and unit number. | String||
||`source.thoroughfare` | The name of the street or neighborhood (for addresses numbered by neighborhood). | String||
||`source.extra_data` | Additional information about door-to-door parcel delivery. This object can be nested in the `source` object (with information about the sender) or the `destination` object (with information about the recipient).

{% note warning "Attention" %}

The object is only available for the `express` and `courier` service classes (set in the [class](#class-desc) field) with the specified `door_to_door` requirement (set in the [requirements](#requirements-desc) field).

{% endnote %}

Contains the following fields:
```json "contact_phone": "+79031111111", "floor": "1", "apartment": "1", "comment": "my comment" ```
- `contact_phone`: The sender's/recipient's phone number. Format: string.
- `floor`: The floor of the sender/recipient. Format: string.
- `apartment`: The sender's/recipient's apartment. Format: string.
- `comment`: Delivery comment. Format: string. | Object||
||`interim_destinations` | A block with information about intermediary points along the ride. The list of fields for each object is the same as in the [source](#source-desc) block. | Array of objects||
||`destination` | A block with information about the ride destination point. The list of fields is the same as in the [source](#source-desc) block. | Object||
||`offer` | [The ride offer](route-stats.md#offer-param). | String||
||`class` | The ride class. Required field. | String||
||`requirements` | A block with order requirements.

Order requirements — the list of order requirements may vary depending on the city. To find the supported requirements, send an empty object `{}` in the body of the `https://business.taxi.yandex.ru/client-api/3.0/cities` POST request. The response contains a list of cities. Cities are listed in the `city` field. Supported requirements and their codes are listed in the `"supported_requirements"` array.| Object||
||`nosmoking` | Indicates a non-smoking driver. | Logical||
||`cost_center` | The name of the [client's cost center](cost-center-create.md). | String||
|#

The list of order requirements may vary depending on the city. To find the supported requirements, send an empty object `{}` in the body of the `https://business.taxi.yandex.ru/client-api/3.0/cities` POST request. The response contains a list of cities. Cities are listed in the `city` field. Supported requirements and their codes are listed in the `"supported_requirements"` array.

Request example:

```
curl -d"{}" https://business.taxi.yandex.ru/client-api/3.0/cities
...
Authorization: <OAuth token>
```

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`_id` | The order ID number. | String


## Request example {#req-ex}

#### Creating an order for a taxi

```json
POST https://business.taxi.yandex.ru/api/1.0/client/a2...d09/order/


{
    "comment": "some comment",
    "fullname": "First name Last name",
    "phone": "+71112223344",
    "due": "2013-04-01T14:00:00+0400",
    "source": {
         "country": "Russia",
         "fullname": "Russia, Moscow, Novosushchevskaya, 1",
         "geopoint": [
             33.6,
             55.1
         ],
         "locality": "Moscow",
         "porchnumber": "1",
         "premisenumber": "1",
         "thoroughfare": "Novosushchevskaya"
    },
    "interim_destinations": [{
        "country": "Russia",
        "fullname": "Russia, Moscow, Troitskaya, 15, 1",
        "geopoint": [
            37.6,
            55.7
        ],
        "locality": "Moscow",
        "porchnumber": "",
        "premisenumber": "15, 1",
        "thoroughfare": "Troitskaya"
    }],
    "destination": {
        "country": "Russia",
        "fullname": "Russia, Moscow, 8 Marta, 4",
        "geopoint": [
            33.1,
            52.1
        ],
        "locality": "Moscow",
        "porchnumber": "",
        "premisenumber": "4",
        "thoroughfare": "8 Marta"
    },
    "class": "econom",
    "requirements": {
        "nosmoking": true
    },
    "cost_center": "some cost center"
}
```

#### Creating an order for door-to-door delivery

```json
POST https://business.taxi.yandex.ru/api/1.0/client/a2...d09/order/


{
  "comment": "",
  "source": {
      "country": "Russia",
      "fullname": "Russia, Moscow, Lva Tolstogo st., 16",
      "short_text": "Lva Tolstogo st., 16",
      "short_text_from": "Lva Tolstogo st., 16",
      "short_text_to": "Lva Tolstogo st., 16",
      "geopoint": [
          37.587093,
          55.733969
      ],
      "locality": "Moscow",
      "premisenumber": "16",
      "thoroughfare": "Lva Tolstogo st.",
      "type": "address",
      "object_type": "other",
      "extra_data": {
          "contact_phone": "+79031111111",
          "floor": "1",
          "apartment": "1",
          "comment": "my comment"
      }
  },
  "class": "express",
  "requirements": {"door_to_door": true},
  "phone": "+79811234567",
  "destination": {
      "country": "Russia",
      "fullname": "Russia, Moscow, Tverskoy blvd., 1",
      "short_text": "Tverskoy blvd., 1",
      "short_text_from": "Tverskoy blvd., 1",
      "short_text_to": "Tverskoy blvd., 1",
      "geopoint": [
          37.597765,
          55.757992 
      ],
      "locality": "Moscow",
      "premisenumber": "27с1",
      "thoroughfare": "Tverskoy blvd.",
      "type": "address",
      "object_type": "other",
      "extra_data": {
          "contact_phone": "+79032222222",
          "floor": "2",
          "apartment": "123",
          "comment": "33"
      },
  "cost_center": "some cost center"
  }
}
```

## Response example

An example response to this request looks like this:

```no-highlight
{
        "_id": "3caa3587675b49deb62e3286b753b05e"
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `404 UNKNOWN_CITY`: Can't create a draft order in this city.
- `406 INACTIVE_USER`: Can't create a draft order for an inactive user.
- `406 TARIFF_IS_UNAVAILABLE`: Can't create a draft order with the specified class.

