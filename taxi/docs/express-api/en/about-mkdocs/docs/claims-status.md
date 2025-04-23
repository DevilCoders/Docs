# Status description

| Status | Description |
| :--- | :--- |
| `new` | New claim. |
| `estimating` | The claim is being evaluated (selection of the vehicle type according to the cargo parameters and cost calculation). |
| `estimating_failed` | The claim could not be evaluated. The reason can be seen in `error_messages` in the response to the `/info` operation. |
| `ready_for_approval` | The claim has been successfully evaluated and is awaiting confirmation from the client. |
| `accepted` | The claim is confirmed by the client. |
| `performer_lookup` | The claim is accepted for processing. Intermediate status before creation of order. |
| `performer_draft` | Looking for a driver. |
| `performer_found` | A driver was found and is driving to point **A**. |
| `performer_not_found`* | A driver couldn't be found. Try again after a while. |
| `pickup_arrived` | The driver arrived at point **A**. |
| `ready_for_pickup_confirmation` | The driver is waiting for the sender to provide the confirmation code. |
| `pickuped` | The driver collected the cargo. |
| `pay_waiting` | The order is waiting for payment (relevant for payment upon receipt). |
| `delivery_arrived` | The driver arrived at point **B**. |
| `ready_for_delivery_confirmation` | The driver is waiting for the recipient to provide the confirmation code. |
| `delivered`* | The driver delivered the cargo. |
| `delivered_finish` | Order is completed. |
| `returning` | The driver had to return the cargo and is driving to the return point. |
| `return_arrived` | The driver arrived at the return point. |
| `ready_for_return_confirmation` | The driver is at the return point and is waiting to be told the confirmation code. |
| `returned` | The driver returned the cargo. |
| `returned_finish`* | Order is completed. |
| `cancelled`* | The order was canceled by the client for free. |
| `cancelled_with_payment`* | The order was canceled by the client for a fee (the driver had already arrived). |
| `cancelled_by_taxi`* | The driver canceled the order (before receiving the cargo). |
| `cancelled_with_items_on_hands`* | The client canceled the claim for a fee without the need to return the cargo (the claim was created with the `optional_return` flag). |
| `failed`* | An error occurred while executing the order and further execution is not possible. |

\* Final delivery status. Further order execution is impossible. Try creating a new claim if necessary.