# Purpose
Form [russian version](https://forms.yandex-team.ru/surveys/18592/), [english version](https://forms.yandex-team.ru/surveys/45986/) are intended for ordering single hosts into maintenance (with shutdown) and speeding up this process.

## The procedure for working with the form
1. Fill out the form:
* in the field `Operation type`, select `Hosts Power-OFF for ITDC maintenance`.
* in the field `List of host's IDs` you must specify the server inventory numbers, one number per line.
* in the field `Ticket from ITDC queue` queue, you have to specify original ticket for activity from ITDC queue.
* in the field `Responsible for the maintenance` you must specify the login of the person responsible for the work.
1. Wait for a ticket in the ticket from the ITDC queue that the hosts are turned off;
1. Perform work;
1. Turn on the server;
1. Close the ticket from the ITDC queue;
* nothing needs to be done with the corresponding ticket from the ITDC queue in the RUNTIMECLOUD queue

## How it works
1. After filling out the form  a ticket in `RUNTIMECLOUD`, queue will be created and associated with the ticket specified in the form from the ITDC queue.
1. A ticket from the RUNTIMECLOUD queue is processed by the robot. The robot performs the following actions:
* checks user rights for the operation
* validates input
* checks the limit on the number of simultaneous operations
* performs an operation
1. At each stage, in case of an error, the robot reports the operation status to both tickets with a comment with a description.

### Procedure for checking user rights for an operation
* verified by ABC group in charge. The responsible person should be in a group [Data Center IT Infrastructure Service](https://abc.yandex-team.ru/services/EXP/) with the role `Support`.
* if an error is detected, the reason for the error is written in both tickets, the ticket in the RUNTIMECLOUD queue closes, processing stops.

### Procedure for checking host requirements
* no more than **8** hosts in the ticket.
* hosts are in Wall-E.
* hosts are located in projects managed by RTC (the project has a tag `rtc`).
* all hosts are in the same rack.
* if an error is detected, the reason for the error is written in both tickets, the ticket in the queue `RUNTIMECLOUD` is closed, processing stops.

### Checking the number of simultaneous operations
* The limit on the number of simultaneous operations (tickets) is checked. Currently, the limit is set to **two** operations.
* in case of exceeding the limit, an appropriate entry is made in tickets and execution is suspended until a free quota appears.

### Operation order
* Hosts are sent the command `set-host-maintenance power-off: True`.
* In case of errors with any hosts, information about this is printed in both tickets.
* When **all** hosts are in `maintenance`, comment in both tickets is recorded and the ticket from the `RUNTIMECLOUD` queue is completed as resolved.
  **Note:** the robot monitors the fact of the host transfer to `maintenance`, which occurs after sending the command to `power-off`. The fact of shutting down the host is not verified. Usually, such a transition does not take much time.
* After the comment appearance in the ticket that the transfer to maintenance has taken place, if the hosts are not physically shut down yet, they can be turned off by the button.
