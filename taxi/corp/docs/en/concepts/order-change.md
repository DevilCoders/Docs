# Edit draft order data

This request is used for editing information about a client's cost centers in the [draft order](order-create.md).

## Request syntax

```
PUT https://business.taxi.yandex.ru/api/1.0/client/{client ID}/order/{order ID}/change
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

Order data is passed in the request body in JSON format:

Field | Description | Format
----- | ----- | -----
`cost_center` | The name of the [client's cost center](cost-center-create.md). | String


## Response field description

If the request is successful, it returns an empty 200 response.

## Request example

```
PUT https://business.taxi.yandex.ru/api/1.0/client/a2...d09/order/a3...b386/change
...
Authorization: <OAuth token>

    { "cost_center": "some cost center" }
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `400`: An unknown parameter or a parameter with an invalid value was passed in the request.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The specified record wasn't found.

