# Panoramas UGC proxy public backend

This is API documentation. SEDEM service documentation is one level up.
Requests should have Passport cookie with https authorization.

## HTTP codes

| HTTP code | Response | Explanation |
|---|---|---
| 200 Ok | proto ||
| 201 Created |  proto ||
| 204 No content | empty ||
| 400 Bad Request | xml | Request parameters malformed |
| 401 Unauthorized | xml | No valid cookie |
| 403 Forbidden | xml | User does not have access to this object |
| 404 Not Found | xml | Database object or handler not found |
| 409 Conflict | xml | Database update conflict |
| 422 Custom error | proto Error | Protobuf error code |
| 500 Internal Server Error | XML | Contact developers |

## Upload API

| Method | URI | Params (Body) | Success | Description |
|---|---|---|---|---|---|
| POST | `/v1/panoramas/create` | `shipmentId` (`image/jpeg`) | 200/201`Panorama`  | 422`Error` |
