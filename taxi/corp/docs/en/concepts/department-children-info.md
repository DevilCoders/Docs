# Get a subsidiary department list

The request is used to get information about subsidiary departments.

## Request syntax

```
GET https://business.taxi.yandex.ru/api/1.0/client/{client id}/department/{department id}/children
```

Request headers:

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](quickstart.md).

## Response field description

Responses may contain the following fields:

Field | Description | Format
----- | ----- | -----
`departments[]` | Department list. | String
`departments[]._id` | Department ID. | String
`departments[].name` | Department name. | String
`departments[].parent_id` | Parent department ID. | String


## Request example

```
GET https://business.taxi.yandex.ru/api/1.0/client/233e7...8fd7/departament/2f...071f34c53/children
...Authorization: <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
  "departments": [
    { 
            "id": "e26c430a0e3a4d3eb639987d085837e6",
            "name": "Department 1",
            "parent_id": "2f...071f34c53"
    },
    {
            "id": "cf7130024b034f548aa6c42bfa810efe",
            "name": "Department 2",
            "parent_id": "2f...071f34c53"

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

