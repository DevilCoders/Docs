# Emon

emon (**e**vent **mon**etization) -- сервис монетизации событий, таких, как звонки, чаты, клики, ...

Эти события формируются не самим пользователем сервиса, а кем-то другим.
Т.е. речь не про покупки услуг (например, поднятия) самим пользователем, а про совершение действий с объектами пользователя (обычно объявлениями).

У этих событий есть нюанс с точки зрения монетизации: контекст этих событий может меняться неограниченное число раз.
Например: за звонок деньги могут быть списаны, затем прийти модерация и признать звонок спам-звонком, затем ещё раз прийти модерация и сказать, что за звонок всё же надо списать деньги, и т.д.

Поэтому события для обилливания обогащаются, причём могут обогащаться много раз.
То, чем они обогащаются, называется факторами.
И события, и факторы emon принимает от других сервисов через очереди.

Разные факторы для одного события могут поставлять разные поставщики факторов.
Например, фактор про модерацию поставляет один сервис, фактор про матчинг звонка на колл-центр поставляет другой сервис, и т.д.
Поэтому нужно мержить факторы, что делается в [SimpleProtoMerger](./consumer/src/SimpleProtoMerger.scala).

Событие, обогащённое факторами, называется снапшотом.
Снапшоты события упорядочены по snapshot_id.

Типичный пример:
- сначала решили, что надо обилливать событие,
- а потом пришла модерация и сказала, что не надо,
- а потом она опять пришла и сказала, что всё-таки надо.

Тогда что лежит в разных снапшотах:
- snapshotId = 0 -- отсутствие модерации.
- snapshotId = 1 -- резолюция модерации о бесплатности звонка.
- snapshotId = 2 -- резолюция модерации о платности звонка.

Подробно о дизайне сервиса, в том числе об используемой терминологии, можно прочитать в [дизайн-доке](design.md).

## Запуск тестов

`bazel test //billing/emon/...:all`

Про запуск конкретного теста см. в [readme](/README.md#как-запустить-именно-свой-тест).

## Релизы

Описание релизного процесса написано [здесь](/docs/how-to/deploy.md).

## SOX

За базу ydb отвечают админы, т.к. база под SOX. Следовательно, при проблемах с ресурсами базы нужно писать админам.
Но вообще, они [замониторили](https://st.yandex-team.ru/VERTISADMIN-26487) ресурсы, так что скорее всего, отреагируют раньше нас.

Доступа в базу у нас нет, можно заказать через тикет админам в очередь VASUP.

## Production metrics

- [emon-consumer](https://grafana.vertis.yandex-team.ru/d/AKvNeiZ7z/emon-consumer)
- [emon-scheduler](https://grafana.vertis.yandex-team.ru/d/IOluJMW7z/emon-scheduler)
- [ydb в yandex monitoring](https://monitoring.yandex-team.ru/projects/kikimr/dashboards/mon2uj4bpehmu39jn18t?p.cluster=ydb_ru&p.service=kqp&p.host=cluster&p.slot=static&p.database=%2Fru%2Fverticals%2Fproduction%2Femon)
- [ydb в старом UI](https://ydb.yandex-team.ru/db/ydb-ru/verticals/production/emon/metrics)

## Production alerts

- [alerts dashboard](https://grafana.vertis.yandex-team.ru/d/zDj5TgD7z/emon-alerts)

## Sentry

- [consumer test](https://sentry.vertis.yandex.net/verticals/emon-consumer/?query=environment%3A%22test%22)
- [consumer prod](https://sentry.vertis.yandex.net/verticals/emon-consumer/?query=environment%3A%22prod%22)
- [scheduler test](https://sentry.vertis.yandex.net/verticals/emon-scheduler/?query=environment%3A%22test%22)
- [scheduler prod](https://sentry.vertis.yandex.net/verticals/emon-scheduler/?query=environment%3A%22prod%22)

## Debug

- [consumer logs prod](https://nda.ya.ru/t/Axo-hoxY4JyYmn)
- [scheduler logs prod](https://nda.ya.ru/t/T5X5f-AK4JyYpK)
- [consumer logs test](https://nda.ya.ru/t/je9_tSRC4JyZ2C)
- [scheduler logs test](https://nda.ya.ru/t/gy9gqZ6q4JyYwv)
- [База ydb в тестинге](https://ydb.yandex-team.ru/db/ydb-ru-prestable/verticals/testing/common/browser/billing/emon)
