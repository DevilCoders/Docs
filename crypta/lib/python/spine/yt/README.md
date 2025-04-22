## Yt*Metric
```python
import datetime

from crypta.lib.python.spine.consts.yt_proxy import YtProxy
from crypta.lib.python.data_size import DataSize
from crypta.lib.python.solomon.proto import alert_pb2
from crypta.lib.python.spine.consts import environment
from crypta.lib.python.spine.juggler import (
    juggler_check_generator,
)
from crypta.lib.python.spine.yt import yt_config_registry
from crypta.lib.python.spine.yt.yt_latency_metric import YtLatencyMetric
from crypta.lib.python.spine.yt.yt_processed_tables_metric import YtProcessedTablesMetric
from crypta.lib.python.spine.yt.yt_size_metric import YtSizeMetric    


# All generators require juggler check generator
juggler = juggler_check_generator.CryptaYtCheckGenerator(
    host="crypta-audience",
    tags=["crypta-audience"],
)

# Yt*Metric classes require YtConfigRegistry which has information about root paths for specific environments
# CryptaYtConfigRegistry has predefined roots for crypta/* projects 
yt_registry = yt_config_registry.CryptaYtConfigRegistry(juggler)

# Creating Yt*Metric object adds metrics for YT paths to solomon
# add_*_alert methods create Solomon alerts and Juggler checks for these metrics
# add_*_alert methods return an instance of JugglerAggregateCheck which can be modified further

# Alert when oldest table in the directory "//{{env_dependent_root}}/relative/directory/path" is at least an hour old
# Ignores any non-table nodes in the directory 
YtLatencyMetric(yt_registry, "relative/directory/path").add_table_latency_alert(
    threshold=datetime.timedelta(hours=1),
)

# Alert when oldest node in directory is at least 4 hours old
# Takes into account nodes of all types
YtLatencyMetric(yt_registry, "relative/directory/path").add_latency_alert(
    threshold=datetime.timedelta(hours=4),
)

# Alert when the node is at least an hour old
YtLatencyMetric(yt_registry, "node").add_age_alert(
    threshold=datetime.timedelta(hours=1),
)

# Add metrics for a special table which tracks processed log tables
dump_processed = YtProcessedTablesMetric(yt_registry, "is/dump/.processed")
for host, env in [
    ("test.host", environment.TESTING),
    ("prod.host", environment.PRODUCTION),
]:
    # Alert when last entry in the table is 4 hours old, aggregate in different hosts depending on environment
    dump_processed.add_lag_alert(
        threshold=datetime.timedelta(hours=4),
        env=env,
    ).set_host(host)

# Alert when node's disk space is greater than 1 Gb
YtSizeMetric(yt_registry, "errors").add_disk_space_alert(
    predicate=alert_pb2.GT,
    threshold=DataSize(gb=1),
)

# Alert when chunk count is greater than 3 million 
YtSizeMetric(yt_registry, "errors").add_chunk_count_alert(
    predicate=alert_pb2.GT,
    threshold=3e+6,
)

# Alert when node count is greater than 100 
YtSizeMetric(yt_registry, "errors").add_node_count_alert(
    predicate=alert_pb2.GT,
    threshold=100,
)

# Alert when row count in dynamic table on seneca-sas falls below 1 billion 
YtSizeMetric(yt_registry, "cookie_matching/rt/db/replica", yt_proxy=YtProxy.seneca_sas).add_unmerged_row_counts_alert(
    predicate=alert_pb2.LT,
    threshold=1e9,
)

# Alert when row count in static table falls below 300 million 
YtSizeMetric(yt_registry, "lab/data/UserData").add_row_count_alert(
    predicate=alert_pb2.LT,
    threshold=3e8,
)

# Just add metrics without adding alerts
YtSizeMetric(yt_registry, "lab/data/UserData")
```

## ReplicatedTableConfigRegistry
```python
# ReplicatedTableConfigRegistry checks replicated_table and its replicas statuses and attributes
master = Master(
    name="markov",
    proxy=YtProxy.markov,
    path="//full/master/path",
    expected_attributes={"tablet_cell_bundle": "crypta-cm"},
    replication_lag_threshold=60000,
    sync_count=1,
)

replicas = [
    Replica(
        name=proxy.split(".", 1)[0],
        proxy=proxy,
        path="//full/replica/path",
        expected_attributes={"tablet_cell_bundle": "crypta-cm"},
    )
    for proxy in YtProxy.Group.dyntable_prod
]

ReplicatedTableConfigRegistry(juggler, ReplicatedTable(master, replicas))
```
