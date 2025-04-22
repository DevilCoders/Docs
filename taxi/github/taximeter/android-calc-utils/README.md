# android-calc-utils
This is a few command line tools which helps upload track/tariff/zones
from back-end for launching taximeter functional tests

# Deal with sources

1. First of all you should compile this tool. For this step JDK 8 is required
(Oracle JDK is strongly recommend)
2. Use `git clone` for getting repository sources
3. After JDK installing you should open terminal and `cd` in root of git cloned
directory
4. Launch the following terminal command: `./gradlew clean build`
5. If compilation completed successfully executable jar will be on
`{root_project_dir}/build/lib` directory


# Pre requirements
1. Before starting please check your actual JRE version with following command:
`java -version` because required version is `1.8+`
2. Generate personal YQL OAuth token on this page:
https://yql.yandex-team.ru/?settings_mode=token and put this one into `~/.yql/token`
file. Note that you should have token without any line breaks and spaces
(right now is 39 bytes size).

# How to download track

You should use following console command:

`track`

### Arguments:

Required arguments:

    -order_id <order id>
    -order_date <YYYY-MM>

Optional arguments:

`-server <production/testing>`  default: `production`
`-server_time <true/false>`  default: `false`
`-partner <true/false>`  default: `true`
`-yt_cluster <hahn/banach>`  default: `hahn`
`-path <absolute/directory/path>`  default:`/download`


### Order id

Remember that taxi-backend and taximeter-backend have different ids for the same order. If you got `order_id` from taximeter admin panel, than use `-partner true`. Otherwise use `-partner false` or just omit parameter.

### Order date

You should specify `order_date` in format `YYYY-MM`. For example:

`2018-03` — :ok:

`2018-3` — wrong

`2018-03-12` — wrong

### Sample:

`java -jar calc-utils-0.1.1.jar track -order_id 2a80546b63ac4ef697f0ef130a1237e25 -order_date 2018-06 -server testing -partner false -path sub_dir`

This sample downloads track with partner id `2a80546b63ac4ef697f0ef130a1237e25`
from testing server into `/sub_dir` directory.

### How to view track on map:

After download you'll find file like `track_2a80546b63ac4ef697f0ef130a1237e25.json` inside download folder. Copy it content into js, that located at `[THIS_REPO]/src/test/tools/track.js`

You need to replace `[]` with data from your track. Note that you should save `;` after data. Like this:

```javascript
TRACK = 
[
  {
    "log_datetime": "2018-06-23T01:32:25",
    ...
    "lat": 56.312383
  }
];
```

Now you can open web page`[THIS_REPO]/src/test/tools/track.html` and see the track.

# How to download tariff

You should use following console command:

`tariff`

### Arguments:

    -server <production/testing>
    -tariff_id <tariff id>
    -path <absolute/directory/path>

### Sample:

`java -jar calc-utils-0.1.1.jar tariff -tariff_id 63a246ef130a1237e2c4ef5b976a805f0 -server testing -path sub_dir`

This sample downloads track with id `63a246ef130a1237e2c4ef5b976a805f0`
from testing server into `sub_dir` directory.

# How to download areas

You should use following console command:

`areas`

### Arguments:

    -server <production/testing>
    -area_ids <area id>,<area id>,<area id>...
    -path <absolute/directory/path>

### Sample:

`java -jar calc-utils-0.1.1.jar areas -area_ids 7c64e39b00c241a5ae015ce07bccdd79,0d92c61fbeaf44f9b71e978ca75e0a4d,bca9b71aa10f4a5cb3fed9f2a24a8dd1 -server testing -path sub_dir`

This sample downloads track with id's
`7c64e39b00c241a5ae015ce07bccdd79`,
`0d92c61fbeaf44f9b71e978ca75e0a4d` and
`bca9b71aa10f4a5cb3fed9f2a24a8dd1`
from testing server into `/sub_dir` directory.
