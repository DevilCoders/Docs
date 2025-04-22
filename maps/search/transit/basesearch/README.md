# Core Transit

Базовый сервис поиска общественного транспорта.

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Владимир Зайцев (volodya@yandex-team.ru) |
| Ответственные SRE | Владимир Зайцев (volodya@yandex-team.ru) |
| Исходники | [maps/search/transit/basesearch](https://a.yandex-team.ru/arc/trunk/arcadia/maps/search/transit/basesearch) |
| Сервис в ABC | [maps-core-search-transit](https://abc.yandex-team.ru/services/maps-core-search-transit/)|
| CI (TestEnv) - Покоммитный | [BUILD_DOCKER_MAPS_CORE_TRANSIT](https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_MAPS_CORE_TRANSIT/history?limit=20) |

## Service infrastructure

### Nanny services

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Datatestingvalidation | [maps_core_transit_datatestingvalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_transit_datatestingvalidation/) | [core-transit.datatestingvalidation](https://yasm.yandex-team.ru/template/panel/maps-core-transit-datatestingvalidation-panel-main/) | [maps_core_transit_datatestingvalidation](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_transit_datatestingvalidation) |
| Datavalidation | [maps_core_transit_datavalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_transit_datavalidation/) | [core-transit.datavalidation](https://yasm.yandex-team.ru/template/panel/maps-core-transit-datavalidation-panel-main/) | [maps_core_transit_datavalidation](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_transit_datavalidation) |
| Stable | [maps_core_transit_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_transit_stable/) | [core-transit.stable](https://yasm.yandex-team.ru/template/panel/maps-core-transit-stable-panel-main/) | [maps_core_transit_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_transit_stable) |
| Testing | [maps_core_transit_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_transit_testing/) | [core-transit.testing](https://yasm.yandex-team.ru/template/panel/maps-core-transit-testing-panel-main/) | [maps_core_transit_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_transit_testing) |
| Unstable | [maps_core_transit_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_transit_unstable/) | [core-transit.unstable](https://yasm.yandex-team.ru/template/panel/maps-core-transit-unstable-panel-main/) | [maps_core_transit_unstable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_transit_unstable) |

### Garden modules

* [Transit Indexer](https://garden.maps.yandex-team.ru/stable/transit_indexer). Запускается после модуля [masstransit_static](https://garden.maps.yandex-team.ru/stable/masstransit_static), собирает индекс, заливает в сэндбокс ресурс [MAPS_TRANSIT_INDEX](https://sandbox.yandex-team.ru/resources?type=MAPS_TRANSIT_INDEX&limit=20&created=14_days) и выкатывает полученный ресурс в datavalidation (или в datatestingvalidation, если билд в testing-окружении).
* [Transit Tester](https://garden.maps.yandex-team.ru/stable/transit_tester). Запускается после transit_indexer и тестирует новосваренный индекс путем сравнения ответов от datavalidation (datatestingvalidation, если в testing-окружении) и stable (testing). Проверяется на корзинах [msk_1](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps-search/transit_coverage/simple/msk_1), [spb_10174](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps-search/transit_coverage/simple/spb_10174) и [mixed](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps-search/transit_coverage/simple/mixed). Допустимое количество неуспешных проверок задано в [конфигах](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/transit_tester/lib/configs).
* [Transit Deployment](https://garden.maps.yandex-team.ru/stable/transit_deployment). Выкатывает индекс, успешно прошедший тестирование, в stable/testing.

### Monitorings

* [Monitorings all (tag=a_prj_maps-core-transit)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-transit)

* [Неответы метапоиску в Сасово](https://yasm.yandex-team.ru/alert/maps-search-transit.sas_unanswers)

* [Неответы метапоиску в Мянтсяля](https://yasm.yandex-team.ru/alert/maps-search-transit.man_unanswers)

* [Неответы метапоиску во Владимире](https://yasm.yandex-team.ru/alert/maps-search-transit.vla_unanswers)

* [Мониторинг на качество поиска](https://juggler.yandex-team.ru/check_details/?host=mapsearch_discovery.sandbox&service=transit_coverage&last=1MONTH)

* [Мониторинг на возраст индекса](https://juggler.yandex-team.ru/check_details/?host=yasm_transit-index-freshness&service=transit-index-freshness&last=1DAY)

## What happens when service is down

Не работает поиск по общественному транспорту в Картах.

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/yandex-maps-search-transit/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | [YQL](https://yql.yandex-team.ru) : USE chyt.hahn; SELECT * FROM "//logs/maps-log/1d/2021-08-20" WHERE tskv_format = 'yandex-maps-search-transit' limit 1; |

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Known clients

[Геометапоиск](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo/meta/rearrs/middle)

## Firewall macroses

| staging | URL |
|---|---|
| stable | [\_ADDRS_PROD_NETS_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_ADDRS_PROD_NETS_) |
| testing | [\_MAPS_CORE_TRANSIT_TESTING_RTC_NETS_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_TRANSIT_TESTING_RTC_NETS_) |

## Regression Stress Testing Configurations

* Регрессионные стрельбы
  * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSEARCH?service=maps-core-search-transit
  * Sandbox: [Тайминги](https://sandbox.yandex-team.ru/scheduler/696353/view), [разладка](https://sandbox.yandex-team.ru/scheduler/696348/view)
  * Если значение разладки оказывается ниже, чем указанный SLA в компоненте в Лунапарке, отправляется соответствующее сообщение в чат geo monitorings и создается тикет в очереди [MAPSREGRESSION](https://st.yandex-team.ru/MAPSREGRESSION).

## Transit Search Quality

* Регулярное тестирование качества поиска, [подробное описание на вики](https://wiki.yandex-team.ru/users/ianaval/transit-search/)
* Есть [шедулер](https://sandbox.yandex-team.ru/scheduler/43711/view), который проверяет процент покрытия по [смешанной корзине](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps-search/transit_coverage/simple/mixed) и отправляет статус в juggler: [алерт](https://juggler.yandex-team.ru/check_details/?host=mapsearch_discovery.sandbox&service=transit_coverage&last=1MONTH).

## How-To

<p>
<details>
<summary>Как выкатывать?</summary>
Выкатка осуществляется <a href="https://docs.yandex-team.ru/sedem/releases">sedem</a>-ом.
Посмотреть список релиз-кандидатов и текущие версии:

<code>sedem release info <путь к сервису/огородному модулю></code>

Покатить в тестовые стейджинги (какие стейджинги считаются тестовыми, задаются в конфиге седема, например, [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/search/transit/basesearch/sedem_config/__all__.yaml?rev=r8054546#L19)):

<code>sedem release start <путь к сервису/огородному модулю> <ревизия> </code>

После того, как релиз успешно выкатится в тестинг, можно катить его в стейбл:

<code>sedem release step <путь к сервису/огородному модулю> <версия> stable </code>

Номер версии после выкатки в тестинг можно посмотреть той же командой <code>sedem release info</code>
</details>

<details>
<summary> Перезапуск билдов огородных модулей </summary>

Упавшие билды можно перезапустить из UI Огорода, нажав на кнопку Restart.

В случае, если хочется перезапустить удачно пробежавший билд map-модуля (такими у нас являются transit_indexer и transit_deployment), придется перед этим удалить в Огороде билды-потомки и сам билд, а потом запустить его заново. При этом логи предыдущих билдов теряются.
</details>

<details>
<summary> Падения огородных модулей </summary>
Модули transit_indexer и transit_deployment имеют свойство падать при неудачной выкатке нового индекса в сервис в Няне. В таких случаях стоит разобраться в причине неудачной выкатки (чаще всего выкатка зависает из-за не отвечающих повисших подов) и, если это модуль transit_indexer, перезапустить его. Transit_deployment можно не перезапускать, если выкатку в Няне подопнули руками, и она доехала.
</details>

<details>
<summary> Endpoint sets </summary>
В каждом ДЦ определено по два endpoint set-а - для прода и для походов из addrs-testing. Понять, какой под для чего предназначен можно на странице <a href="https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_transit_stable/endpoint_sets/">Endpoint Sets</a>, нажав кнопку Resolve Filter соответствующего сета.
</details>
</p>
