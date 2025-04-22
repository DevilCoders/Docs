# Geoapp Goods Async Processor

Асинхронный обработчик данных товарной базы.

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Михаил Куприянов (kupriyanov-m@yandex-team.ru) <br> Михаил Смирнов (msmirnov91@yandex-team.ru) |
| Отвественные SRE | Михаил Крутяков (mkrutyakov@yandex-team.ru) <br> Антон Прокопьев (aaprokopyev@yandex-team.ru) |
| Исходники | [maps/goods/async_processor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/goods/async_processor) |
| Сервис в ABC | [maps-geoapp-async-processor](https://abc.yandex-team.ru/services/maps-geoapp-async-processor/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_GEOAPP_GOODS_ASYNC_PROCESSOR |
| Документация | [DB Schema](https://a.yandex-team.ru/arc/trunk/arcadia/maps/goods/lib/goods_db/schema/db.sql) |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_geoapp_goods_async_processor_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_async_processor_prestable/) | [ geoapp-goods-async-processor.prestable ](https://yasm.yandex-team.ru/template/panel/maps-geoapp-goods-async-processor-prestable-panel-main/) | [ maps_geoapp_goods_async_processor_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_geoapp_goods_async_processor_prestable) |
| Stable | [maps_geoapp_goods_async_processor_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_async_processor_stable/) | [ geoapp-goods-async-processor.stable ](https://yasm.yandex-team.ru/template/panel/maps-geoapp-goods-async-processor-stable-panel-main/) | [ maps_geoapp_goods_async_processor_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_geoapp_goods_async_processor_stable) |
| Testing | [maps_geoapp_goods_async_processor_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_async_processor_testing/) | [ geoapp-goods-async-processor.testing ](https://yasm.yandex-team.ru/template/panel/maps-geoapp-goods-async-processor-testing-panel-main/) | [ maps_geoapp_goods_async_processor_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_geoapp_goods_async_processor_testing) |


[Monitorings all (tag=a_prj_maps-geoapp-goods-async-processor)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-geoapp-goods-async-processor)

| Staging | PostgreSQL  | Avatars | CleanWeb | S3 | SQS |
| ------- | ----------- | ------- | -------- | -- | --- |
| Testing | [goods-testing](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbdota04krmmk773usa) | sprav-products | [tycoon_goods](https://solomon.yandex-team.ru/?project=safesearch&cluster=cleanweb_preprod&service=cleanweb_router&l.app=router&l.sensor=received&graph=auto&l.client=tycoon_goods&b=1h&e=) | [maps-geoapp-goods-imports-testing](https://yasm.yandex-team.ru/template/panel/s3_client/ctype=testing;owner=33521;bucket=maps-geoapp-goods-imports-testing/?range=36450163) | [maps-geoapp-goods-test: moderation-results.fifo](https://solomon.yandex-team.ru/?project=kikimr&cluster=sqs&service=kikimr_sqs&host=cluster&dashboard=SQS&l.user=maps-geoapp-goods-test&l.queue=moderation-results.fifo) |
| Stable | [goods-stable](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb4klq8nssigf9i8km7) | [sprav-products](https://yasm.yandex-team.ru/template/panel/avatars_mds/ns=sprav-products) | [tycoon_goods](https://solomon.yandex-team.ru/?project=safesearch&cluster=cleanweb&service=cleanweb_router&l.app=router&l.sensor=received&graph=auto&l.client=tycoon_goods&b=1h&e=) | [maps-geoapp-goods-imports-stable](https://yasm.yandex-team.ru/template/panel/s3_client/ctype=production;owner=33521;bucket=maps-geoapp-goods-imports-stable) | [maps-geoapp-goods: moderation-results.fifo](https://solomon.yandex-team.ru/?project=kikimr&cluster=sqs&service=kikimr_sqs&host=cluster&dashboard=SQS&l.user=maps-geoapp-goods&l.queue=moderation-results.fifo) |

### Other components

| Name | Testing | Stable |
| ---- | ------- | ------ |
| PostgreSQL | [goods-testing](https://yc.yandex-team.ru/folders/aku2lc9fjae6f5bhtaru/managed-postgresql/cluster/mdbdota04krmmk773usa) | [goods-stable](https://yc.yandex-team.ru/folders/aku2lc9fjae6f5bhtaru/managed-postgresql/cluster/mdb4klq8nssigf9i8km7) |
| Avatars | - | [sprav-products](https://mds.yandex-team.ru/avatars/namespaces/sprav-products/overview) |

## What happens when service is down

Начинаются проблемы со вкладкой "Товары и услуги" в личном кабинете Яндекс.Бизнес:

1. Перестают импортироваться прайс-листы, загруженные пользователями в виде файлов (висят в обработке)
2. Информация о товарах и услугах перестаёт публиковаться (выгружаться в сниппеты Карт)

При этом API вкладки "Товары и услуги" сохраняет работоспособность.

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/goods-async-processor/* |
| Yacare service (json) | /var/log/yandex/maps/goods-async-processor-json/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'goods-async-processor.maps.yandex.net' limit 1; |
| YT (service logs) | [stable](https://yt.yandex-team.ru/hahn/navigation?path=//logs/maps-front-geosearch-geoapp-goods-stable-async-processor-logs), [testing](https://yt.yandex-team.ru/hahn/navigation?path=//logs/maps-front-geosearch-geoapp-goods-testing-async-processor-logs) |
| Logbroker | [stable](https://lb.yandex-team.ru/logbroker/accounts/maps-front-geosearch/geoapp-goods/stable/async-processor), [testing](https://lb.yandex-team.ru/logbroker/accounts/maps-front-geosearch/geoapp-goods/testing/async-processor) |

## How to fix common problems

- [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
- **CleanWeb жалуется на избыточную нагрузку** &mdash; остановить сервис с помощью ``yacare detach all`` и звать разработчиков
- **PhotoUploader-loop-failure-count** &mdash; известна проблема с превышением рейтлимитера.
  В логах при этом должны быть ошибки от Аватарницы с кодом 429:
  `too many put requests to your namespace`.
  Можно попытаться остановать загрузку фоток на нескольких подах и разбираться, почему выросла нагрузка. Источник запросов можно поискать [в вот этом веб-интерфейсе Аватарницы](https://avatars.chv.yandex-team.ru/projects/sprav-products/network?filter=handler_type%20%3D%3D%20PUT).


**В любой непонятной ситуации** можно остановить сервис с помощью ``yacare detach all`` и разбираться дальше с остановленным сервисом. Пользователи личного кабинета Бизнеса заметят только то, что их прайсы будут долго висеть на импорте, но API тем временем будет для них доступно и продолжит работать.

**Остановить один из background-процессов** можно запросом в ручку `/pause`, зайдя на поду. Примерно так:

```bash
# Остановить
curl -X POST http://localhost/internal/threads/pause?thread=PricesImporter \
    -H 'Host: goods-async-processor.stable.maps.yandex.net'

# Перезапустить
curl -X POST http://localhost/internal/threads/unpause?thread=PricesImporter \
    -H 'Host: goods-async-processor.stable.maps.yandex.net'

# Посмотреть список процессов и их статус
curl -X GET http://localhost/internal/threads/list \
    -H 'Host: goods-async-processor.stable.maps.yandex.net'

# Остановить все процессы (перезапустить можно аналогично)
curl -X POST http://localhost/internal/threads/pause?thread=all \
    -H 'Host: goods-async-processor.stable.maps.yandex.net'
```

## Documentation

- [Товарный поиск 2.0](https://wiki.yandex-team.ru/users/kupriyanov-m/tovarnyjj-poisk-2.0/)
- [Новый личный кабинет: Архитектура](https://wiki.yandex-team.ru/users/kupriyanov-m/goodsandservicesfunduk/tycoongoodspart/novyjj-lichnyjj-kabinet/)

## Known clients

- [Фундук](https://a.yandex-team.ru/arc/trunk/arcadia/maps/goods/funduk) &mdash; забирает опубликованные данные и выкладывает их в сниппеты на Картах
- [api_server](https://a.yandex-team.ru/arc/trunk/arcadia/maps/goods/api_server) &mdash; загружает в общую базу файлы с товарами для импорта

## SLA

Не требуется, т.к. нет API.

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_async_processor_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_async_processor_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_async_processor_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_GEOAPP_GOODS_API_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_GEOAPP_GOODS_API_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_GEOAPP_GOODS_API_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_GEOAPP_GOODS_API_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations

Стрельб нет, т.к. нет API

