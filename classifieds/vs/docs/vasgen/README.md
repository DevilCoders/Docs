### Searcher
#### Локальный запуск
Запускается средствами `IDEA` с установленным [аркадийным плагином](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij) и [ya tool](https://wiki.yandex-team.ru/yatool/distrib/).  
Конфигурация для запуска - `.run/searcher_general_test.run.xml` (если отсутствует, нужно перенести из `.run.template/searcher_general_test.run.xml.template`)  
Тестовый запрос:
```
grpcurl --plaintext -d '{"domain":{"id":"general"}, "query":{"plan":{"plan_id":"search"}, "text":{"query":"техника"}}}'  localhost:8080 vertis.vasgen.grpc.Search/Execute
```

### Saas-indexer

#### Артефакты индексирования

Артефакты индексирования описаны в документе [Индексирование](indexing.md)

#### Локальный запуск
Запускается средствами `IDEA` с установленным [аркадийным плагином](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij) и [ya tool](https://wiki.yandex-team.ru/yatool/distrib/).  
Конфигурация для запуска - `.run/SaasIndexerApp.run.xml

1. Удостовериться, что следующие env-переменные отличны от [тестинга](https://github.com/YandexClassifieds/services/blob/master/conf/vasgen-saas-indexer/test.yml):
- KAFKA_GROUP_ID

1. Удостовериться, что следующие env-переменные отличны от [тестинга](https://github.com/YandexClassifieds/services/blob/master/conf/vasgen-saas-indexer/test.yml) и [прода](https://github.com/YandexClassifieds/services/blob/master/conf/vasgen-saas-indexer/prod.yml):
- WORKER_LOCKER_WORKER_LOCK
- WORKER_LOCKER_SHARD_LOCK
- WORKER_LOCKER_STATUS_NODE
- WORKER_LOCKER_PATH_PREFIX

1. Запустить конфигурацию запуска.

### План деплоя на прод c новой эпохой (на примере general)

1. [General] Остановить наливку в _general-scheduler_
1. Ждем, пока все со старой эпохой долетит от general (см. [график](https://grafana.vertis.yandex-team.ru/d/r4y5ngFMk/kafka?viewPanel=34&orgId=1&refresh=1m&from=now-1h&to=now) и ждем провала до 0)
1. Останавливаем _консьюмер_.
   На графиках увеличится возраст сообщений в батчах, это в пределах нормы.
1. Заливаем новый _индексер_, _серчер_ тем временем летит на старой эпохе
1. [General] Поднять эпоху и включить наливку в general-scheduler
1. Запускаем _консьюмер_
1. Запускаем [переиндексацию](saas_indexer_api.md#reind-prod) с НОВОЙ эпохой, прогресс отслеживаем [тут, секция Reindexing](https://grafana.vertis.yandex-team.ru/d/R--dgDpMk/general-search-scheduler?orgId=1&refresh=1m&var-datasource=Prometheus)
   и [тут](https://grafana.vertis.yandex-team.ru/d/r4y5ngFMk/kafka?viewPanel=43&orgId=1&refresh=1m)

   **ER**: В [zk](indexing.md#zk-prod) наполняется маппинг для новой эпохи
1. Деплоим новый _серчер_
1. Переключаем эпоху на серчере: в ноде `/vasgen/saas/epoch/current` для атрибута `general` меняем значение на новую эпоху.
   Тайминги searcher могут подскочить, т.к. необходимо время для прогрева кэша.

   **Смок-тест searcher:**
    - фильтр на цену и любые атрибуты со значениями float и boolean
    - сортировка по цене
1. [Удаляем](saas_indexer_api.md#epoch-del) старую эпоху

### План деплоя на тестинг c новой эпохой (на примере general)

Для тестинга можно провести ту же процедуру, но т.к. downtime для него некритичен, а процедура длинная и требует содействия
двух сторон, то можно пренебречь и упростить процедуру:
1. Залить новый _индексер_
   При этом часть документов(если в консьюмер действительно что-то будет попадать) проиндексируется по-новому
1. [General] Поднять эпоху
1. Запускаем [переиндексацию](saas_indexer_api.md#reind-test) с НОВОЙ эпохой, прогресс отслеживаем [тут, секция Reindexing](https://grafana.vertis.yandex-team.ru/d/R--dgDpMk/general-search-scheduler?orgId=1&refresh=1m&var-datasource=Prometheus-testing)
   и [тут](https://grafana.vertis.yandex-team.ru/d/r4y5ngFMk/kafka?viewPanel=43&orgId=1&refresh=1m&var-Environment=Prometheus-testing&var-topic=vasgen-indexer&var-dc=myt&var-dc=sas&var-dc=man&var-dc=vla)

   **ER**: В [zk](indexing.md#zk-test) наполняется маппинг для новой эпохи
1. Далее как для прода с п.8


### Графики
1. [Production alert](https://grafana.vertis.yandex-team.ru/d/icXvOhfMk/production-alert?orgId=1)

1. [System Info - информация о контейнерах](https://grafana.vertis.yandex-team.ru/d/system-info/system-info?orgId=1&var-datasource=Prometheus&var-job=vasgen-saas-indexer&var-dc=All&var-window=2m&var-gc=All&refresh=30s)

1. [GRPC](https://grafana.vertis.yandex-team.ru/d/grpc/grpc-server?orgId=1&refresh=30s&var-datasource=Prometheus-testing&var-job=vasgen-searcher&var-dc=All&var-service=vertis.vasgen.grpc.Search&var-method=Execute&var-window=2m)

1. [Kafka related](https://grafana.vertis.yandex-team.ru/d/r4y5ngFMk/kafka?orgId=1&var-Environment=Prometheus&var-topic=auto-vasgen-indexer&var-dc=myt&var-dc=sas&var-dc=man&var-dc=vla)

1. [Searcher](https://grafana.vertis.yandex-team.ru/d/zGdQawhMk/searcher?orgId=1&var-Environment=Prometheus&var-dc=sas&var-dc=vla&var-plan=search)

1. [kafka clients](https://grafana.vertis.yandex-team.ru/d/k3s7s-cMk/kafka-clients?orgId=1&from=1618926907554&to=1618930507554&refresh=1m&var-datasource=Prometheus&var-job=vasgen-saas-indexer&var-client_id=saas-indexer)
