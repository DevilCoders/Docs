Stat Copy Report
================
Copies data from one Yandex.Stat report to another, adds and renames dimensions if needed.

### Examples
Copy report:

    report_data_copy
        --env production
        --src  'Maps.Wiki/Source_Report'
        --dest 'Maps.Wiki/Destination_Report'
        --scale daily

Copy report, rename "dimension_old_name", add "new_dimension_name":

    report_data_copy
        --env production
        --src  'Maps.Wiki/Source_Report'
        --dest 'Maps.Wiki/Destination_Report'
        --scale continual
        --rename '{"dimension_old_name":"dimension_new_name"}'
        --new '{"new_dimension_name":"default_value"}'


Authentication
--------------
The tool acts on behalf of the user who executes it, therefore the tool must be able to authenticate itself. An OAuth token is used for this purpose. The following steps have to be performed by the user who runs this tool for the first time:
1. ```
   mkdir -p ~/.statbox
   chmod 700 ~/.statbox
   echo $'---\noauth_token: ' > ~/.statbox/statface_auth.yaml
   ```
2. [Get OAuth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=801af94c94e040848ebe206086a7a4e2).
3. Add this token to the created file.
4. `chmod 400 ~/.statbox/statface_auth.yaml`

More information about authentication can be found at [wiki](https://wiki.yandex-team.ru/statbox/statface/externalreports/statface-python-client).
