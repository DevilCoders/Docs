# Errors

| Error code | Error text | Error description |
| :--- | :--- | :--- |
| 401 | Not authorized request | Make sure you have transmitted a valid token |
| 404 | Delivery window in the past | The delivery window that you specified is in the past |
| 404 | Delivery window is too narrow | The window specified is too narrow. Time windows are accepted in GMT+0, UNIX/UTC format |
| 404 | Item's articles must be unique. Bad article: ... | You have specified the same SKUs |
| 404 | Cannot deliver | Unable to create a delivery claim. Window transmission error: delivery to the region is not supported, shipment orders have not been created |
| 404 | Dimensions should not exceed | Dimensions exceeded |
| 404 | Inconsistency billing details | You have errors in item costs. Check that `assessed_unit_price` ≥ `unit_price` |
| 400 | Incorrect station platform ID | Check that you transmitted a valid station ID |
| 400 | Incorrect JSON content. Please check the formatting | Cross-check against our integration examples |
| 400 | There is place with no items | You have a place with no items in it |
| 400 | There are items with no place | You have items without any place |
| 400 | Cannot parse ... info | Error when reading JSON. Check the data or contact support |
| 400 | There already was request with such code within this employer | Check the data. The key `operator_request_id` must be unique for each order |

