[Концепция агр. статусов](concept.md)<br />
[Код агр. статусов](howto-code.md)<br />
[Диагностика статуса объекта](howto-diagnose-status.md)<br />


# Эксплуатация


## Мониторинг { #monitoring }
В первую очередь проверить что работает [ESS](../ess/jeri.md)

Также можно смотреть на состояние топика со стороны логброкера.
Топик lb: [ess--aggregated-statuses_update-events](https://lb.yandex-team.ru/lbkx/accounts/direct/ess/aggregated-statuses_update-events?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1609042959847&metricsTo=1609129359848&sortOrder=%22default%22)

Затем через логвьювер оценить по бинлогам — нет ли какого-то всплеска записи в базу.
Советы:
- ограничить `source` проблемным шардом
- посмотреть по очереди несколько основных таблиц: `campaigns`, `banners`, `bids`, `phrases`, другие
- использовать группировку по методу
- сравнить статистику с предыдущими часами, днями

### Задержки вычисления статусов
[График в секундах](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.ess_processor=aggregated_statuses_updater&l.sensor=binlog_delay&l.shard=*&graph=auto&stack=false&l.env=production)

Задержка более чем в 300с по этому графику зажигает мониторинг. В среднем статусы пересчитывваются за несколько секунд (<10s).


### Количество событий для пересчета статусов
[График](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.ess_processor=aggregated_statuses_updater&l.sensor=logic_objects_count&l.shard=*&graph=auto&transform=differentiate&l.env=production)

Этот график чаще всего объясняет причину задержки. Частой причиной задержки может быть массовая архивация или разархивация больших кампаний, когда сотни тысяч ключевых фраз перезжают из bids в bids_arc и обратно. (Причину также можно искать по [binlog-ам](https://direct.yandex.ru/logviewer/short/Cd-3ulJd3gGtcm) и [объектам logicObject](https://direct.yandex.ru/logviewer/short/ugFwcMJ13gGtxX) в logviewer-е).


### Зависшие is_obsolete

[График количества подвисших is_obsolete](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs-push&service=push-monitoring&l.flow=AggregatedStatusesMonitorJob&l.sensor=*&l.host=CLUSTER&l.type=*&l.env=production&graph=auto)

При синхронных действиях пользователя влияющих на статус (массовых операция по запуску/остановке), необходимо сразу отобразить, что статус изменился, при этом пересчитать статус синхронно мы не можем. В такой ситуации в БД на статусе устанавливается флажок is_obsolete, и пока он выставлен статус отображается как "Обрабатывается".

Иногда такие объекты зависают и не пересчитываются. Для отслеживания таких ситуаций служит этот график, на нем видно количетсво is_obsolete статусов по типу объекта а также записи которые не были пересчитаны за определенный промежуток времени (суфикс `_old`) — подвисшие.


### Упавшие чанки
[график failed_chunks](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.sensor=aggregated_statuses_failed_chunks&graph=auto&l.host=CLUSTER&l.ess_processor=aggregated_statuses_updater&l.shard=*&l.env=production)

Статусы для объектов пересчитываются пачками, если в процессе происходит exception, то падает пересчет всей пачки. Об этом этот график. Такие ситуация надо отслеживать и пересчитывать статусы для пострадавших объектов, а также исправлять причину падения.

Падают например из-за deadlock-ов в БД. Наблюдать можно так: [job logs logviewer link (deadlocks and other errors)](https://direct.yandex.ru/logviewer/short/aBG-WJZw3feaYN)



## Пересчет статусов


### Пересчет по списку CampaignId
Кампанию и все ее подобъекты можно пересчитать во внутреннем инструменте:

[внутренний отчет recompute_aggr_statuses](https://direct.yandex.ru/internal_tools/#recompute_aggr_statuses)

Указав id, кампаний через запятую. Будут пересчитаны все объекты внутри указанных кампаний и сами кампании.


### Полный пересчет БД
После изменений логики расчета статусов и/или исправаления багов (а иногда и просто раз в какой-то промежуток времени), статусы стоит пересчитывать полностью, для этого есть job-а. Т.к. статусы агрегируются снизу вверх, то сначала надо пересчитать фразы и объявления, потом группы, потом кампании, т.е. job-у надо с разными настройками запускать 3 раза. Полный пересчет занимает примерно неделю, дольше всего пересчитывается нижний слой (ключевые фразы и объявления).

Ссылка на внутренний инструмент для запуска job-ы: [manage_recalculate_campaigns_status_job](https://direct.yandex.ru/internal_tools/#manage_recalculate_campaigns_status_job)

