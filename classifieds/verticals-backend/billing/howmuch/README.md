# Howmuch

howmuch (a.k.a. price service) - сервис, аудируемо хранящий цены на продукты наших классифайдов.

Аудируемость в контексте howmuch означает, что хранится полная история изменения цен.

Является относительно простой обёрткой над ydb. Не ходит в другие сервисы, помимо S3 (см. ниже).

На данный момент в howmuch-api есть [две ручки](api/src/PriceService.scala):
1. Сохранение цен.
2. Получение сохранённых цен.

Эти ручки ходят только в ydb.

Основная сложность в этих ручках -- валидация запросов, в том числе относительно данных в базе, для обеспечения консистентности данных.

Также, в howmuch-scheduler есть [переливка](scheduler/src/DefaultS3UploadTask.scala) всех актуальных ценовых правил в бакеты в S3.
Каждая матрица переливается в отдельный бакет.

Подробно о дизайне сервиса, в том числе об используемой терминологии, можно прочитать в [дизайн-доке](design.md).

## Запуск тестов

`bazel test //billing/howmuch/...:all`

Про запуск конкретного теста см. в [readme](/README.md#как-запустить-именно-свой-тест).

## Релизы

Описание релизного процесса написано [здесь](/docs/how-to/deploy.md).

## SOX

За базу ydb отвечают админы, т.к. база под SOX. Следовательно, при проблемах с ресурсами базы нужно писать админам.
Но вообще, они [замониторили](https://st.yandex-team.ru/VERTISADMIN-26487) ресурсы, так что скорее всего, отреагируют раньше нас.

Доступа в базу у нас нет, можно заказать через тикет админам в очередь VASUP.

## Production metrics

- [grpc server](https://grafana.vertis.yandex-team.ru/d/grpc/grpc-server?var-job=howmuch-api)
- [Выгрузка матриц в S3](https://grafana.vertis.yandex-team.ru/d/lFeVlYeMk/howmuch-alerts?viewPanel=17)
- [ydb в yandex monitoring](https://monitoring.yandex-team.ru/projects/kikimr/dashboards/mon2uj4bpehmu39jn18t?p.cluster=ydb_ru&p.service=kqp&p.host=cluster&p.slot=static&p.database=%2Fru%2Fverticals%2Fproduction%2Fhowmuch)
- [ydb в старом UI](https://ydb.yandex-team.ru/db/ydb-ru/verticals/production/howmuch/metrics)

## Production alerts
- [alerts dashboard](https://grafana.vertis.yandex-team.ru/d/lFeVlYeMk/howmuch-alerts?orgId=1)

## Sentry

- [api test](https://sentry.vertis.yandex.net/verticals/howmuch-api/?query=environment%3A%22test%22)
- [api prod](https://sentry.vertis.yandex.net/verticals/howmuch-api/?query=environment%3A%22prod%22)
- [scheduler test](https://sentry.vertis.yandex.net/verticals/howmuch-scheduler/?query=environment%3A%22test%22)
- [scheduler prod](https://sentry.vertis.yandex.net/verticals/howmuch-scheduler/?query=environment%3A%22prod%22)

## Debug
- [Jaeger prod](https://jaeger.vertis.yandex.net/search?service=howmuch-api)
- [Jaeger test](https://jaeger.test.vertis.yandex.net/search?service=howmuch-api)
- [Выгрузка production базы howmuch в yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/export/ydb/howmuch) (может отставать на сутки)
- [api logs prod](https://nda.ya.ru/t/6JLRM12W4JyYEK)
- [scheduler logs prod](https://nda.ya.ru/t/TMBA9F-J4JyYLy)
- [api logs test](https://nda.ya.ru/t/PUaU3iSQ4JyYQD)
- [scheduler logs test](https://nda.ya.ru/t/ZqjVkF4k4JyYMa)
- [База ydb в тестинге](https://ydb.yandex-team.ru/db/ydb-ru-prestable/verticals/testing/common/browser/billing/howmuch)
