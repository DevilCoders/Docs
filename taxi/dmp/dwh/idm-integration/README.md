# idm_integration.
Проект для выдачи прав до:
1. Tableau - выдаются лицензии, как для Такси, так и для Еды:
    1. Viewer
    2. Explorer
    3. Creator
2. География
    1. Все регионы
    2. Операционная иерархия
    3. Финансовая иерархия
3. Greenplum
4. SSAS кубы

УРЛ до системы в IDM: https://idm.yandex-team.ru/system/taxi-dwh-idm-integration/  
ABC-сервис: https://abc.yandex-team.ru/services/taxidwhidmintegration/
Ссылка на описание в вики: <потом добавить сюда>

Небольшая схема по сервису:
![Небольшая схема по сервису:](https://jing.yandex-team.ru/files/pshevtsov/IDM.png)

## Ссылка на разморозку лицензии Таблё всегда одинакова для всех
https://dwh-idm-integration.taxi.yandex-team.ru/unsuspend-tableau-license/  
https://dwh-idm-integration.taxi.yandex.net/unsuspend-tableau-license/

## Сборка.
Сборка производится командой:
```
sudo docker build --cgroup-parent docker -f app/Dockerfile.testing -t registry.yandex.net/taxi-dwh/idm-integration-test:0.18 app/
```

Отправить в докер-репозиторий Яндекса:
```
sudo docker push registry.yandex.net/taxi-dwh/idm-integration-test:0.16
```

Запустить контейнер локально:
```
sudo docker run --cgroup-parent docker --name test01 -p 5002:80 registry.yandex.net/taxi-dwh/idm-integration-test:0.31
```

## Выкладка
1. Собрать докер образ через sandbox, предварительно настроив нужные параметры (ветка в гите, версия образа и тд):
  1. Sandbox таска для выкладки докер образа на тестовое окружение: https://sandbox.yandex-team.ru/task/446112456/view
  2. Sandbox таска для выкладки докер образа на продовое окружение: https://sandbox.yandex-team.ru/task/445956685/view
2. Зайти по ссылке: https://platform.yandex-team.ru/projects/taxi-tools/taxi-dwh-idm-integration/{testing, stable} и нажать там Update, выбрав нужную версию для раскатки.
3. Выбрать нужную версию образа и нажать Update

## Логи.
1. yabs-graphite-client
    + ```/var/log/yandex/graphite-client/graphite-client.log```
    + ```/var/log/yandex/graphite-client/graphite-sender.log```
2. Веб-приложения
    + ```/var/log/yandex/idm_integration/flask_idm_integration.log.tskv```
3. Логи работы контейнера:
    + ```tail -f -n 10 run/qloud/app.stderr```
4. Docker logs: 
    + ```/var/log/upstart/docker.log```
5. Логи из контейнеров также пишутся ещё в PGaaS. Таблица log.python_log
6. Логи приложения в тестовой кибане: индекс = taxi-dwh-* https://kibana7.taxi.tst.yandex-team.ru/
7. Логи приложения в продовой кибане: индекс = taxi-dwh-qloud-* https://kibana.taxi.yandex-team.ru
    + чтобы найти в продовой кибане логи приложения, нужно поставить фильтр ```application: idm_integration```
8. Логи отправки данных в графит:
   + ```/var/log/yandex/idm_integration/send_license_info.log```
   + ```/var/log/yandex/idm_integration/send_unsuspend_info.log```

Логи внутри контейнера хранятся 14 дней (используется стандартный питоновский log-rotate). Если выложили новую версию контейнера - то все записанные ранее логи теряются.
  
Так как используется яндекс платформа, то можно посмотреть логи на YT.
```
use hahn;

SELECT
    *
FROM
    [//home/logfeller/logs/qloud-runtime-log/stream/5min/2018-11-23T13:55:00]
WHERE 
    qloud_application = `taxi-dwh-idm-integration`
    AND qloud_environment = `stable`
    AND qloud_project = `taxi-tools`
LIMIT 100;
```  

## Дашборды и графики
1. Дашборд по лицензиям в Tableau: https://grafana.yandex-team.ru/d/oVFwWkQiz/tableau-licenses?refresh=1h&orgId=1
2. Дашборд по работе сервиса: https://grafana.yandex-team.ru/d/Mz9qdLYik/taxi_qloud-ext-taxi-tools-taxi-dwh-idm-integration-stable-backend?refresh=30s&orgId=1
3. Дашборд по работоспособности прод-сервера Tableau: https://grafana.yandex-team.ru/d/ylhqtiHZz/tableau-prod-server-metrics
4. Дашборд по работоспособности тест-сервера Tableau: https://grafana.yandex-team.ru/d/mB6zY54Wz/tableau-test-server-metrics
5. Дашборд для анализа логов в прод Кибане: https://kibana.taxi.yandex-team.ru/goto/2a3cb52bf5806eac4b00ceb612d2410c

## Конфиги.
Общие конфиги лежат здесь: app/settings/common_settings.yaml (test/prod)
Также используется секретница для хранения паролей, логинов и тд.
1. Для продакшен окружения:
    + https://platform.yandex-team.ru/secrets/secret.taxi-dwh-idm-secret-settings
    + https://platform.yandex-team.ru/secrets/secret.taxi-dwh-idm-yt-token
2. Для тестового окружения:
    + https://platform.yandex-team.ru/secrets/secret.testing-taxi-dwh-idm-secret-settings
    + https://platform.yandex-team.ru/secrets/secret.taxi-dwh-idm-yt-token-test

Доступ до этих секретов имеют все, кто входит в группу на стаффе: https://staff.yandex-team.ru/departments/yandex_mrkt_analytics_serv_taxi_3499/

Секретный файл имеет структуру вида:
```
PGaaS:
    user: `taxi_test_dwhidm`
    password: `ENTER PASSWORD HERE`
Tableau:
    user: `robot-taxi-tableau`
    password: `ENTER PASSWORD HERE`
SSAS:
    user: `someuser`
    password: `somepassword`
```
Ссылка на файл: https://github.yandex-team.ru/taxi-dwh/idm-integration/blob/master/app/settings/secret_settings.yaml.example

Логины, пароли и тд и тп лежат в секретнице:
1. secret_idm: https://yav.yandex-team.ru/secret/sec-01dghq41py1z32yx9z27zvwct5/explore/versions
2. robot-taxidwh-idm: https://yav.yandex-team.ru/secret/sec-01d6js21bxfsem049saykp77mc/explore/versions
3. pgaas_idm_prod: https://yav.yandex-team.ru/secret/sec-01d68m00tg5zn712xxzjv2733m/explore/versions
4. pgaas_idm_test: https://yav.yandex-team.ru/secret/sec-01d68kx9xdmr70djksjbds3sbb/explore/versions

	
## Роботные пользователи.
1. Тестовая среда:
    + robot-taxi-tableau - для похода в Tableau
    + taxi_dwhidm - для похода в PGaaS
    + robot-taxi-heimdallr - для похода в GP
2. Продовая среда:
    + robot-taxi-tableau - для похода в Tableau
    + taxi_dwhidm - для похода в PGaaS
    + robot-taxi-gp-usrman - для похода в GP
    + robot-taxidwh-idm - под этим пользователем отбираются роли. Т.е. этот робот имеет роль в ИДМ: "Исполнитель чужой роли"
    

## PGaaS
Тестовая среда:
  + Пользователь: taxi_test_dwhidm
  + БД: taxi_test_db_dwhidm_shard0
  + урл: pgaas-test.mail.yandex.net

Продовая среда:
  + Пользователь: taxi_dwhidm
  + БД: taxi_db_dwhidm_shard0
  + урл: pgaas.mail.yandex.net

  
## YT
В данный момент в YT ходим за даннымив таблицу ```//home/taxi-dwh/raw/dim_geo_hierarchy/dim_geo_hierarchy``` на Hahn`е. Это для синхронизации гео-иерархии.

 
## Отправка в графит.
https://st.yandex-team.ru/TAXIDWH-1654
Нужные пакеты: ```yabs-graphite-sender``` и ```yabs-graphite-client```
Сама отправка идёт через крон раз в 63 минуты.
Исполняемый файл по отправке: ```app/cron/send_license_info```


## Реализованные методы
1. Для интеграции с IDM. Более подробное описание: https://wiki.yandex-team.ru/intranet/idm/API/
    1. ```/info/``` [get]
    2. ```/get-all-roles/``` [get]
    3. ```/add-role/``` [post]
    4. ```/remove-role/```
2. ```/sync-geo-roles/``` [get] - синхронизация гео-ролей YT->PGaaS
3. ```/active-roles/``` [get] - для синхрониции пользователей между PGaaS и gpdb-bouncer`а
4. ```/unsuspend-tableau-license/``` [get] - для разморозки лицензии в Таблё.


## Полезные ссылки
1. Работа с ИДМ через апи: https://wiki.yandex-team.ru/intranet/idm/API/public/
2. Запуск приложения в Qloud на основе базового образа: https://wiki.yandex-team.ru/taxi-ito/baseqloudimage/
3. Ручная сборка и выкатка docker в qloud: https://wiki.yandex-team.ru/taxi-ito/Manual-assembly-and-rollout-docker-in-qloud/
4. Инфраструктура и эксплуатация Я.Такси: https://wiki.yandex-team.ru/taxi-ito/
5. Описание как подключаться к ИДМ: https://doc.yandex-team.ru/idm/idm-guide/concepts/add-system-to-idm.html
6. Форма для подключения к ИДМ: https://wiki.yandex-team.ru/Intranet/idm/new/request/
7. Токен для публичного АПИ ИДМа: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=b222f0730d124c24aa379253d9a079c2
8. tvm-qloud-post https://wiki.yandex-team.ru/users/e-sidorov/tvm-qloud-post/
9. Как завести TVM в QLOUD: https://wiki.yandex-team.ru/edadeal/development-philosophy/edadeal-in-qloud/tvm-qloud/
10. TVM: https://wiki.yandex-team.ru/qloud/doc/secrets/tvm/
11. Проверка TVM2-тикетов: https://wiki.yandex-team.ru/intranet/idm/security/tvm/

## Основные тикеты по разработке:
1. https://st.yandex-team.ru/TAXIDWH-1325
2. https://st.yandex-team.ru/TAXIDWH-1640
3. https://st.yandex-team.ru/TAXIDWH-1985


## Разное
1. Чтобы можно было выполнять запросы по апи в Таблё - у пользователя (под которым авторизуемся) должны быть такие настройки в AD:
 Заменил группу у робота NoLogonUsers на NoInteractiveLogonUsers
2. Настройка ДатаГрипа, чтобы работало нормально с Пегасом:
 Если после соединения возникает ошибка ("prepared statement s_3 does not exist"), то добавить 
 ?prepareThreshold=0 в URL connection string https://confluence.atlassian.com/crowdkb/crowd-crashes-due-to-psqlexception-error-prepared-statement-s_1-does-not-exist-729482785.html
3. Как получить нужную подсеть IPV6 для следующего шага: https://wiki.yandex-team.ru/zen/tech/devichwill/docker/
4. Как настроить докер в IPV6 only: https://wiki.yandex-team.ru/mobilesearch/app/android/avtomaticheskietestyinfrastruktura/#izvestnyeproblemy
5. https://docs.platform.yandex-team.ru/doc/starter/
6. https://wiki.yandex-team.ru/qloud/docker-registry/
7. Ссылка на вики пилорамы: https://wiki.yandex-team.ru/taxi/backend/architecture/pilorama/

## Примеры как курлить :)
### Тестируем ручку sync-geo-roles

На разработческой машинке:
```curl -i -X GET -d  -H "application/x-www-form-urlencoded" -L -k http://etl-myt-02.taxi.dev.yandex.net:5003/sync-geo-roles/```

Из под контейнера:
```curl -i -X GET -d  -H "application/x-www-form-urlencoded" -L -k https://dwh-idm-integration.taxi.tst.yandex.net/sync-geo-roles/```

### Тестируем шафлинг лицензий:
```curl -i -X POST -d "path=/taxi_dwh_analytics/tableau_analyst/tableau_subgroups/license/role/viewer/&login=vverstov&role={\"tableau_subgroups\": \"license\", \"taxi_dwh_analytics\": \"tableau_analyst\", \"role\": \"viewer\"}" -H "application/x-www-form-urlencoded" -L -k http://etl-myt-02.taxi.dev.yandex.net:5003/add-role/```

```curl -i -X POST -d "path=/taxi_dwh_analytics/tableau_analyst/tableau_subgroups/license/role/viewer/&login=nikmort&role={\"tableau_subgroups\": \"license\", \"taxi_dwh_analytics\": \"tableau_analyst\", \"role\": \"viewer\"}" -H "application/x-www-form-urlencoded" -L -k http://etl-myt-02.taxi.dev.yandex.net:5003/add-role/```

```curl -i -X POST -d "path=/taxi_dwh_analytics/tableau_analyst/tableau_subgroups/license/role/viewer/&login=vgurbatova&role={\"tableau_subgroups\": \"license\", \"taxi_dwh_analytics\": \"tableau_analyst\", \"role\": \"viewer\"}" -H "application/x-www-form-urlencoded" -L -k http://etl-myt-02.taxi.dev.yandex.net:5003/add-role/```

### 

## Запуск на разработческой машинке
```
sudo docker run --cgroup-parent docker --name test01 -p 5002:80 registry.yandex.net/taxi-dwh/idm-integration-test:0.31
```

### Подключиться к bash'у контейнера
```
sudo docker exec -it test01 bash
```
