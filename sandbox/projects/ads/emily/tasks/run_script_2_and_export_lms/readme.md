This task extends RUN_SCRIPT_2. After the script is completed it searches for last resource
of type SANDBOX_TASKS_BINARY having attributes
```
attrs={
    "task_type": "EXPORT_LINEAR_MODEL_TABLES_TO_YT",
    "released": "stable"
}
```
and starts the export task.
To release new binary, just build it (you can use BUILD_SANDBOX_TASKS or ya) and set those attributes
