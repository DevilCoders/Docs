# Core Indoor Radiomap Capturer

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) <br> Илья Власюк (tail@yandex-team.ru) |
| Отвественные SRE | Александр Миков (sashamikoff@yandex-team.ru) <br> Алексей Панёв (panevnav@yandex-team.ru) <br> Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) <br> Василий Косьянчук (kosyanchuk@yandex-team.ru) <br> Павел Тычинин (pnavigine@yandex-team.ru) <br> Фёдор Пучков (fnav@yandex-team.ru) |
| Исходники | [maps/indoor/radiomap-capturer](https://a.yandex-team.ru/arc/trunk/arcadia/maps/indoor/radiomap-capturer) |
| Сервис в ABC | [maps-core-indoor-radiomap-capturer](https://abc.yandex-team.ru/services/maps-core-indoor-radiomap-capturer/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_INDOOR_RADIOMAP_CAPTURER |


## Service infrastructure

### Instances and graphics

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_indoor_radiomap_capturer_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_indoor_radiomap_capturer_stable/) | [ core-indoor-radiomap-capturer.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-indoor-radiomap-capturer-stable-panel-main/) | [ maps_core_indoor_radiomap_capturer_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_indoor_radiomap_capturer_stable) |
| Testing | [maps_core_indoor_radiomap_capturer_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_indoor_radiomap_capturer_testing/) | [ core-indoor-radiomap-capturer.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-indoor-radiomap-capturer-testing-panel-main/) | [ maps_core_indoor_radiomap_capturer_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_indoor_radiomap_capturer_testing) |


MDB:
| Staging | User panels |
| ------- | ----------- |
| Stable | [indoor_capturer](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdba24p00o7ufj5gpskv;dbname=indoor_capturer/) |
| Testing | [indoor_capturer](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbpj555a068v9lmnkhd;dbname=indoor_capturer/) |


### Monitorings
Все мониторинги можно найти по тегу [`a_prj_maps-core-indoor-radiomap-capturer`][juggler-all-checks].


#### Мониторинг копирования данных из PostgreSQL в YT
Данный мониторинг следит за свежестью данных в YT которые туда копируются с помощью [Трансфер менеджера][tm]. Информация об активности Трансфер Менеджера сохраняется в Соломоне и доступна на [дешборде][solomon-tm-replication-dashboard]. В свою очередь, в картах используется Джаглер. Для объединения этих двух систем, в Соломоне настроен [алерт PostgreSQL to YT Replication Delay (Indoor UGC)][solomon-psql-to-yt]. Этот алерт пробрасывается в мониторинг настроенный в Джаглере: [`host=solomon-alert, service=nmaps_dynamic_replica_indoor_ugc`][juggler-psql-to-yt].


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-indoor-radiomap-capturer.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-indoor-radiomap-capturer.maps.yandex.net/) | [core-indoor-radiomap-capturer.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-indoor-radiomap-capturer.maps.yandex.net;itype=balancer;ctype=prod;locations=man,vla,sas;prj=core-indoor-radiomap-capturer-maps;signal=service_total) | [rtc_balancer_core-indoor-radiomap-capturer_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-indoor-radiomap-capturer_maps_yandex_net_man)<br>[rtc_balancer_core-indoor-radiomap-capturer_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-indoor-radiomap-capturer_maps_yandex_net_sas)<br>[rtc_balancer_core-indoor-radiomap-capturer_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-indoor-radiomap-capturer_maps_yandex_net_vla) |
| Testing | Default | [core-indoor-radiomap-capturer.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-indoor-radiomap-capturer.testing.maps.yandex.net/) | [core-indoor-radiomap-capturer.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-indoor-radiomap-capturer.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas;prj=core-indoor-radiomap-capturer-testing-maps;signal=service_total) | [rtc_balancer_core-indoor-radiomap-capturer_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-indoor-radiomap-capturer_testing_maps_yandex_net_sas) |


## What happens when service is down

