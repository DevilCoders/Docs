# Cancel an order

This request is used for canceling an order that was created.

## Request syntax

```
POST https://business.taxi.yandex.ru/api/1.0/client/{client ID}/order/{order ID}/cancel
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

Order data is passed in the request body in JSON format:

Field | Description | Format
----- | ----- | -----
`state` | The status of the cancellation. To get the cancellation status, use the [Detailed order information](order-info.md) request with the `show_cancel_text=true` parameter. | String


## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`_id` | The ID of the order to cancel. | String


## Request example

```
POST https://business.taxi.yandex.ru/api/1.0/client/a2...d09/order/9b...7ee8/cancel
...
Authorization: <OAuth token>        

{
    "state": "free"
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
- `400`: The request is invalid.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `404`: The order wasn't found.
- `409`: The order can't be canceled.

