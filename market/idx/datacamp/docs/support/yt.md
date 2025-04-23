# Расследование проблем с YT

## Категории проблем с YT:
1. Проблемы с записью в таблицы vs проблемы с чтением из таблиц.
2. Проблемы с синхронной репликой vs проблемы с async репликой.

## Проблемы с записью в таблицы
1. Приложение не может записать данные в таблицу. Происходит потому, что кончилось место на ноде: ```Node is out of tablet memory, all writes disabled``` - cамая актуальная наша проблема.
Примеры:
   - https://st.yandex-team.ru/YTADMINREQ-27825

## Проблемы с чтением из таблиц
Идем в [YT Artemis[market-datacamp-production]](https://solomon.yandex-team.ru/?cluster=seneca-sas&project=yt&dashboard=yt_artemis_bundle_v2&l.tablet_cell_bundle=market-datacamp-production&b=1d&e=) и проверяем, не замучили ли мы таблицу своими запросами.
Два способа задудосить таблицу:
1. Мы читаем слишком часто. Названия графиков на дашборде YT Artemis:
```
Table lookup row count rate
Table lookup request rate
Table select row count rate
Table select request rate
```
2. Мы читаем слишком много. ЫТю не хватает кэша для ответов на запросы, он начинает поднимать данные с дисков, увеличиваются использование диска, нагрузка на ЦПУ, время ответа на запрос. Названия графиков на дашборде YT Artemis:
```
Table lookup data weight rate
Table lookup data bytes read from disk
Table lookup cpu time rate
Table select data weight rate
Table select data bytes read from disk
Table select cpu time rate
```

## Проблемы с синхронной репликой
1. Растут очереди в логброкере. Общий дашборд очередей Pipep LB есть в разделе [Графики и метрики Дежурному Piper](https://docs.yandex-team.ru/market-datacamp/support/metrics#piper):
   1. [Piper LB length MessageLagByCommited](https://solomon.yandex-team.ru/?project=market.datacamp&sensor=MessageLagByCommitted&dashboard=datacamp_piper_production) (что такое [MessageLagByCommitted](https://logbroker.yandex-team.ru/docs/reference/metrics?#MessageLagByCommitted))
   2. [Piper Commit lag CreateTimeLagMsByCommitted](https://solomon.yandex-team.ru/?project=market.datacamp&sensor=CreateTimeLagMsByCommitted&dashboard=datacamp_piper_production) (что такое [CreateTimeLagMsByCommitted](https://logbroker.yandex-team.ru/docs/reference/metrics?#CreateTimeLagMsByCommitted))
2. Растет количество коллизий и количество офферов, отправленных в [ретрай топик](https://fcs.yandex-team.ru/#!TOPIC.*%3D.*retry,market%2Fidx%2Fdatacamp.*,jCm,arcadia,%2Fut%2F,100) market-indexer/{**prod**|**testing**}/united/datacamp-offers-retry - он есть на дашборде лагов логброкера в пайпер.

## Проблемы с асинхронной репликой
1. Растет лаг репликации. [График лага репликации Y.Monitoring](https://monitoring.yandex-team.ru/projects/datacamp/dashboards/mon3n1gu4hgd5poj3925?from=now-1d&to=now&refresh=60000). [Алерт на лаг репликации в Juggler](https://juggler.yandex-team.ru/project/market.datacamp/aggregate?host=market-yt-datacamp-production&service=datacamp_replication_lag&project=market.datacamp).

## Трассировки запросов в динтаблицы из контроллеров
Для запросов в динтаблицы из контроллеров и диспатчера можно включить [трассировку](https://yt.yandex-team.ru/docs/other/tracing#poisk-v-interfejse-jaeger):
```
TRACE_SAMPLING_PERCENT=100 # Процент семплирование запросов для трассировки, необходимо чтобы регулировать нагрузку на jaeger
ROOT_TRACING_SPAN_NAME='DatacampController' # любое непустое значение включает трассировку
```

После включения, в логах можно найти trace id для запросов, попавших в выборку:
```
INFO: 2022-07-07 19:31:32.009 +0300 datacamp_client.cpp:79 Request: UpdateOffers;  trace id: bcbff687-f93ab7f7-417c007d-72dfddd8
```
Трассировку по запросу смотреть в [jaeger](https://jaeger.yt.yandex-team.ru/yt/search).

Кроме того, можно искать трейсы по стандартным тегам yt:
```
   -- user - имя робота, от которого сделан запрос. Например robot-mrkt-dc-p-tst.
   -- yt.table_path	- имя таблицы.
```

