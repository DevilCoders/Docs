# Route node visit detection tool

## Description

This tool is run manually.
```
$ ./route_node_visit_detection --help
usage: route_node_visit_detection [-h] --env {stable,testing} --route-id ROUTE_ID [--file-settings FILE_SETTINGS] [--file-visits FILE_VISITS]
                                  [--log-level {DEBUG,INFO,WARNING,ERROR}] [--yav-token YAV_TOKEN]

Display information when courier on route route_id was close to orders. Script must be run from host which has access to ya-courier-backend PostgreSql database

options:
  -h, --help                                           show this help message and exit
  --env ENV                                            Environment: testing or stable
  --route-id ROUTE_ID                                  Route id to analyze
  --file-settings SETTINGS_FILE                        File with company, route, depot settings, see: settings.json.example
  --file-visits FILE_VISITS                            File for output result
  --log-level                                          Logging level
```
