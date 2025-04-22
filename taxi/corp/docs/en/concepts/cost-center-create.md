# Create client's cost centers

This request is used to add information about a client's cost centers.

## Request syntax

```
PUT https://business.taxi.yandex.ru/api/1.0/client/{client ID}/cost_centers
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

Requests are sent with the `multipart/form-data` content type. This means you have to use the `Content-Type: multipart/form-data` header when sending the request.

The request body must pass an `.xls` file with information about the cost centers. Cost center values must be in the first column of the `.xls` file.

## Response field description

If the request is successful, it returns an empty 200 response.

## Request example

```
PUT https://business.taxi.yandex.ru/api/1.0/client/a2...09/cost_centers
...
Authorization: <OAuth token>


--Asde457BGe4h
Content-Disposition: form-data; name="cost_centers_file"; filename="cost_centers.xls"

(binary content of .xls file)
--Asde457BGe4h--


```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `400`: An unknown parameter or a parameter with an invalid value was passed in the request.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.
- `415`: The specified request content type isn't supported.

