Command for build task binary and upload it as resource with required attributes:

`ya make --dist -E && ./arcadia_kernels upload --attr task_type=JUPYTER_ARCADIA_KERNELS`

Version for local sandbox:

`ya make --dist -E && ./arcadia_kernels upload --attr task_type=JUPYTER_ARCADIA_KERNELS --no-auth --skynet --url "http://localhost:13337"`

Instantly create task with dev-version of task binary:

`ya make --dist -E && ./arcadia_kernels run --create-only --type JUPYTER_ARCADIA_KERNELS`
