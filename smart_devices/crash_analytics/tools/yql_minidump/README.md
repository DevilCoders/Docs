# yql-minidump

Downloads and decodes minidumps from production environment.

**Works in Linux environment only**

## Usage

First need to provide token as the environment variable

```
export YQL_TOKEN=[your token]
```

```
./yql_minidump [flags] [output_dir] [start_datetime] [end_datetime] [stackwalk_policy]
```

It'll take all minidumps in range of `[start_datetime...end_datetime]` and store in `output_dir`.
Minidumps can be filtered by device model, FW version, device ID etc (see `./yql_minidump -h`).
You can apply stackwalk to minidumps by `stackwalk_policy` (see `./yql_minidump -h`).

There can be 2 datetime formats used: YYYY-MM-DD and YYYY-MM-DDThh-mm-ss (there's just T letter between date and time).

### Examples

With YYYY-MM-DD format, filtering by service and version and stackwalking all.
```
./yql_minidump --service mediad --version 1.60.4.26.936156574.20210402 ./minidumps 2021-04-11 2021-04-12 all
```

With YYYY-MM-DDThh-mm-ss format, filtering by model and without stackwalking.
```
./yql_minidump --model yandexmini ./minidumps 2021-04-12T04:00:00 2021-04-12T05:00:00 none
```
