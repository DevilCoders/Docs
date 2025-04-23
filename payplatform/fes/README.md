# Сервис фискализации платежных событий
- [Дизайн-страничка](https://wiki.yandex-team.ru/spirit/fiscal_event_service/design/)
- [ABC](https://abc.yandex-team.ru/services/fes/)
- [Deploy](https://deploy.yandex-team.ru/projects/FES)
- [CI](https://a.yandex-team.ru/projects/fes/ci/releases/timeline?dir=payplatform%2Ffes%2Ffes&id=fes-api-release)

## Observability
### Графики
0. [Метрики приложения](https://monitoring.yandex-team.ru/projects/trust_cashregisters/explorer/queries?q.0.s=%7Bproject%3D%22trust_cashregisters%22%2C%20cluster%3D%22fes_testing%22%2C%20service%3D%22fes_api%22%7D&utm_source=solomon_shard_graphs&from=1652891302332&to=1652893138947&refresh=off&normz=off&colors=auto&type=auto&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg) в Соломоне:
    * Общее: `build` (сборка), `duration` (тайминги), `count` (rps в разерезе по кодам ответа, ручкам);
    * GC (`go.gc.<...>`): количество вызовов, время последнего, длительность пауз, ...;
    * Memory (`go.mem.<...>`): колличество аллокаций, характеристики кучи, стека, ...;
    * Process (`proc.<...>`): CPU, IO, memory, ...;
    * Logger (`logger.<...>`): количество выброшенных записей и количество ошибок записи;
    * Concurrency (`go.goroutine.num` и `go.thread.num`): количество потоков и горутин;
    * YDB Driver: количество и lattency вызовов, коннекшены и сессии, ... (Модуль сбора метрик в драйвере [тут](https://a.yandex-team.ru/arcadia/library/go/yandex/ydb/metrics));
    * Tracing (`tracing.reporter.<...>`): длина очереди, количество успешных/неуспешных отправок спанов;
1. [Deploy](https://yasm.yandex-team.ru/template/panel/New-Porto-Container/deploy_unit=fes-api;geo=vla|sas;itype=deploy;stage=fes-production)
2. YDB:
    * [Основной дашборд](https://monitoring.yandex-team.ru/projects/kikimr/dashboards/monllvavev47fqmirf72?p.cluster=ydb_ru&p.service=utils&p.host=cluster&p.slot=static&p.database=%2Fru%2Ffes%2Fproduction%2F%2A&range=10m&refresh=60)
    * [Более подробный дашборд](https://monitoring.yandex-team.ru/projects/kikimr/dashboards/monjsbfduhubu5boup12/view?p.cluster=ydb_ru&p.database=%2Fru%2Fspirit%2Fproduction%2F%2A&refresh=60&range=1h)
    * Также есть [системные таблички](https://cloud.yandex.ru/docs/ydb/troubleshooting/system_views_cluster) со статистикой выполнения запросов.

### Алерты
Заданы кодом в `payplatform/spirit`.
* На API: `.../graphs_alerts_helpers/alerts/fes.py`
* На YDB:
  * Изменить/добавить/удалить алерты: `.../graphs_alerts_helpers/alerts/ydb.py`,
  * Добавить ещё одну базу: см. YDB_DATABASES в `.../graphs_alerts_helpers/constants.py`.

## SQS
[Заведены](https://st.yandex-team.ru/SQSREQUESTS-140) аккаунты `fes`, `fes-test`, `fes-dev`. На первые два настроены прод и тестинг соответственно, дев-аккаунт можно использовать для разработки/экспериментов.

Авторизация на данный момент через `OAuth`. Токены выписаны для роботов @robot-fes-test и @robot-fes для тестинга и прода соответственно. С авторизацией через TVM не всё гладко, пока заведена задачка на будующее: [SPIRIT-2688](https://st.yandex-team.ru/SPIRIT-2688)

ACL настраивается с помощью AWS CLI, подробности есть в документации по SQS: https://wiki.yandex-team.ru/sqs/

## YDB

Все базы доступны на `https://yc.yandex-team.ru` в каталоге [fes](https://yc.yandex-team.ru/folders/akuki83gm1s1vjrgh6oj/ydb/databases).

При необходимости можно также заводить тестовые YDB-базы в `ydb-home` на https://yc.yandex-team.ru/

Файлы, связанные с БД лежат в папке `ydb` соответствующего сервиса.

### Миграции

Все миграции лежат в папке `ydb/migrations` соответствующего сервиса.

#### Подготовка
1. Убедиться, что используем аркадийный [go](https://docs.yandex-team.ru/arcadia-golang/getting-started)
2. Выгрузить ветку [golang-migrate for ydb](https://github.com/golang-migrate/migrate/pull/677).
    * [Вот тут](https://gist.github.com/piscisaureus/3342247) описано как счекаутиться на PR.
3. Собрать из выгруженной ветки утилиту
   `make build-cli`
4. Настроить параметры для нужного сервиса:
   ```bash
   MIGR_FOLDER="path/to/migrations/folder"
   YDB_TOKEN="$(cat path/to/file/with/token)"  # (токен можно взять [здесь](https://yql.yandex-team.ru/oauth)
   YDB_ENDPOINT="..." # YDB эндпоинт из описания БД в UI YDB, пример для тестинга YDB_ENDPOINT=ydb-ru-prestable.yandex.net:2135
   YDB_NAME="URL_ENCODED_DB_NAME" # на примере тестинг БД `fiscaldb`: YDB_NAME="$(python3 -c 'import sys, urllib.parse as ul;print(ul.quote_plus(sys.argv[1]))' /ru-prestable/fes/testing/fiscaldb)"
   ```

#### Создать новый файл для миграций (по сути создает два файла с правильным именованием, при желании можно создать руками)
  `./cli/build/migrate.linux-amd64 create -ext sql -dir ${MIGR_FOLDER} -seq MIGR_NAME` # MIGR_NAME -
  часть имени файла миграции с описанием сути миграции

#### Накатить все миграции
  `./cli/build/migrate.linux-amd64 -source file://${MIGR_FOLDER} -database "ydb://${YDB_ENDPOINT}?database=${YDB_NAME}&token=${YDB_TOKEN}" up`

#### Накатить первые 2 миграции
  `./cli/build/migrate.linux-amd64 -source file://${MIGR_FOLDER} -database "ydb://${YDB_ENDPOINT}?database=${YDB_NAME}&token=${YDB_TOKEN}" up 2`

#### Откатить последние 2 миграции
  `./cli/build/migrate.linux-amd64 -source file://${MIGR_FOLDER} -database "ydb://${YDB_ENDPOINT}?database=${YDB_NAME}&token=${YDB_TOKEN}" down 2`

#### Если операция миграции закончилась ошибкой
Если операция миграции закончилась ошибкой, перед повторным применением миграций необходимо убедиться, что
БД в корректном состоянии и подтвердить это состояние прямым указанием текущей версии (VERSION: int) миграции
`./cli/build/migrate.linux-amd64 -source file://${MIGR_FOLDER} -database "ydb://${YDB_ENDPOINT}?database=${YDB_NAME}&token=${YDB_TOKEN}" force VERSION`
Без явного выставления версии, команды будут возвращать ошибки вида `Dirty database version N. Fix and force version`

### Прочее

Ещё немного про автопартиционирование в YDB:
- [переписка с коллегами из YDB](https://ml.yandex-team.ru/thread/ydb/178173660257846018/#message178173660257846018)
- [микроэксперимент](https://st.yandex-team.ru/SPIRIT-2432#61e138d32bc98e09aa6f8d60)
