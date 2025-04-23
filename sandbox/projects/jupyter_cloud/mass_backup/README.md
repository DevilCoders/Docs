Command for build task binary and upload it as resource with required attributes:

`ya make --dist -E && ./mass_backup upload --attr task_type=JUPYTER_CLOUD_MASS_BACKUP`

Version for local sandbox:

`ya make --dist -E && ./mass_backup upload --attr task_type=JUPYTER_CLOUD_MASS_BACKUP --no-auth --skynet --url "http://localhost:13337"`

Instantly create task with dev-version of task binary:

`ya make --dist -E && ./mass_backup run --create-only --type JUPYTER_CLOUD_MASS_BACKUP`
