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
```bash
$ sudo docker build -t "goals_aggregation" .
$ sudo docker run -d -p 33502:80 --name=goals_aggregation goals_aggregation
### or ( with space before command to hide token from bash history )
$ sudo ./redeploy_service.sh "${GOALS_TOKEN}"
```
