## rtmr_utils.create_checks

```python
from crypta.lib.python.data_size import DataSize
from crypta.lib.python.spine import rtmr_utils
from crypta.lib.python.spine.juggler import juggler_check_generator


# Requires JugglerCheckGenerator
juggler = juggler_check_generator.CryptaYtCheckGenerator(tags=["crypta-rt-task"])

# Create set of checks for RTMR task
rtmr_utils.create_checks(
    juggler,
    task_name="task",
    project_id="project",
    solomon_service="processing",
    output_operations=[
        rtmr_utils.OutputOperationConfig("pqout_operation", escalation=True),
    ],
    processing_operations=[
        rtmr_utils.ProcessingOperationConfig("processing_op", error_threshold=0, fail_threshold=500),
    ],
    operations_for_total_delivery_time=[
        rtmr_utils.OperationForTotalDeliveryTimeConfig("processing_op", threshold_seconds=rtmr_utils.TotalDeliveryTime.SECONDS_60),
    ],
    resources=[
        "resource/my_resource",
    ],
    tracked_state_sizes=[
        rtmr_utils.StateSizeConfig("processing_op", threshold=DataSize(gb=1)),
    ],
    tracked_table_sizes=[
        rtmr_utils.TableSizeConfig("task/table", threshold=DataSize(gb=3)),
    ],
)
```