TODO: Напишите, что происходит при отказе сервиса

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/mobile-indoor-radiomap-capturer/* |
| Cron Job | /var/log/yandex/maps/radiomap-evaluation-cron-job/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-indoor-radiomap-capturer.maps.yandex.net' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

TODO: Добавьте описание, как чинить ваш сервис


## Documentation

Сервис по сбору радиокарт
### Основной функционал
- Периодическое создание заданий для обходов ТЦ по "мета"-заданиям
- Поиск доступных заданий на карте
- Возможность взять задание в работу и отказаться от уже принятого задания
- Возможность принять собранные траектории, сделать первичную валидацию собранных данных
- Восстановление позиций маяков по собранным траекториям

### Описание концепции работы:
- В приложении mrc, на карте отображаются задания синими или красными точками. При тапе на задание его можно взять в работу или отказаться от задания, которое было принято в работу ранее.
- Каждое задание содержит в себе набор траекторий на каждом этаже здания.
- Каждая траектория (длительностью не более 15 минут) состоит из набора *check point*-ов. При достижении очередного *check point*-а пользователь должен нажать *check in* и продолжить обход.
- При достижении последнего *check point*-а пользователь должен завершить обход нажав кнопку *finish*

### Список endpoint'ов для общения c сервисом:
- [/indoor/tasks/search](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/indoor/radiomap-capturer/lib/agent_api.cpp?rev=7437168#L34)- производит поиск заданий на карте по заданному *bbox*. 
-- Ответ: cписок (доступных для выполнения или взятых в работу) заданий
-- Формат ответа: [protobuf](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/common2/response.proto?rev=7437168#L5)
-- Пример ответа: [text-plain](/trunk/arcadia/maps/mobile/libs/mrc/indoor/tests/data/indoor_tasks_search.pb.txt)

- [/indoor/tasks/acquire](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/indoor/radiomap-capturer/lib/agent_api.cpp?rev=7437168#L66) - взять задание в работу
-- Ответ: задание, взятое в работу
-- Формат ответа: [protobuf](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/common2/response.proto?rev=7437168#L5 )
-- Пример ответа: [text-plain](/trunk/arcadia/maps/mobile/libs/mrc/indoor/tests/data/indoor_tasks_acquire.pb.txt)

- [/indoor/assignments/list](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/indoor/radiomap-capturer/lib/agent_api.cpp?rev=7437168#L98) - получить список заданий (взятых в работу или тех от которых пользователь отказался) для конкретного пользователя. 
-- Ответ: cписок заданий, взятых в работу
-- Формат ответа: [protobuf](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/common2/response.proto?rev=7437168#L5)
-- Пример ответа: [text-plain](/trunk/arcadia/maps/mobile/libs/mrc/indoor/tests/data/indoor_assignments_list.pb.txt)

- [/indoor/assignments/complete](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/indoor/radiomap-capturer/lib/agent_api.cpp?rev=7437168#L169) - завершить задание.

- [/indoor/assignments/abandon](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/indoor/radiomap-capturer/lib/agent_api.cpp?rev=7437168#L202 ) - отказаться от задания.

- [/indoor/assignments/paths](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/indoor/radiomap-capturer/lib/agent_api.cpp?rev=7437168#L232) - получить список маршрутов для конкретного задания. 
-- Ответ: cписок маршрутов обхода для задания
-- Формат ответа: [protobuf](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/common2/response.proto?rev=7437168#L5)
-- Пример ответа: [text-plain](/trunk/arcadia/maps/mobile/libs/mrc/indoor/tests/data/indoor_paths_list.pb.txt)

- [/indoor/paths/upload](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/indoor/radiomap-capturer/lib/upload_api.cpp?rev=7437168#L38 ) - загрузить собранные радиосигналы, провести первичную валидацию обхода и сохранить результат в s3. 
-- Формат данных: [protobuf](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/offline-mrc/indoor.proto?rev=7437168#L63)

### Список таблиц:

#### **ugc.task**
Данная таблица описывает одно задание на карте

| **Column** | **Type** | **Description** |
| ---------- | -------- | --------------- |
| task_id| bigint | primary key |
| status| ugc.task_status | available, acquired, done, pending, cancelled |
| geom | geometry(Point,4326) | расположение задания на карте |
| distance| bigint | примерное суммарное расстояние всех обходов (в метрах) |
| duration| bigint | примерная суммарная длительность всех обходов (в секундах) |
| indoor_plan_id| bigint | *indoorPlanId* идентификатор здания (из НЯК) |

#### **ugc.task_path** 
Данная таблица описывает один обход, на одном этаже

| **Column** | **Type** | **Description** |
| ---------- | -------- | --------------- |
| task_path_id| bigint | primary key |
| task_id| bigint |  идентификатор задания, к которому относится обход|
| geom | geometry(LineString,4326) | траектория обхода |
| indoor_level_universal_id | text | *indoorLevelId* идентификатор здания (из НЯК) |
| distance| bigint | примерное расстояние обходa (в метрах) |
| duration| bigint | примерная длительность обходa (в секундах) |
| description| text | описание маршрута |

#### **ugc.assignment** 
Данная таблица описывает задание, взятое в работу

| **Column** | **Type** | **Description** |
| ---------- | -------- | --------------- |
| assignment_id| bigint | primary key |
| task_id| bigint |  идентификатор задания, к которому относится обход|
| status | ugc.assignment_status | active, abandoned, completed, accepted, revoked |
| assigned_to | text | идентификатор пользователя, который взял задание в работу |
| acquired_at| timestamp with time zone | время, когда задание взято в работу |
| expires_at| timestamp with time zone | дедлайн сдачи задания |
| submitted_at| timestamp with time zone | время, когда задание было выполнено |

#### **ugc.assignment_task_path**
Данная таблица описывает информацию о прохождении маршрута пользователем

| **Column** | **Type** | **Description** |
| ---------- | -------- | --------------- |
| assignment_task_path_id| bigint | primary key |
| assignment_id| bigint | идентификатор принятого в работу задания |
| task_id | bigint | идентификатор базового задания |
| task_path_id | bigint | идентификатор обхода |
| status| ugc.assignment_task_path_status | active, accepted, rejected, abandoned |
| reason| text | комментарий |

#### **ugc.assignment_task_path_track** 
Данная таблица описывает результат выполнения задания

| **Column** | **Type** | **Description** |
| ---------- | -------- | --------------- |
| assignment_task_path_track_id| bigint | primary key |
| assignment_task_path_id| bigint | идентификатор |
| s3_id | text | идентификатор ресурса в s3, который является proto файлом с собранными сенсорами и сигналами |
| complete_ratio | double precision | прогресс пройденного пути |
| comment| timestamp with time zone | комментарий, если пройти целый маршрут было невозможно |

### Алгоритм восстановления позиций маяков
Весь процесс описан тут: [Ссылка на wiki](https://wiki.yandex-team.ru/maps/dev/core/indoor/mexanizm-vosstanovlenija-pozicijj-majakov/)


## Known clients
- https://abc.yandex-team.ru/services/maps-core-mobile/

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stable | ????? |
| Testing | ????? |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_INDOOR_RADIOMAP_CAPTURER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_INDOOR_RADIOMAP_CAPTURER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_INDOOR_RADIOMAP_CAPTURER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_INDOOR_RADIOMAP_CAPTURER_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSCORE?service=maps-
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/????
    * Тикет: https://st.yandex-team.ru/MAPSCORE-???


[juggler-all-checks]: https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-indoor-radiomap-capturer
[juggler-psql-to-yt]: https://juggler.yandex-team.ru/check_details/?host=solomon-alert&service=nmaps_dynamic_replica_indoor_ugc&query=
[solomon-psql-to-yt]: https://solomon.yandex-team.ru/admin/projects/maps-nmaps/alerts/b9d385a9-2256-4286-bfa8-9eb41c4bdcdb
[solomon-tm-replication-dashboard]: https://solomon.yandex-team.ru/?project=data-transfer&cluster=rtc-prod&dashboard=transfer_dashboard&l.resource_id=*dtt687otl2c2vnhsaakk&l.source_type=pg&l.target_type=yt&l.source_id=mdba24p00o7ufj5gpskv&l.target_id=hahn--home-maps-nmaps-dynamic-replica-indoor-ugc
[tm]: https://yc.yandex-team.ru/folders/foo0a4665021doa6pr7s/data-transfer/transfers
