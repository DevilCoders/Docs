Build task binary and upload it as a new resource with required attributes:
```shell
ya make -r && ./salt upload --enable-taskbox --attr task_type=JUPYTER_CLOUD_SALT
```

Create task with dev-version of task binary:
```shell
ya make -r && ./salt run --create-only --enable-taskbox --attr task_type=JUPYTER_CLOUD_SALT
```

Instantly run a copy of another task with new binary:
```shell
ya make -r && ./salt run --tid 975505663 --enable-taskbox --attr task_type=JUPYTER_CLOUD_SALT
```
