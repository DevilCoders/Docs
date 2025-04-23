# Suggest metrics

## How to run

```shell script
ya make . && ./metrics_builder \
  --yt-token $(cat ~/.yt/token) \
  --yql-token $(cat ~/.yql/token) \
  --tvm-client-secret {your-tvm-secret} \
  [--prepare]
  [--region-requests-table {path-to-region-requests-table}]\
  [--hotel-requests-table {path-to-hotel-requests-table}]
```

`--region-requests-table` and `--hotel-requests-table` are optional, but if both arguments are missing the result will be an empty table.

## Input tables structure

In this section schema is not necessary but this is a convenient way to describe table structure.

### Hotel requests table

```python
schema = [
    {"name": "hash", "type": "string"}, # Some unique string identifier (hash for example)
    {"name": "name", "type": "string"},  # Hotel query
    {"name": "count", "type": "int64"},  # Query count
    {"name": "permalink", "type": "int64"},  # Expected hotel permalink
]
```

### Region requests table

```python
schema = [
    {"name": "hash", "type": "string"}, # Some unique string identifier (hash for example)
    {"name": "name", "type": "string"},  # Region query
    {"name": "count", "type": "int64"},  # Query count
    {"name": "geoId", "type": "int64"},  # Expected region id
]
```

### Search requests table

```python
schema = [
    {"name": "hash", "type": "string"}, # Some unique string identifier (hash for example)
    {"name": "query", "type": "string"},  # Region query
    {"name": "count", "type": "int64"},  # Query count
]
```

Input tables can be generated on the fly with `--prepare` argument or be passed via `--region-requests-table`,
`--hotel-requests-table` and `--search-requests-table` arguments.
Note that these arguments are mutually exclusive.


## Output tables structure

### Result table
```python
schema = [
    {"name": "query", "type": "string"},  # user query
    {"name": "count", "type": "int64"},  # query count in bucket
    {"name": "queryType", "type": "string"},  # query type (hotel, region)
    {"name": "suggestType", "type": "string"},  # suggest type (geo, new)
    {"name": "recall", "type": "int64"},  # 'recall' metric value
    {"name": "show", "type": "int64"},  # 'show' metric value
    {"name": "savedLength", "type": "int64"},  # saved length, part of 'saved' metric
    {"name": "queryLength", "type": "int64"},  # query length, part of 'saved' metric
]
```


### Aggregate result table
```python
schema = [
    {"name": "timestamp", "type": "uint64"},  # program start timestamp
    {"name": "date", "type": "string"},  # program start date
    {"name": "queryType", "type": "string"},  # query type (hotel, region)
    {"name": "suggestType", "type": "string"}, # suggest type (geo, new)
    {"name": "weighted", "type": "boolean"},  # True if metrics calculated with weight
    {"name": "recall", "type": "double"},  # 'recall' metric value
    {"name": "show", "type": "double"},  # 'show' metric value
    {"name": "saved", "type": "double"}, # 'saved' metric value
]
```


## Testing vs production

To make requests to testing you must change tvm service id via parameter:

```shell script
--tvm-service-id 2002548
```

Production TVM service id is:

```shell script
--tvm-service-id 2002546
```

And this is default value of this parameter.

## Dev run

```shell script
ya make . && ./metrics_builder \
  --yt-token $(cat ~/.yt/token) \
  --yql-token $(cat ~/.yql/token) \
  --tvm-client-secret {secret} \
  --tvm-service-id 2002548 \
  --prepare \
  --days 3 \
  --limit 100 \
  --cleanup-strategy KeepLastN:3
```

### Production run

```shell script
ya make . && ./metrics_builder \
  --yt-token {yt-token-value} \
  --yql-token {yql-token-value} \
  --tvm-client-secret {tvm-client-secret} \
  --prepare \
  --target-folder //home/travel/prod/suggest/metrics \
  --suggest-aggregated-metrics-table //home/travel/prod/metrics/suggest-metrics-aggregated
```

## Autobuild

[TestEnv job](https://beta-testenv.yandex-team.ru/project/travel-trunk/job/TRAVEL_MAKE_HOTELS_SUGGEST_METRICS_BUILDER/history) is setted up via [code in arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/travel/TravelBuild.yaml?rev=6675389#L532) to autobuild [sandbox resource](https://sandbox.yandex-team.ru/resources?type=TRAVEL_HOTELS_SUGGEST_METRICS_BUILDER) [described in arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/Travel/resources/__init__.py?rev=6674379#L691).
