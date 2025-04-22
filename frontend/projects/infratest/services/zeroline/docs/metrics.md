# Сигналы и метрики

Задачи trendbox-ci и sandbox-ci (включая SANDBOX_CI_MERGE_QUEUE) при завершении отправляют:
- сигналы в YASM о статусе завершения задачи;
- хуки в zeroline-ручку `/api/v1/report-task-status`.

В свою очередь ручка `report-task-status` наливает данные:

- в [Clickhouse](https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-clickhouse/cluster/mdb93hb3hj9nthd6mme3) в таблицу [stats.task_statuses](https://yql.yandex-team.ru/Operations/YEDLjtK3DI_DLknI35ww1E_5M6X53PihNK7QUKn6Dy0=) информацию о том, задача какого типа, в каком проекте и контексте и с каким статусом завершилась;
- в Clickhouse в таблицу [stats.task_resolutions](https://yql.yandex-team.ru/Operations/YEDMKwPTTsvp9B2mNY3hv2h4FmTAxcSIDgTHJ6YUp6g=) информацию о том, какие проблемы найдены в каждой задаче — если нашлось несколько проблем, они все будут добавлены в базу;
- в YASM сигналы о том, какие проблемы найдены в каждой задаче.

## Infra Fail Rate

По данным из таблиц в Clickhouse строятся метрики [Infra Fail Rate](https://datalens.yandex-team.ru/aclfv98lnuo25-infra-fr-dashboard) (код лежит в [charts/arcadia-frontend-infra/infra-fr](../../charts/arcadia-frontend-infra/infra-fr)).

Так, для каждого проекта и контекста можно узнать:

- какая доля сборок (билдов) завершается неуспешно (Infra Fail Rate, %);
- задачи какого типа наиболее нестабильные (Fail Rate по типам задач, %);
- какие причины падения задач (Found Problems).

Поверх табличек можно писать любые аналитические запросы, которые придут в голову, например «[а какие задачи сейчас генерят больше всего неизвестных проблем](https://yql.yandex-team.ru/Operations/YC-_x1J2-RfYnmGiBubpLU4F5tcDWI3g4hM9H8xtVWw=)».

## Сигналы в YASM

Можно настроить алерты на **падения задач для определенного контекста и проекта** ([график](https://yasm.yandex-team.ru/chart/signals=sum(0,push-status_timeout_mmmm,push-status_exception_mmmm,push-status_failure_mmmm);repo=git_github_yandex-team_ru_search-interfaces_frontend_git,arcadia__frontend;workflow_name=build;itype=trendboxci;hosts=ASANDBOX;ctype=prod/?range=604800000)):

```
signals=sum(0, push-status_timeout_mmmm, push-status_exception_mmmm, push-status_failure_mmmm);
repo=git_github_yandex-team_ru_search-interfaces_frontend_git, arcadia__frontend;
workflow_name=build;
itype=trendboxci;
hosts=ASANDBOX;
ctype=prod;
```

Такой график покажет количество задач в репозитории frontend (и в git, и в arc) в workflow build (во frontend так называется workflow для ревью-реквестов), упавших с failure, exception или timeout.

Можно только на определенный **тип задач** ([график](https://yasm.yandex-team.ru/chart/signals=sum(0,push-status_timeout_mmmm,push-status_exception_mmmm,push-status_failure_mmmm);repo=git_github_yandex-team_ru_search-interfaces_frontend_git,arcadia__frontend;workflow_name=build_master;job_name=Hermione__master;itype=trendboxci;hosts=ASANDBOX;ctype=prod/?range=604800000)):

```
signals=sum(0, push-status_timeout_mmmm, push-status_exception_mmmm, push-status_failure_mmmm);
repo=git_github_yandex-team_ru_search-interfaces_frontend_git, arcadia__frontend;
workflow_name=build_master;
job_name=Hermione__master;
itype=trendboxci;
hosts=ASANDBOX;
ctype=prod;
```

Вот пример для **sandbox-ci** ([график](https://yasm.yandex-team.ru/chart/signals=sum(0,push-status_timeout_mmmm,push-status_exception_mmmm,push-status_failure_mmmm);service_name=web4;build_context=dev;task_type=SANDBOX_CI_HERMIONE;itype=sandboxci;prj=sandboxci;hosts=ASANDBOX/?range=604800000)):

```
signals=sum(0, push-status_timeout_mmmm, push-status_exception_mmmm, push-status_failure_mmmm);
service_name=web4;
build_context=dev;
task_type=SANDBOX_CI_HERMIONE;
itype=sandboxci;
prj=sandboxci;
hosts=ASANDBOX;
```

А можно на определённый **тип проблем** ([график](https://yasm.yandex-team.ru/chart/signals=sum(0,unistat-frontend_release-packages_unknown-error_dmmm);build_context=merge;hosts=ASEARCH;itype=fei_zeroline/?range=604800000)):

```
signals=sum(0, unistat-frontend_release-packages_unknown-error_dmmm);
build_context=merge;
hosts=ASEARCH;
itype=fei_zeroline;
```

TODO: Ждём [релиза](https://bb.yandex-team.ru/projects/SEARCH_INFRA/repos/yasm/pull-requests/10512/overview), чтобы фильтровать по repo
