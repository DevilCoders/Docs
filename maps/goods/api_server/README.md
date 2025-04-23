# Geoapp Goods Api Server

API к базе товарного поиска

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Михаил Куприянов (kupriyanov-m@yandex-team.ru) <br> Михаил Смирнов (msmirnov91@yandex-team.ru) |
| Отвественные SRE | Михаил Крутяков (mkrutyakov@yandex-team.ru) <br> Антон Прокопьев (aaprokopyev@yandex-team.ru) |
| Исходники | [maps/goods/api_server](https://a.yandex-team.ru/arc/trunk/arcadia/maps/goods/api_server) |
| Сервис в ABC | [maps-geoapp-goods-api](https://abc.yandex-team.ru/services/maps-geoapp-goods-api/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_GEOAPP_GOODS_API_SERVER |
| Документация | [API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/goods/api_server/docs/api.md) <br> [DB Schema](https://a.yandex-team.ru/arc/trunk/arcadia/maps/goods/lib/goods_db/schema/db.sql) |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_geoapp_goods_api_server_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_api_server_prestable/) | [ geoapp-goods-api-server.prestable ](https://yasm.yandex-team.ru/template/panel/maps-geoapp-goods-api-server-prestable-panel-main/) | [ maps_geoapp_goods_api_server_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_geoapp_goods_api_server_prestable) |
| Stable | [maps_geoapp_goods_api_server_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_api_server_stable/) | [ geoapp-goods-api-server.stable ](https://yasm.yandex-team.ru/template/panel/maps-geoapp-goods-api-server-stable-panel-main/) | [ maps_geoapp_goods_api_server_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_geoapp_goods_api_server_stable) |
| Stress | [maps_geoapp_goods_api_server_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_api_server_stress/) | [ geoapp-goods-api-server.stress ](https://yasm.yandex-team.ru/template/panel/maps-geoapp-goods-api-server-stress-panel-main/) | [ maps_geoapp_goods_api_server_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_geoapp_goods_api_server_stress) |
| Testing | [maps_geoapp_goods_api_server_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_api_server_testing/) | [ geoapp-goods-api-server.testing ](https://yasm.yandex-team.ru/template/panel/maps-geoapp-goods-api-server-testing-panel-main/) | [ maps_geoapp_goods_api_server_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_geoapp_goods_api_server_testing) |


[Monitorings all (tag=a_prj_maps-geoapp-goods-api-server)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-geoapp-goods-api-server)

**Ratelimiter panel** [RPS and Quotas](https://yasm.yandex-team.ru/template/panel/maps_goods_api_server-ratelimiter2-panel/)

| Staging | PostgreSQL  | Avatars | CleanWeb | S3 |
| ------- | ----------- | ------- | -------- | -- |
| Testing | [goods-testing](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbdota04krmmk773usa) | sprav-products | [tycoon_goods](https://solomon.yandex-team.ru/?project=safesearch&cluster=cleanweb_preprod&service=cleanweb_router&l.app=router&l.sensor=received&graph=auto&l.client=tycoon_goods&b=1h&e=) | [maps-geoapp-goods-imports-testing](https://yasm.yandex-team.ru/template/panel/s3_client/ctype=testing;owner=33521;bucket=maps-geoapp-goods-imports-testing/?range=36450163) |
| Stable | [goods-stable](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb4klq8nssigf9i8km7) | [sprav-products](https://yasm.yandex-team.ru/template/panel/avatars_mds/ns=sprav-products) | [tycoon_goods](https://solomon.yandex-team.ru/?project=safesearch&cluster=cleanweb&service=cleanweb_router&l.app=router&l.sensor=received&graph=auto&l.client=tycoon_goods&b=1h&e=) | [maps-geoapp-goods-imports-stable](https://yasm.yandex-team.ru/template/panel/s3_client/ctype=production;owner=33521;bucket=maps-geoapp-goods-imports-stable) |


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [geoapp-goods-api-server.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/geoapp-goods-api-server.maps.yandex.net/) | [geoapp-goods-api-server.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=geoapp-goods-api-server.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,man,sas;prj=geoapp-goods-api-server-maps;signal=service_total) | [rtc_balancer_geoapp-goods-api-server_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_geoapp-goods-api-server_maps_yandex_net_man)<br>[rtc_balancer_geoapp-goods-api-server_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_geoapp-goods-api-server_maps_yandex_net_sas)<br>[rtc_balancer_geoapp-goods-api-server_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_geoapp-goods-api-server_maps_yandex_net_vla) |
| Testing | Default | [geoapp-goods-api-server.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/geoapp-goods-api-server.testing.maps.yandex.net/) | [geoapp-goods-api-server.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=geoapp-goods-api-server.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,man,sas;prj=geoapp-goods-api-server-testing-maps;signal=service_total) | [rtc_balancer_geoapp-goods-api-server_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_geoapp-goods-api-server_testing_maps_yandex_net_man)<br>[rtc_balancer_geoapp-goods-api-server_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_geoapp-goods-api-server_testing_maps_yandex_net_sas)<br>[rtc_balancer_geoapp-goods-api-server_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_geoapp-goods-api-server_testing_maps_yandex_net_vla) |

### Other components

| Name | Testing | Stable |
| ---- | ------- | ------ |
| PostgreSQL | [goods-testing](https://yc.yandex-team.ru/folders/aku2lc9fjae6f5bhtaru/managed-postgresql/cluster/mdbdota04krmmk773usa) | [goods-stable](https://yc.yandex-team.ru/folders/aku2lc9fjae6f5bhtaru/managed-postgresql/cluster/mdb4klq8nssigf9i8km7) |


## What happens when service is down

Начинаются проблемы со вкладкой "Товары и услуги" в личном кабинете Яндекс.Бизнес:

1. Товары перестают отображаться во вкладке
2. Невозможно загрузить товары, фотографии и файлы с прайсами для импорта

## BlackBox grants

Искать по `maps-geoapp-goods-api` в [форме](https://grantushka.yandex-team.ru/grants/consumer/).
Используем BlackBox, чтобы получить UID пользователя и проверить права на организацию.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/goods-api-server/* |
| Yacare service (json) | /var/log/yandex/maps/goods-api-server-json/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'geoapp-goods-api-server.maps.yandex.net' limit 1; |
| YT (service logs) | [stable](https://yt.yandex-team.ru/hahn/navigation?path=//logs/maps-front-geosearch-geoapp-goods-stable-api-server-logs), [testing](https://yt.yandex-team.ru/hahn/navigation?path=//logs/maps-front-geosearch-geoapp-goods-testing-api-server-logs) |
| Logbroker | [stable](https://lb.yandex-team.ru/logbroker/accounts/maps-front-geosearch/geoapp-goods/stable/api-server), [testing](https://lb.yandex-team.ru/logbroker/accounts/maps-front-geosearch/geoapp-goods/testing/api-server) |

## How to fix common problems

- [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
- **default-balancer-5xx** &mdash; посмотреть в логи и на графики.
    Если причина в таймаутах запросов к базе, и ошибок мало (разовое явление), то выставить даунтайм и призывать разработчиков.
    Если ошибок много, остановить сервис ``async_processor`` с помощью команды:
```bash
ya tool sedem p_exec --cmd 'yacare detach all' maps_geoapp_goods_async_processor_prestable maps_geoapp_goods_async_processor_stable
```
- **total-4xx** &mdash; проверка отключена для сервиса, т.к. большое количество `4xx` ответов ожидаемо. Если она почему-то включилась, можно выставить даунтайм.
- Товары ошибочно **отклонены модерацией** - [Тикет в котором чинили подобную проблему](https://st.yandex-team.ru/GOODSFEEDBACK-12), [wiki:Ручная модерация прайсов](https://wiki.yandex-team.ru/users/kupriyanov-m/tovarnyjj-poisk-2.0/ruchnaja-moderacija-prajjsov/)
- **Забился диск в PostgreSQL** из-за таблицы `items_history` - [wiki:Как вручную ротировать items_history](https://wiki.yandex-team.ru/users/kupriyanov-m/tovarnyjj-poisk-2.0/ruchnaja-moderacija-prajjsov/#kakvruchnujurotirovatitemshistory)
- [Ratelimiter alerts troubleshooting](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ratelimiter2/agent_troubleshooting.md)

## Documentation

- [Товарный поиск 2.0](https://wiki.yandex-team.ru/users/kupriyanov-m/tovarnyjj-poisk-2.0/)
- [Новый личный кабинет: Архитектура](https://wiki.yandex-team.ru/users/kupriyanov-m/goodsandservicesfunduk/tycoongoodspart/novyjj-lichnyjj-kabinet/)

## Known clients

- [async_processor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/goods/async_processor) &mdash; забирает из общей базы файлы прайсов для импорта
- **Фронтенд Яндекс.Бизнес** &mdash; ходит в API

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_geoapp_goods_api_server) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_geoapp_goods_api_server.py)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_api_server_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_api_server_stable/yp_pods/ |
| Stress | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_api_server_stress/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_geoapp_goods_api_server_testing/yp_pods/ |

## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_GEOAPP_GOODS_API_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_GEOAPP_GOODS_API_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_GEOAPP_GOODS_API_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_GEOAPP_GOODS_API_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/GEOAPPGOODS
    * Reactor: https://reactor.yandex-team.ru/browse?selected=9089738
    * Тикет (const): https://st.yandex-team.ru/GEOAPPGOODS-77
    * Тикет (imbalance): https://st.yandex-team.ru/GEOAPPGOODS-78
