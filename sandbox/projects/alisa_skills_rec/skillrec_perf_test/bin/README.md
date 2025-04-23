## Upload binary task to production Sandbox
To release binary task you should use DEPLOY_BINARY_TASK task with inputs:
- target: sandbox/projects/alisa_skills_rec/skillrec_perf_test/bin/bin
- attrs: `released:stable`, `task_type:SKILL_REC_PERF_TEST`
- check_types: SKILL_REC_PERF_TEST
- yt_token_vault: <your yt token secret in https://sandbox.yandex-team.ru/admin/vault>
- release_ttl: inf
- binary_executor_release_type: stable

To upload binary task for testing:
```
$ ./bin upload --attr target=sandbox/projects/alisa_skills_rec/skillrec_perf_test/bin/bin --attr released=testing --attr task_type=SKILL_REC_PERF_TEST
```


## Upload binary task to local Sandbox
```
$ sandbox/sandbox upload_binary sandbox/projects/alisa_skills_rec/skillrec_perf_test/bin/bin --enable-taskbox --attr target=sandbox/projects/alisa_skills_rec/skillrec_perf_test/bin/bin --attr released=testing --attr task_type=SKILL_REC_PERF_TEST
```
