# Get information about upcoming rides

This request is used to learn the preliminary ride price for different classes and create a ride offer.

## Request syntax

```
POST https://business.taxi.yandex.ru/api/1.0/estimate
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

Order data is passed in the request body in JSON format:

#|
||**Field**|**Description**|**Format**||
||`route` {#route-param}| A block with information about the route. Ride coordinates are provided in the following format:``` route:[[<departure point longitude>,<departure point latitude>],[<destination point longitude>,<destination point latitude>]] ```
Required field. | Array||
||`requirements` {#requirements-param}| A list of ride requirements.

List of ride requirements — the list of order requirements may vary depending on the city. To find the supported requirements, send an empty object `{}` in the body of the `https://business.taxi.yandex.ru/client-api/3.0/cities` POST request. The response contains a list of cities. Cities are listed in the `city` field. Supported requirements and their codes are listed in the `"supported_requirements"` array. | Object||
||`phone` {#phone-param}| A phone number for contacting the passenger. | String||
||`selected_class`{#selected-class-param} | The ride class. Required field. | String||
|#


## Response field description

Responses may contain the following fields:

#|
||**Field**|**Description**|**Format**||
||`currency_rules` {#currency-rules-param}| A block with information about the currency. | Object||
||`code` {#code-param}| The currency code. | String||
||`sign` {#sign-param}| The currency symbol.| String||
||`template` {#template-param}| The template for comments with the price. | String||
||`text` {#text-param}| A text description of the currency. | String||
||`is_fixed_price`{#is-fixed-param} | Indicates if the price is fixed. Possible values:
- `true`: Price is fixed.
- `false`: Price is dynamic. | Logical||
||`service_levels`{#serv-levels-param} | A block with ride information for different fares. The block for each class contains the following fields:
- [name](#name-param)
- [price](#price-param)
- [price_raw](#price-raw-param)
- [details_tariff](#details-param) | Array of objects||
||`name`{#name-param} | The name of the class. | String||
||`price` {#price-param} | A text description of the ride price. | String||
||`price_raw` {#price-raw-param}| A numerical description of the ride price. | Number||
||`details_tariff` {#details-param}| An explanation of the fare. | Array of objects||
||`type` {#type-param}| The explanation type. Possible values:
- `price`: Minimum ride price.
- `comment`: Text comment about the fare. | String||
||`value` {#value-param} | The explanation value. | String||
||`fare_disclaimer`{#disclaimer-param} | An explanation of the price. | String||
||`offer` {#offer-param}| The ride offer. Use this field to [create a draft order](order-create.md) with the ride price indicated in the [price](#price-param) field.

The offer with the current price is valid for a limited time. If the offer expires, the response to the [Process an order](processing.md) request contains a 406 error code.

If the [phone](#phone-param) field is not specified in the request, the price is calculated without creating an offer. | String||
|#

## Request example

```
POST https://business.taxi.yandex.ru/api/1.0/estimate
...
Authorization: <OAuth token>


{
  "route": [
    [
      37.622504,
      55.753215
    ],
    [
      37.635813,
      55.839525
    ]
  ],
  "requirements": {
    "nosmoking": true,
    "conditioner": true
  },
  "phone": "+71234567890",
  "selected_class": "econom"
}
```

## Response example

An example response to this request looks like this:

```no-highlight
{
    "currency_rules": {
        "code": "RUB",
        "sign": "₽",
        "template": "$VALUE$ $SIGN$$CURRENCY$",
        "text": "rub"
    },
    "is_fixed_price": true,
    "service_levels": [
        {
            "class": "econom",
            "price": "460 rubles",
            "price_raw": "460",
            "details_tariff": [
                {
                    "type": "price",
                    "value": "from 99 rubles"
                },
                {
                    "type": "comment",
                    "value": "4 minutes included, then 9 rubles/minute"
                },
                {
                    "type": "comment",
                    "value": "2 kilometers included, then 9 rubles/kilometre"
                }
            ],
            "fare_disclaimer": "increased demand"
        },
        ...
    ],
    "offer": "1bfc6ef0377607d98deb6b91ab90ef2f"
}
```

## Response codes {#section_rrq_mfb_mhb}

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `400`: An unknown parameter or a parameter with an invalid value was passed in the request.
- `401`: The [OAuth token](quickstart.md) is incorrect.

