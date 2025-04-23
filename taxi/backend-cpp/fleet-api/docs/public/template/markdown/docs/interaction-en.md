# Interaction

Interaction with the API via:
```text
https://fleet-api.taxi.yandex.net
```

Data is transferred via secure protocol HTTPS.
The JSON format is used to represent the data in the request and response fields.

## Request headers

General headers for API requests:

| Heading | Description |
| - | - |
| X-Client-ID | Client ID |
| X-API-Key | Secret API key |
| Accept-Language | Accept Language (default `en`) |

## Response Codes

The following response codes are used in the API:

| Code | Reason | Description |
| - | - | - |
| 200 | OK | Request completed successfully |
| 400 | BadRequest | Incorrect request parameters |
| 401 | Unauthorized | Missing authorization parameters |
| 403 | Forbidden | Not enough rights for the request |
| 404 | NotFound | Resource not found |
| 409 | Conflict | Operation could not be completed due to change conflict |
| 429 | TooManyRequests | Limit exceeded (see restrictions below) |
| 500 | InternalServerError | Internal server error|

## Error format

The API regulates the format of unsuccessful responses to a request:

```json
{
  "code": "Machine-readable error code",
  "message": "Human-readable error message"
}
```

## Restrictions

Following restrictions apply while using the API:

* No more than 2 requests per second
* No more than 5000 requests per hour

If the limits are exceeded, the code 429 Too Many Requests is returned.

## Feedback

Questions regarding the API can be sent at [api-taxi@yandex-team.ru](mailto:api-taxi@yandex-team.ru).

