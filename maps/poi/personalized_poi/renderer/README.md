## General information
| Key | Value |
|---|---|
| Ответственные разработчики | [Группа качества сервисов](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) |
| Ответственные SRE | [Группа качества сервисов](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/ |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-personalized-poi-renderer/ |
| CI (TestEnv) - Покомитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_PERSPOI_RDR |
| Исходники стрельб | https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/renderer/regression |

## Instances
| Environment | URL |
|---|---|
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_personalized_poi_renderer_stable |
| prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_personalized_poi_renderer_prestable |
| datavalidation | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_personalized_poi_renderer_datavalidation |
| datatesting | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_personalized_poi_renderer_datatesting |
| datatestingvalidation | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_personalized_poi_renderer_datatestingvalidation |
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_personalized_poi_renderer_testing |
| load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_personalized_poi_renderer_load |

| Dashboard |
|---|
| https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_personalized_poi |


## TVM
Информация доступна в [abc](https://abc.yandex-team.ru/services/maps-core-personalized-poi-renderer/resources/?supplier=14&type=47&type=50&state=requested&state=approved&state=granted&view=consuming)

## Documentation
https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi <br/>
https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder <br/>
https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/renderer/yacare <br/>


## Known clients

- Mobile proxy (\_C_MAPS_MOBILE\_)

## Graphics
| Type |
|---|
| [stable+prestable](https://yasm.yandex-team.ru/template/panel/maps-core-personalized-poi-renderer-stable-panel-main/) |
| [prestable](https://yasm.yandex-team.ru/template/panel/maps-core-personalized-poi-renderer-prestable-panel-main/) |
| [datavalidation](https://yasm.yandex-team.ru/template/panel/maps-core-personalized-poi-renderer-datavalidation-panel-main/) |
| [datatesting](https://yasm.yandex-team.ru/template/panel/maps-core-personalized-poi-renderer-datatesting-panel-main/) |
| [datatestingvalidation](https://yasm.yandex-team.ru/template/panel/maps-core-personalized-poi-renderer-datatestingvalidation-panel-main/) |
| [testing](https://yasm.yandex-team.ru/template/panel/maps-core-personalized-poi-renderer-testing-panel-main/) |
| [load](https://yasm.yandex-team.ru/template/panel/maps-core-personalized-poi-renderer-load-panel-main/) |

Для детальной диагностики так же можно посмотреть графики, предоставляемые Няней для каждого инстанса и детальные графики балансеров.

## Monitorings
| Type | URL |
|---|---|
| stable (with prestable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_personalized_poi_renderer_stable |
| prestable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_personalized_poi_renderer_prestable |
| datavalidation | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_personalized_poi_renderer_datavalidation |
| datatesting | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_personalized_poi_renderer_datatesting |
| datatestingvalidation | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_personalized_poi_renderer_datatestingvalidation |
| testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_personalized_poi_renderer_testing |
| load | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_personalized_poi_renderer_load |

## Regression testing

https://lunapark.yandex-team.ru/regress/GEOQ?service=maps-core-personalized-poi-renderer

## Ecstatic datasets
* yandex-maps-perspoi-renderer
* yandex-maps-perspoi-design
* yandex-maps-perspoi-dynamic

[стейбл](http://ecstatic.maps.yandex.net/) и [дататестинг](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/) экстатики

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_PERSONALIZED_POI_RENDERER_STABLE_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_PERSONALIZED_POI_RENDERER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_PERSONALIZED_POI_RENDERER_TESTING_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_PERSONALIZED_POI_RENDERER_TESTING_RTC_NETS_ ) |


## Logs
Файловые логи искать в контейнерах в сервисах Няни.

| Name | Path |
|---|---|
| Nginx | /var/log/nginx/* |
| Poi renderer | /var/log/yandex/maps/personalized_poi_renderer/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Roquefort | /var/log/yandex/roquefort/* |

## Balancers
#### Production - core-personalized-poi-renderer.maps.yandex.net
* L3
  * L3-manager: https://l3.tt.yandex-team.ru/service/5306
  * Racktables: https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=6622
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-personalized-poi-renderer.maps.yandex.net/l3-balancers/list/
  * Grafana: https://grafana.yandex-team.ru/d/WIxTf99iz/l3-vs-core-personalized-poi-renderer-maps-yandex-net

* L7
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-personalized-poi-renderer.maps.yandex.net/show/
  * Nanny-сервисы для awacs-l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-personalized-poi-renderer_maps_yandex_net_man/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-personalized-poi-renderer_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-personalized-poi-renderer_maps_yandex_net_vla/
  * Фаервол: https://puncher.yandex-team.ru/?destination=core-personalized-poi-renderer.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination


#### Testing - core-personalized-poi-renderer.common.testing.maps.yandex.net
В качестве тестингового балансера используется коммунальный: common.testing.maps.yandex.net.

* L3
  * L3-manager: https://l3.tt.yandex-team.ru/service/11006
  * Racktables: https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=12298
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/l3-balancers/list/
  * Grafana: https://grafana.yandex-team.ru/d/90iRzVFGz/l3-vs-common-testing-maps-yandex-net?
* L7
  * Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/show/
  * Nanny-сервисы для awacs-l7-балансеров:
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas/
    * https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla/
  * Фаервол: https://puncher.yandex-team.ru/?destination=core-personalized-poi-renderer.common.testing.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination


## SLA
* [chart wizard](https://charts.yandex-team.ru/preview/wizard/maps_SLA/maps_core_personalized_poi_renderer)
* [stat](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_personalized_poi_renderer)
* [arcanum](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_personalized_poi_renderer.py)

## Regression Stress Testing Configurations
| Name | Link |
|---|---|
| Lunapark | https://lunapark.yandex-team.ru/regress/GEOQ?service=maps-core-personalized-poi-renderer |
| Sandbox | https://sandbox.yandex-team.ru/scheduler/14169/view |
| Startrek | https://st.yandex-team.ru/GEOQ-88 |

## Про окружения
Общую картину с окружениями и как релизятся данные/софт можно посмотреть
[в общем описании окружений](https://wiki.yandex-team.ru/maps/dev/core/environment/)
и [в документации огорода](https://docs.yandex-team.ru/garden/data_deploy).

В наших реалиях:
| Окружение | Данные | Ecstatic | Ecstatic branch | Софт | Трафик |
| --- | --- | --- | --- | --- | --- |
| testing | `stable` | [testing](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/list) | stable | testing | Зеркалируется из `stable` с заменой puid |
| load | `stable` | [testing](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/list) | stable | testing | Трафик только из-за [обстрелов](https://lunapark.yandex-team.ru/regress/GEOQ?service=maps-core-personalized-poi-renderer) |
| prestable | `stable` | [stable](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/list) | stable | prestable | Несколько процентов реального трафика пользователей |
| datatesting | `testing` | [datatesting](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/list) | stable | stable | Зеркалируется из `testing` |
| datatestingvalidation | `testing` | [datatesting](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/list) | testing | stable | Трафик только из-за обстрелов (**TBD**) |
| datavalidation | `stable` | [stable](http://core-ecstatic-coordinator.maps.yandex.net/pkg/list) | testing | stable | Трафик только из-за обстрелов (**TBD**) |
| stable | `stable` | [stable](http://core-ecstatic-coordinator.maps.yandex.net/pkg/list) | stable | stable | Весь основной трафик пользователей |

# How to release with SEDEM (humorous instruction by ngng@)

1. Зайди в директорию с тем, что хочешь выкатить в любимом терминале на любимой машинке (`~/arcadia/maps/poi/personalized_poi/renderer` скорее всего)
2. Делай `ya tool sedem release info .` и очень внимательно посмотри что оно вывело
3. После того, как ты достаточно насмотрелся и морально приготовился, запускай `ya tool sedem release start .`
4. Иди на большой кофепоинт (желательно), завари крепкий двойной эспрессо и вернись обратно (желательно)
5. Операция может либо не закончиться (в таком случае я бы апнул скилл “походник за кофе”), закончиться с `DEPLOY_SUCCESS` (в таком случае нужно перейти к следующему шагу), либо упасть ошибкой (тогда тебе (https://wiki.yandex-team.ru/geo-infra/sedem/faq/) надо читать вот это (https://wiki.yandex-team.ru/geo-infra/sedem/faq/) или спросить у коллег, что делать)
6. Пей кофе и изображай работу. Так хотя бы 30-40 минут или пока к тебе не подойдут и не спросят “что с релизом?“
7. Сделай `ya tool sedem release info .` ещё раз или зайди на няню через ссылку, которую тебе кинула предыдущая операция (она начинается на `nanny.yandex-team.ru/*`). Посмотри какая версия релиза у тебя получилась.
8. Запускай `ya tool sedem release step . {версия релиза} prestable`, после этого можешь повторить шаг 6 или реально пойти работать, потому что злоупотреблять доверием плохо
9. В принципе, если к тебе еще не пришли и этот чат не завален сообщениями о пожарах в датацентре или/и в районе кресла руководителя группы, то можешь смело делать `ya tool sedem release step . {версия релиза} stable`.
10. `PROFIT_SUCCESS`

# Troubleshooting

Возможные действия в случае срабатывания мониторинга персональных POI:

* Если вам позвонил мониторинг, нужно, следуя голосовым указаниям робота,
  остановить эскалацию, поставить даунтайм в чате GeoQuality - Monitorings, и
  начать разбираться с проблемой, либо передать ее свободному дежурному и
  удостовериться, что инцидент начал расследоваться.
* Проверить отображение персональных и динамических POI через все клиенты:
  Мобильные Яндекс Карты, Браузерные Яндекс Карты. Для проверки можно
  использовать 
  [тестовых пользователей](https://yav.yandex-team.ru/secret/sec-01fms46dtbtt0hr6tm6n8s98cg/explore/version/ver-01fms46dv30hxjb8xmpah0wat5).
* Установить, совпадает ли падение с одним из следующих событий: 
  * выкатка новой версии софта: в nanny (см. раздел [Instances](#instances))
    можно посмотреть активный релиз и его поле Since, либо при помощи команды 
    `ya tool sedem release info .` в папке 
    `/maps/poi/personalized_poi/renderer`.
  * публикация одного из датасетов: по ссылкам из раздела [Ecstatic
    datatsets](#ecstatic-datasets)
    зайти в нужное окружение, зайти в каждый датасет, в активную версию,
    посмотреть даты публикации;
  * учения (https://infra.yandex-team.ru/).
* Зайти на любой бекенд в интересующем окружении. Для этого нужно
  воспользоваться ссылками на nanny (см. раздел [Instances](#instances)). Далее
  на активной плашке нажать Instances, в развернувшемся списке найти активный
  инстанс и слева от него нажать на облачко, скопировать строку подключения по
  SSH.
* Посмотреть сообщения в логах, пути до логов указаны в одной из секций выше.
* При помощи SEDEM откатить версию софта на предыдущую. Команды описаны в
  документации SEDEM: 
  https://docs.yandex-team.ru/sedem/releases#release-rollback.
* Откатить датасеты. Рекомендуется откатывать по одному, а не все сразу, если 
  позволяет время. Процедура отката подробно описана в документации:
  https://docs.yandex-team.ru/ecstatic/instructions/dataset_rollback
* Если требуется более точно локализовать проблему и предыдущие пункты не дали
  результатов, можно попробовать отключить динамические POI. Для этого нужно
  перейти в шедулер динамических POI и предварительно сохранив куда-то очистить
  список источников. Список актуальных шедулеров можно найти в
  [personalized_poi/builder/dynamic_poi/README.md](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/dynamic_poi).
* Если проблема связана с конкретным источником данных для динамических POI, то
  нужно связаться с поставщиками соответствующего датасета, если есть серьезное
  опасение, что данные битые, то стоит отключить проблемный источник в шедулере
  согласно 
  [personalized_poi/builder/dynamic_poi/README.md](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/dynamic_poi).
* Для более точной локализации проблемы стоит получить backtrace. Узнать pid
  процесса: `ps aux | grep personalized_poi_renderer`. Подключиться при помощи
  `gdb -p <pid>` к процессу. Установить break point на строчке из логов `break
  path/to/file:line`. И продолжить исполнение процесса `continue`. Получить
  backtrace: `backtrace`.
* При необходимости собрать и выкатить hotfix по инструкции SEDEM:
  https://docs.yandex-team.ru/sedem/releases#release-hotfix.
* Управлять статусом сервиса в рамках одной машины можно при помощи команд
  `yacare [start|stop|restart|status|stacktraces|loglevel] personalized_poi_renderer`.
* Поснифать запросы в реальном времени можно командой `tshark -i veth -V -Y
  "http.request"`.
