Command for build task binary and upload it as resource with required attributes:

`ya make --dist -E && ./backup upload --attr task_type=JUPYTER_CLOUD_BACKUP`

Version for local sandbox:

`ya make --dist -E && ./backup upload --attr task_type=JUPYTER_CLOUD_BACKUP --no-auth --skynet --url "http://localhost:13337"`

Instantly create task with dev-version of task binary:

`ya make --dist -E && ./backup run --create-only --type JUPYTER_CLOUD_BACKUP`
