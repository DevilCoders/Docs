## Upload binary task to production Sandbox
To release binary task you should use DEPLOY_BINARY_TASK task with inputs:
- target: sandbox/projects/trust/tasks/StartTrustPerfTesting/bin/bin
- attrs: `released:stable`, `task_type:START_TRUST_PERF_TESTING`
- check_types: START_TRUST_PERF_TESTING
- yt_token_vault: <your yt token secret in https://sandbox.yandex-team.ru/admin/vault>
- release_ttl: inf
- binary_executor_release_type: stable

To upload binary task for testing:
```
$ ./bin upload --attr target=sandbox/projects/trust/tasks/StartTrustPerfTesting/bin/bin --attr released=testing --attr task_type=START_TRUST_PERF_TESTING
```


## Upload binary task to local Sandbox
```
$ sandbox/sandbox upload_binary sandbox/projects/trust/tasks/StartTrustPerfTesting/bin/bin --enable-taskbox --attr target=sandbox/projects/trust/tasks/StartTrustPerfTesting/bin/bin --attr released=testing --attr task_type=START_TRUST_PERF_TESTING
```
