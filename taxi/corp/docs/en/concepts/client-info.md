# Detailed client information

This request is used to get detailed information about a client.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client ID}
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`comment` | A comment about the client. | String
`yandex_login` | The Yandex account name. | String
`cost_centers_file_name` | The name of the [cost centers file](cost-center-create.md). | String
`contract_id` | The client's contract ID number. | String
`billing_name` | The client's name for billing. | String
`is_active` | Indicates the client is active. An inactive client can't order rides. | Logical
`cabinet_only_role_id` | The ID of the user role that doesn't have the right to place orders. | String
`_id` | The client's ID number. | String
`email` | The client's email address. | String
`name` | The client's name. | String


## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/client/a2...d09
...
Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "comment": "",
  "yandex_login": "example-company",
  "cost_centers_file_name": "CC.xls",
  "contract_id": "49975/16",
  "billing_name": "ExampleCompany",
  "is_active": true,
  "cabinet_only_role_id": "1e0202a78f894ad38127aecf31140fbd",
  "_id": "a2...d09",
  "email": "example-mail@example-company.ru",
  "name": "Test Company"
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](quickstart.md) is incorrect.
- `400`: An unknown parameter was passed in the request.
- `403`: The client doesn't have sufficient rights to execute this request.

