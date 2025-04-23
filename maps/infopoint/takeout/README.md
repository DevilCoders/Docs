# Maps Jams Infopoint Takeout
Предоставляет интерфейс для взаимодействия с [passport-takeout](https://passport.yandex.ru/profile/getdata)
Информация о родительском Jams Infopoint - [README.md](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/readme.md)

## General information

|  |  |
| --- | --- |
| Кому звонить, если ничего не понятно | Игорь Ретинский ([@retinskii](https://staff.yandex-team.ru/retinskii))<br>Александр Наплавков ([@twisterok](https://staff.yandex-team.ru/twisterok))<br>Антон Газизов ([@bamboo](https://staff.yandex-team.ru/bamboo))|
| Отвественные SRE | Игорь Ретинский ([@retinskii](https://staff.yandex-team.ru/retinskii)) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/takeout |
| Sedem | https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/sedem_config |
| Docker | https://a.yandex-team.ru/arc/trunk/arcadia/infopoint/docker |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-jams-infopoints |
| CI (TestEnv) | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_JAMS_INFOPOINTS |

## Instances
| Environment | URL |
|---|---|
| **Nanny dashboard** | [maps_core_jams_infopoints dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_jams_infopoints/) |
| Stable | [maps_core_jams_infopoints_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_infopoints_stable) |
| Prestable | [maps_core_jams_infopoints_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_infopoints_prestable) |
| Load | [maps_core_jams_infopoints_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_infopoints_load) |
| Testing | [maps_core_jams_infopoints_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_infopoints_testing) |

## Graphics dashboards
| Staging | Golovan panel |
|---|---|
| Stable & Prestable | [maps-core-jams-infopoints-takeout-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-jams-infopoints-takeout-stable-panel-main) |
| Testing & Load | [maps-core-jams-infopoints-takeout-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-jams-infopoints-takeout-testing-panel-main) |

## Monitorings (Juggler)
| Staging |  URL |
| --- | --- |
| stable | [maps_core_jams_infopoints_takeout_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_infopoints_takeout_stable) |
| testing | [maps_core_jams_infopoints_takeout_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_infopoints_takeout_testing) |

## What happens when service is down
Пользователи Яндекс.Карт при инициализации процедуры выгрузки своих данных в контексте GDPR не смогут получить данные относящиеся к Инфоточкам

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx* |
| Yacare service | /var/log/yandex/maps/infopoint-takeout* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YQL | `` SELECT * FROM hahn.`//logs/maps-log/1d/{date}` WHERE vhost = 'core-jams-infopoints.maps.yandex.net' LIMIT 100; `` | `

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
Если во время работы hahn по каким-то причинам будет не доступен.
Задачи будут сохранены и будут пытаться повторно выполниться до восстановления связи с кластером.
Для диагностики можно попробовать сделать выгрузку в ручную по ручке gdpr/takeout.

## Usage
В текущий момент поддерживаются два сценария взаимодействия

1. /gdpr/takeout - позволяет взаимодействовать с сервисом для тестирования разработчиками 
1. /gdpr/schedule_takeout - используется непосредственно Паспортом, осуществляя ассинхронное помещение результатов в хранилище Паспорта

### Первый сценарий

1. Необходимо выписать tvm тикет сервиса самого в себя
   ```sh
   # testing
   ya tool tvmknife get_service_ticket sshkey -s 2017625 -d 2017625
   # production
   ya tool tvmknife get_service_ticket sshkey -s 2017627 -d 2017627
   ```
1. Передать сгенерированный тикет в заголовке
   ```sh
   # testing
   curl -v -k -H 'X-Ya-Service-Ticket: <tvm-ticket>' 'https://core-jams-infopoints-takeout.testing.maps.yandex.net/gdpr/takeout?uid=<uid>'
   # production
   curl -v -k -H 'X-Ya-Service-Ticket: <tvm-ticket>' 'https://core-jams-infopoints-takeout.maps.yandex.net/gdpr/takeout?uid=<uid>'
   ```

### Второй сценарий (тестирование через Паспорт)
В данный момент грант запрошен только для сетевых макросов самого сервиса
Поэтому шаги 2-3 можно будет выполнить только на машинах сервиса в соотвествующем staging

1. Необходимо выписать tvm тикет от сервиса до Паспорта
   ```sh
   # testing
   ya tool tvmknife get_service_ticket sshkey -s 2017625 -d 2009783
   # production
   ya tool tvmknife get_service_ticket sshkey -s 2017627 -d 2009785
   ```
1. Передать сгенерированный тикет в заголовке, а параметры в теле
   ```sh
   # testing
   curl -X POST 'https://takeout-test.passport.yandex.net/1/debug/run_integration_test/?consumer=maps-jams-infopoints-takeout' -d 'uid=<uid>&service_name=maps-infopoint' -H 'X-Ya-Service-Ticket: <tvm-ticket>'
   # production
   curl -X POST 'https://takeout.passport.yandex.net/1/debug/run_integration_test/?consumer=maps-jams-infopoints-takeout' -d 'uid=<uid>&service_name=maps-infopoint' -H 'X-Ya-Service-Ticket: <tvm-ticket>'
   ```
1. Запросить результат теста, передав extract_id полученный на предыдущем шаге
   ```sh
   # testing
   curl -X POST 'https://takeout-test.passport.yandex.net/1/debug/get_status/?consumer=maps-jams-infopoints-takeout' -d 'uid=<uid>&service_name=maps-infopoint&extract_id=<extract_id>' -H 'X-Ya-Service-Ticket: <tvm-ticket>'
   # production
   curl -X POST 'https://takeout.passport.yandex.net/1/debug/get_status/?consumer=maps-jams-infopoints-takeout' -d 'uid=<uid>&service_name=maps-infopoint&extract_id=<extract_id>' -H 'X-Ya-Service-Ticket: <tvm-ticket>'
   ```

### How to release new soft
* Перейти в папку с изохроном `cd maps/infopoint`
* Смотрим `ya tool sedem release info .` по версии
* Если есть unstable/testing:
  * В PR перед мержем указываем тэг в заголовке `[mergeto:maps_core_carparks_renderer_lots:<version>]` см. [пример](https://arcanum.yandex-team.ru/review/1021911/details)
* Если актуальная ветка уже в prestable/stable:
  * Делаем `ya tool sedem release start .` (создаст новый бранч с trunk-а, тикет в StarTrek, дифф в wiki и т.п. )
* Ждем пока появится `V <version>.x` в `ya tool sedem release info .` (пример v1.1)
* Катим в тестинг `ya tool sedem release step . v<version>.x testing` (пример: `ya tool sedem release step . v1.1 testing`)
* Катим в prestable `ya tool sedem release step . v<version>.x prestable` 
* Катим в stable `ya tool sedem release step . v<version>.x stable`
* Если требуется сделать hotfix в уже существующую stable ветку и стандартный `[mergeto]`не работает, то можно:
  * Посмотреть [tips & tricks](https://wiki.yandex-team.ru/elenamarkova/deployment/)
  * Если есть желание сброситься на предыдущую стабильную ветку, то `ya tool sedem release step --force . v<prevVersion>.x stable`
  * Пункт выше эквивалентен [sedem release rollback](https://wiki.yandex-team.ru/geo-infra/sedem/faq/#rollback)
* Всю информацию по работе Release Machine можно посмотреть [тут](https://wiki.yandex-team.ru/geo-infra/SEDEM/faq/#relizy)

Данное действие **автоматически** выкатит образ в следующие окружения: testing, prestable, stable.

Наблюдать за ходом выкладки можно на дашборде из секции [Instances](#instances-nanny).

## Known clients
Сервисы Яндекс.Пасспорт - Takeout

## SLA
Не применим - колличество запросов может составлять 0 за месяц

## Ecstatic Datasets
Отсуствуют. Данные потребляеются из YT

## Балансеры

### AWACS L3-балансер

| Key | Values |
| --- | --- |
| Nanny | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-infopoints.maps.yandex.net/l3-balancers/list/ |
| l3manager | https://l3.tt.yandex-team.ru/service/6380 |
| racktables | https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=7685 |

### AWACS L7-балансеры

| Key | Values |
| --- | --- |
| Prod balancer | [core-jams-infopoints-takeout.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-infopoints-takeout.maps.yandex.net/) |
| L7-балансеры. Сервисы - Production | [rtc_balancer_core-jams-infopoints-takeout_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-infopoints-takeout_maps_yandex_net_man/)<br>[rtc_balancer_core-jams-infopoints-takeout_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-infopoints-takeout_maps_yandex_net_sas/)<br>[rtc_balancer_core-jams-infopoints-takeout_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-infopoints-takeout_maps_yandex_net_vla/) |
| L7-балансеры. Сервисы - Testing | [rtc_balancer_core-jams-infopoints-takeout_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-jams-infopoints-takeout_testing_maps_yandex_net_man/) |

## Persistent Volumes
 /logs - логи, сюда ставится симлинка из /var/log
* /persistent - основной раздел для хранения персистентных данных:
  * /persistent/infopoint-takeout - файлы отображающие запросы ассинхронных запросов выгрузки, используются для восстановления задачи выгрузке при перезагрузке сервиса

## Firewall macroses
| Staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_JAMS_INFOPOINTS_TAKEOUT_STABLE_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_INFOPOINTS_TAKEOUT_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_JAMS_INFOPOINTS_TAKEOUT_TESTING_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_INFOPOINTS_TAKEOUT_TESTING_RTC_NETS_ ) |
