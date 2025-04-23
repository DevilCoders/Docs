# Process an order

This request is used to pass an order created with the [Create a draft order](order-create.md) request for processing.

## Request syntax

```
POST /client/{client ID}/order/{order ID}/processing
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`_id` | The order ID number. | String
`status` | The order status block. | Object
`simple` | The [simplified order status](order-list.md#simple-desc). | String
`full` | [Detailed order status](order-list.md#full-desc). | String
`description` | Order [description status](order-list.md#description-desc). | String


## Request example

```
POST https://business.taxi.yandex.ru/api/1.0/client/a2...d09/order/3c...b05e/processing
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
    "_id": "3caa3587675b49deb62e3286b753b05e",
    "status": {
        "simple": "active",
        "full": "search",
        "description": "Your taxi will arrive in N minutes."
    }}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The specified record wasn't found.
- `406`: The ride price changed since the [offer](route-stats.md) was received. Receive the offer again, pass the offer number in the [Create a draft order](order-create.md) request, and send the order for processing.

