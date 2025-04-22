Stat Data Remover
=================
Removes data from a Stat report.


### Examples
Remove data for a week from 15 till 21 July (both dates included).

    report_data_remove
        --env production
        --token 'AQAD-...'
        --report 'Maps.Wiki/Report'
        --date-min 2020-06-15
        --date-max 2020-06-21
        --scale daily
        --execute


Authentication
--------------
The authentication token can be obtained [here][token].


[token]: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=801af94c94e040848ebe206086a7a4e2
