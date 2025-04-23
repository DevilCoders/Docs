Сервис тасклетов
==

Дизайн дока: [wiki/design-review](https://wiki.yandex-team.ru/sandbox/tasklets/design-review/)

Докс: [docs/tasklets](https://docs.yandex-team.ru/tasklets/)

Runtime:
===
Тестинг: [https://deploy.yandex-team.ru/projects/Tasklets](https://deploy.yandex-team.ru/projects/Tasklets)


Developer notice
===

Локальный запуск
====

Сборка:

```shell
$ ya make cmd/server/
```

Конфиг:

1. Создаём `cmd/server/configs/${user}.yaml`
2. Заполняем `db.ydb.*`
3. Добавляем `${user}.yaml` в `cmd/server/configs/.arcignore`

Посмотреть конфиг можно так:

```shell
./cmd/server/tasklet-server config  -b devel -c cmd/server/configs/${user}.yaml
```

Базу данных можно получить двумя способами:

1.

Поднять [serverless ydb](https://ydb.yandex-team.ru/docs/getting_started/create_manage_database#create-db-via-ui-serverless)
в облаке `ydb_home`

2. Принести через docker: [doc](https://cloud.yandex.com/en/docs/ydb/solutions/ydb_docker)

Инициализация БД:

```shell
./cmd/server/tasklet-server -b devel -c ${user}.yaml storage init --purge
```

Запуск:

```shell
./cmd/server/tasklet-server -b devel -c ${user}.yaml  run
```

Конфигурация:

1. Дефолтные значения описаны в `server/configs/base.yaml`
2. Дефолтные конфиги лежат там же и бандлятся в бинарник
3. Есть возможность при старте передать оверрайды (для локального тестирования)

```shell
./cmd/server/tasklet-server  run -b devel -c "config_overrides.yaml"
```

Тестирование
====

Аркадия:

```shell
$ ya make -tt
```

Запуск в IDE:

Пока не работает. Нужно:

1. добавить docker-compose поднятия local ydb
2. поправить линковку с swagger схемой на go:embed

В качестве workaround можно в конфиге написать имеющуюся инсталляцию ydb

Тесты процессора: нужно написать mock для sandbox клиента



IDE
====

```shell
$  ./scripts/codegen.sh
$ ya ide goland ...
```

Protocol buffers
=====
Не забываем про педиодический автоформат кода. Используем [prototool](https://clubs.at.yandex-team.ru/arcadia/24169)

```shell
$ ~/go/bin/prototool format -w   # Форматирование
$ ~/go/bin/prototool valid  # Валидация
```

Тесты
====
Основа -- функциональные тесты в `/tests`


Логи
====

```shell
sky run --stream 'tail -F  /porto_log_files/api-server-workload_stderr.portolog | grep -v -e name=core.ydb_client -e "name=grpc " '  b@tasklets.tasklets-testing.api-server.api-server-box
```



