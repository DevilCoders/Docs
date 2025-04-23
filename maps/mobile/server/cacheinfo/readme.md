# Maps Core Mobile Cacheinfo
Отдает mapkit'ам список доступных offline кешей

## General information
| Key | Value |
|---|---|
| Ответственные разработчики | Дмитрий Федин (dmfedin@yandex-team.ru) |
| Отвественные SRE | Вадим Мазаев ( vmazaev@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/cacheinfo |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-mobile-cacheinfo/ |
| CI (TestEnv) | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_MOBILE_CACHEINFO |

## Instances
| Environment | URL |
|---|---|
| **Nanny dashboard** | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_mobile_cacheinfo |
| Stable | [maps_core_mobile_cacheinfo_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_cacheinfo_stable) |
| Prestable | [maps_core_mobile_cacheinfo_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_cacheinfo_prestable) |
| Datatesting | [maps_core_mobile_cacheinfo_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_cacheinfo_datatesting) |
| Testing | [maps_core_mobile_cacheinfo_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_cacheinfo_testing) |
| Load | [maps_core_mobile_cacheinfo_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_cacheinfo_load) |

## Graphics dashboards
| Staging | Golovan panel |
|---|---|
| Stable+Prestable | [maps-core-mobile-cacheinfo-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-cacheinfo-stable-panel-main) |
| Datatesting | [maps-core-mobile-cacheinfo-datatesting-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-cacheinfo-datatesting-panel-main) |
| Testing | [maps-core-mobile-cacheinfo-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-cacheinfo-testing-panel-main) |
| Load | [maps-core-mobile-cacheinfo-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-cacheinfo-load-panel-main) |
| MDS storage info | [dashboard](https://yasm.yandex-team.ru/template/panel/mds_proxy/ns=maps-offline-caches/) |

## What happens when service is down
Клиенты не могут скачать или обновить offline кеши.
Деградации: если сломаются ETag-и, то будем отдавать 200 и чрезмерно потреблять трафик пользователей

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/mobile-cacheinfo/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Получить список кэшей:
`apt-get install yandex-maps-downloader protobuf-compiler`
`downloader "spdy3.mob.maps.yandex.net/mapkit2/cacheinfo/2.x/regionlist?deviceid=3dd49f67d93a7149d4ae2066857d1e6f&l=search%2Cdriving&lang=ru_RU&miid=a9bee1321ff4ccadd6be2500c03a91e8a8df1a821&scale=2" | zcat | protoc --decode_raw`
ИЛИ
`apt-get install protobuf-compiler`
`curl --verbose  -H "Host: 2x.cacheinfo.maps.yandex.net" "<hostname>/mapkit/2.x/regionlist?scale=2&l=meta,map,vmap_labels,vmap_geometry&lang=en_EN" | zcat | protoc --decode_raw`

## Balancers
| Staging | URL |
|---|---|
| Production | [core-mobile-cacheinfo.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-cacheinfo.maps.yandex.net/) |
| Datatesting | [core-mobile-cacheinfo.datatesting.maps.n.yandex.ru](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-mobile-cacheinfo-datatesting-slb) |
| Testing | [core-mobile-cacheinfo.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-cacheinfo.testing.maps.yandex.net/) |

## Documentation
На огороде мы собираем оффлайн-кеши для тайлов, поиска, маршрутизации, шрифтов.

Для каждого региона в [конфиге](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/conf/offline_cache/) мы строим заданный набор файлов. Кеши разных типов определяются названием слоя и локалью.

После сборки на группу машин через ecstatic выкатываются датасеты, в которых содержатся протобуфы с информацией о всех сгенерированных кэшах, а так же mds ссылками на файлы кэшей.

Далее на ручку приходят клиенты с определенным списком слоев, scale_factor-ом, локалью, параметрами экспериментов. На основе этих аргументов мы отдаем клиенту подмножество ссылок на файлы кешей, для всех регионов. То есть, клиент получает полный список регионов, в каждом регионе лежит подмножество ссылок на файлы с кешами, построенными для этого региона.

### How to release new soft
1. Перейти из [General information](#general-information) по ссылке в `CI (TestEnv)`, найти свой коммит
2. Перейти в sandbox по ссылке в столбце `task id`, убедиться, что сборка завершилась успешно
3. Нажать на `release`, выбрать окружение, нажать `Release`.

Данное действие **автоматически** выкатит образ в следующие окружения:
- testing -> testing, load;
- prestable -> prestable;
- stable -> stable, datatesting.

Наблюдать за ходом выкладки можно на дашборде из секции [Instances](#instances).

Графики для каждого стейджинга доступны в секции [Graphics dashboards](#graphics-dashboards).
Например, в testing зеркалируется траффик из продакшена, стоит смотреть на него, прежде, чем катить дальше.

### How to release offline caches
Офлайн кэши собираются тремя независимыми датасетами: tiles, search и driving (graph). Сборка и выкладка осуществляется через [огород](https://garden.maps.yandex-team.ru).
1. Собрать нужный кэш в огороде (вкладка Shipping/Offline \<тип>)
2. По необходимости выкатить в дататестинг (вкладка Deployment/\<тип> caches datatesting)
3. Выкатить в продакшн (вкладка Deployment/\<тип> caches production)

В дальнейшем через вкладки Deployment/ можно переключать кэши на нужные версии

## Known clients
- [Maps Core Mobile Proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/proxy/README.md) - мобильная мапкитовая прокся

## Monitorings
| Type | URL |
|---|---|
| Juggler (All) | https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-mobile-cacheinfo |
| Juggler (Stable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_cacheinfo_stable |
| Juggler (Prestable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_cacheinfo_prestable |
| Juggler (Datatesting) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_cacheinfo_datatesting |
| Juggler (Testing) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_cacheinfo_testing |
| Juggler (Load) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_cacheinfo_load |

## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_cacheinfo)
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_cacheinfo.py)

## Ecstatic Datasets
* yandex-maps-mobile-cacheinfo-tile
* yandex-maps-mobile-cacheinfo-search
* yandex-maps-mobile-cacheinfo-driving
* yandex-maps-mobile-cacheinfo-fonts

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
  * /etc/yandex/maps/mobile/cacheinfo - тут хранятся тайловые кэши
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_MOBILE_CACHEINFO_STABLE_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_CACHEINFO_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_MOBILE_CACHEINFO_TESTING_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_CACHEINFO_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
| Type | URL |
|---|---|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPADMIN/3825 |
| Ammo | https://sandbox.yandex-team.ru/scheduler/15811 |
| CI | https://sandbox.yandex-team.ru/scheduler/11825 |
