# Полезные графики


## YDB

### Общий дашборд базы

https://solomon.yandex-team.ru/?project=kikimr&service=kqp&cluster=ydb_ru&database=%2Fru%2Fverticals%2Fproduction%2Fgeneral&host=cluster&slot=cluster&dashboard=kikimr-mt-database-overall&b=1h&e=


### Range-запросы, число прочитанный байт.
Проверять что читаем не слишком много.

https://solomon.yandex-team.ru/?project=kikimr&cluster=ydb_ru&service=tablets&host=cluster&slot=cluster&database=/ru/verticals/production/general&sensor=DataShard%2FEngineHostRangeReadBytes&type=DataShard&graph=auto&downsamplingAggr=max&b=1d&e=


## Vasgen

### Индексация
https://grafana.vertis.yandex-team.ru/d/r4y5ngFMk/kafka?orgId=1

### Размер индекса saas 
https://yasm.yandex-team.ru/chart/signals=%7Bdm_dashboard-stable-vasgen_search_lb-min-replica-docs_txxv,dm_dashboard-stable-vasgen_search_lb-max-replica-docs_txxv%7D;hosts=ASEARCH;itype=deploymanager/

## Модерация

### Лаг консьюмеров
https://grafana.vertis.yandex-team.ru/d/8iBfJ77Wk/moderation?viewPanel=44&orgId=1&from=now-6h&to=now&var-datasource=Prometheus&var-dc=.*&var-module=moderation-.*&var-component=All&var-service=general&var-error=false&var-percentile=99&var-window=5m&var-job=bureau-user-offers-statistics-AUTORU-USERS_AUTORU&refresh=30s


## Telepony
###Доступные подменники
https://grafana.vertis.yandex-team.ru/d/Oz5gJhjiz/telepony-number-pool?orgId=1&from=now-7d&to=now&var-datasource=Prometheus&var-domain=ya_general&var-operator=All&var-phone_type=Mobile&var-geo_name=All&var-geo_id=All&var-status=All