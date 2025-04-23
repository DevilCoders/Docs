## Event processing alerts
Generate alerts for metrics produced by [event_processing](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/lib/native/event_processing) library

```python
from crypta.lib.python.spine import event_processing_utils
from crypta.lib.python.spine.consts import environment
from crypta.lib.python.spine.juggler import juggler_check_generator
from crypta.lib.python.spine.solomon import solomon_check_generator

# Requires SolomonCheckGenerator
solomon = solomon_check_generator.DcSolomonCheckGenerator(
    juggler_check_generator.JugglerCheckGenerator(tags=["crypta-siberia"]),
    project="crypta_siberia",
    service="describer",
    cluster=environment.PRODUCTION,
    dc="sas",
)

# Alert when event_processing receives invalid events
event_processing_utils.get_invalid_events_check(solomon)

# Alert when event_processing receives events with unsupported types
event_processing_utils.get_unsupported_events_check(solomon)

# Alert when solomon metric is greater then 0
event_processing_utils.get_zero_threshold_check(
    solomon_sensor=solomon.get_sensor("worker.describe_ids.batch.errors.empty_batch"),
    juggler_description="empty batches: {{ pointValue }}",
)
```
