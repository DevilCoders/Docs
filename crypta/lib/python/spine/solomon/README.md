## SolomonCheckGenerator

Create Solomon alerts connected to Juggler aggregate checks

```python
# Generate checks for solomon metrics sent by host in "stable_nanny_service_sas" Nanny service
solomon = DcSolomonCheckGenerator(
    JugglerCheckGenerator(
        child_group="stable_nanny_service_sas",
        child_group_type=consts.GroupType.nanny,
    ),
    # Select only metrics with these labels 
    project="project",  # Also store alerts in this project
    service="service",
    env="stable",
    dc="sas",
)

# Alert when maximum of (sensor="errors") metric over a 5 minute period rises above 0
# Argument of get_sensor is used as a "sensor" label and as Juggler service
# "host" label is used as Juggler host
# Solomon project must have a configured juggler channel, for example see https://solomon.yandex-team.ru/admin/projects/crypta_audience/channels/crypta-juggler 
solomon.get_sensor("errors").create_threshold_check(
    aggregation=alert_pb2.MAX,
    predicate=alert_pb2.GT,
    threshold=0,
    period=timedelta(minutes=5),
    description="errors: {{ pointValue }}",
# Do not alert when metric is missing
).add_nodata_mode(consts.NoDataMode.force_ok)

# Alert when number of 5** codes exceed 600 over a 2 minute period
# This alert uses solomon expressions, because many possible sensors need to be aggregated for each host 
solomon.create_sensor_aggregation_check_by_host(
    service="5XX_codes",
    period=timedelta(minutes=2),
    sensor_glob="*.request.http_code.5??",
    predicate=alert_pb2.GT,
    threshold=600,
    description="Total 5XX codes : {{expression.total}} > {{expression.threshold}}",
).add_nodata_mode(consts.NoDataMode.force_ok)

# Alert when rate of uploads with zero retries falls below 90% over a 5 minute period
solomon.create_hist_check(
    service="upload_retries",
    period=timedelta(minutes=5),
    labels_bins="uploader.upload.retries.b0",
    # Sensor glob that includes all of the labels belonging to this histogram 
    labels_all="uploader.upload.retries.*",
    threshold=0.9,
    predicate=alert_pb2.LT,
    description="Uploaded with zero retries : {{expression.percentile}} < {{expression.threshold}}",
)

# Create any solomon expression alert
solomon.create_expression_alert_check(
    service="hahn.crypta-graph",
    period=timedelta(minutes=5),
    program="""
    let Used = avg({{
        project="yt", cluster="hahn", service="accounts",
        account="crypta-graph", sensor="disk_space_in_gb", medium="default"
    }});
    let Limit = avg({{
        project="yt", cluster="hahn", service="accounts",
        account="crypta-graph", sensor="disk_space_limit_in_gb", medium="default"
    }});
    let QuotaUsage = (Used/Limit);
    let QuotaUsagePretty = to_fixed(QuotaUsage * 100.0, 2);

    let UsedQuota = to_fixed(Used / 1024.0, 2);
    let LimitQuota = to_fixed(Limit / 1024.0, 2);

    let ThresholdSoft = 0.93;
    let ThresholdHard = 0.95;
    let Account = "crypta-graph";
    let Host = "hahn";

    alarm_if(QuotaUsage >= ThresholdHard);
    warn_if(QuotaUsage >= ThresholdSoft);
    """,
    description="""
    {{^is_ok}}
    Please kindly check {{expression.Account}} on {{expression.Host}}:
        quota used {{expression.QuotaUsagePretty}}%
        {{expression.UsedQuota}} Tb out of {{expression.LimitQuota}} Tb
    {{/is_ok}}
    """,
)

# Alert when real lag exceeds 100K messages, averaged over 5 minute period
solomon.create_logbroker_lag_check(
    consumer="crypta/prod/cm/consumer",
    topic="crypta/prod/cm/change-log",
    threshold=10**5,
    period=timedelta(minutes=5),
)

# Generate checks for solomon metrics not bound to a host group
solomon = SolomonCheckGenerator(
    JugglerCheckGenerator(
        host="crypta-audience",
        child_group_type=consts.GroupType.host,
        child_group="crypta-audience-solomon",
    ),
    AlertCreator(
        project_id="crypta_audience",
        selectors={"project": "crypta_audience", "cluster": "production"},
    ),
)

# Alert when input size exceeds 25k
# You can pass a dict of labels if "sensor" label is not enough to describe the full metric
solomon.get_sensor({"sensor": "input_size", "service": "metrics_audience"}).create_threshold_check(
    aggregation=alert_pb2.MAX,
    predicate=alert_pb2.GT,
    threshold=25000,
    period=timedelta(minutes=5),
    juggler_service="CryptaAudience_queues_regular_input",
    description="Input size (regular): {{ pointValue }}",
)
```
