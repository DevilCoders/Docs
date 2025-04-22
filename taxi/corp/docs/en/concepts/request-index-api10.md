# API 1.0

To call API version 1.0 methods, use the host:

```
https://business.taxi.yandex.ru/api/...
```

Below is a list of requests that can be sent to Yandex Taxi for the API version 1.0:

Request URL | Method | Description
----- | ----- | -----
/auth | GET | [Client information](auth.md)
/oauth/refresh | GET | [Update OAuth token](oauth-refresh.md)
/1.0/class | GET | [List of classes](class-list.md)
/1.0/client/{client_id} | GET | [Detailed client information](client-info.md)
/1.0/client/{client_id}/cost_centers | POST | [Create client's cost centers](cost-center-create.md)
/1.0/estimate | POST | [Get information about upcoming rides](route-stats.md)
/1.0/client/{client_id}/order | GET | [List of orders](order-list.md)
/1.0/client/{client_id}/order |POST | [Create a draft order](order-create.md)
/1.0/client/{client_id}/order/{order_id} | GET | [Detailed order information](order-info.md)
/1.0/client/{client_id}/order/{order_id}/cancel | POST | [Cancel an order](order-cancel.md)
/1.0/client/{client_id}/order/{order_id}/progress | GET | [Track an order](order-progress.md)
/1.0/client/{client_id}/order/{order_id}/processing | POST | [Process an order](processing.md)
/1.0/client/{client_id}/order/{order_id}/change | PUT | [Edit draft order data](order-change.md)
/1.0/client/{client_id}/role | GET | [List of employee roles](role-list.md)
/1.0/client/{client_id}/role |POST | [Create a new role](role-create.md)
/1.0/client/{client_id}/role/{role_id} | GET | [Detailed role information](role-info.md)
/1.0/client/{client_id}/role/{role_id} |PUT | [Edit a role](role-edit.md)
/1.0/client/{client_id}/role/{role_id} |DELETE | [Delete a role](role-delete.md)
/1.0/client/{client_id}/user | GET | [List of client's users](user-list.md)
/1.0/client/{client_id}/user |POST | [Create a new user](user-create.md)
/1.0/client/{client_id}/user/{user_id} | GET | [Detailed user information](user-info.md)
/1.0/client/{client_id}/user/{user_id} |PUT | [Update user data](user-update.md)
/1.0/client/{client_id}/user/{user_id} |DELETE | [Delete a user](user-delete.md)
/1.0/client/{client_id}/user/{user_id}/restore | PUT | [Restore a user](user-restore.md)
/1.0/client/{client_id}/geo_restrictions | GET | [Region list](region-list.md)
/1.0/client/{client_id}/geo_restrictions |POST | [Create a new region](region-create.md)
/1.0/client/{client_id}/geo_restrictions/{geo_id} | PUT | [Edit a region](region-edit.md)
/1.0/client/{client_id}/geo_restrictions/{geo_id} |DELETE | [Remove a region](region-delete.md)


