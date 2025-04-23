quotateka --abc <client-abc-slug> <command> <args>

commands:
  - quota <command> <args>
    sub-commands:
      - info [--account <account>, ...] [--provider <provider>, ...]
      - set <account> <provider>:<resource>:(<absolute-limit>|<relative-limit>)
      - move <account> <account> <provider>:<resource>[:<limit>]

  - account <command> <args>
    sub-commands:
      - info
      - create <account> --name <name> [--description <description>]
      - rename <account> [--name <name>] [--description <description>]
      - close <account>
      - reopen <account>
      - add <account> --tvm <tvm-id> --name <tvm-name>
      - remove <account> --tvm <tvm-id>


$ quotateka --abc taxi-service quota info --provider driving-router --provider renderer-tilesgen
┌ taxi-service ┬────────────────┬────────────────┬───────────────────┬───────────────────┐
│              │ driving-router │ driving-router │ renderer-tilesgen │ renderer-tilesgen │
│              │    general     │     heavy      │       raster      │       vector      │
├──────────────┼────────────────┼────────────────┼───────────────────┼───────────────────┤
│      testing │     20rps      │      5rph      │        3rps       │       100rps      │
├──────────────┼────────────────┼────────────────┼───────────────────┼───────────────────┤
│   production │     40rps      │     10rph      │        5rps       │       700rps      │
├──────────────┼────────────────┼────────────────┼───────────────────┼───────────────────┤
│ used / total │ 60rps / 100rps │ 15rph / 20rph  │    8rps / 10rps   │  800rps / 1000rps │
└──────────────┴────────────────┴────────────────┴───────────────────┴───────────────────┘

$ quotateka --abc taxi-service quota move testing production driving-router:general:10
┌ taxi-service ┬────────────────┐
│              │ driving-router │
│              │    general     │
├──────────────┼────────────────┤
│      testing │ 20rps -> 10rps │
├──────────────┼────────────────┤
│   production │ 40rps -> 50rps │
├──────────────┼────────────────┤
│ used / total │ 60rps / 100rps │
└──────────────┴────────────────┘
Deploy displayed quotas? [y/N] y

$ quotateka --abc taxi-service quota set testing driving-router:general:+15
┌ taxi-service ┬─────────────────────────┐
│              │      driving-router     │
│              │         general         │
├──────────────┼─────────────────────────┤
│      testing │      10rps -> 25rps     │
├──────────────┼─────────────────────────┤
│   production │          50rps          │
├──────────────┼─────────────────────────┤
│ used / total │ 60rps -> 75rps / 100rps │
└──────────────┴─────────────────────────┘
Deploy displayed quotas? [y/N]

$ quotateka --abc taxi-service account info
Account: testing
Name: Testing staging
Description: Testing staging of taxi service
Default: false  Closed: false
Created: 2020-10-30 22:45
Updated: 2020-10-30 22:46
TVM ids:
    src-router-maps_test: 2019773

Account: production
Name: Production staging
Description: Production staging of taxi service
Default: true  Closed: false
Created: 2020-10-30 22:45
Updated: 2020-10-30 22:46
TVM ids:
    src-router-maps: 2019775
    route-calc: 2019337
    candidates: 2014780
