### Notice
Постарайтесь не ломать ничего в транке, на сервер изменения попадут в течении 5 минут автоматически.
Кроме коммита в аркадию для этого ничего делать не нужно.
Тесты перед деплоем НЕ прогоняются, поскольку на хосте не установлены зависимости (установлены только в контейнере).

### To Development:

```bash
$ ./app/run_tests.sh
$ export FLASK_DEBUG_ENABLED=1
$ ./app/run_app_local.sh
```
 or 
```bash
$ ./app/run_tests.sh
$ export FLASK_DEBUG_ENABLED=1
$ export GOALS_TOKEN="${GOALS_TOKEN}"
$ ./app/run_app_local.sh real
```

Run specific testcase:
```bash
$ ./app/run_tests.sh tests.test_data_storage.TestGoalsStorage.test_dump_global
### or
$ ./app/run_tests.sh tests.test_data_storage
```

### To Deploy
1. Commit your changes
2. Clone and run sandbox task with type BUILD_DOCKER_IMAGE_V6 and "goals_aggregation_production" description
https://sandbox.yandex-team.ru/tasks?type=BUILD_DOCKER_IMAGE_V6&desc_re=goals-aggregation-production
3. Update image in qloud
https://qloud.yandex-team.ru/projects/market-dev/goals-aggregation/production
