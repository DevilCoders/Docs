# pers-qa

### Описание

Бекэнд для работы с Q&A, а также комментариями

[Описание сервиса](https://wiki.yandex-team.ru/users/korolyov/Voprosy-Otvety/)

[Настройка модерации](https://wiki.yandex-team.ru/market/development/pers/qa/)

[Памятка дежурному](https://wiki.yandex-team.ru/market/development/pers/duty/)

[Памятка разработчику](https://wiki.yandex-team.ru/users/varvara/market/development/pers/)

### API (тестинг)
[Swagger для сервиса](http://pers-qa.tst.vs.market.yandex.net/swagger-ui.html)

[Админка](https://pers-qa-admin.tst.market.yandex-team.ru)

### Выкладка
[Релиз из транка](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/pers-qa-arc)

[Выкладка в тестинг из ветки](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/pers-qa-branch)

Проверку доработок желательно делать до вливания в транк - через выкатку из бранчи.
Нужно указывать путь пользовательской ветки в арке `users/user_name/branch_name` или `trunk` для выкатки из транка.

При выкатке релиза из транка нужно зайти в релизную машину, и из неё запустить релиз нужной ревизии.

### RTC дашборды
[Nanny pers-qa](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_qa/)

[Nanny pers-qa-admin](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_qa_admin/)

[Nanny pers-qa-tms](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_qa_tms/)

Секретница:
- [тест](https://yav.yandex-team.ru/secret/sec-01f33r2hezzhc12zth8gc418rc/explore/versions)
- [прод](https://yav.yandex-team.ru/secret/sec-01f33r7481maz2zv7yhsb7vc5q/explore/versions)

После изменения секрета можно накатить его через `persec qa test/prod`

### Выгрузки таблиц
Сервисом: https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/pers-qa&

Напрямую из БД: https://yt.yandex-team.ru/hahn/navigation?path=//home/cdc/market/production/pers-qa/tables

Описание: https://wiki.yandex-team.ru/market/development/pers/pers-tables/

### Графики qa
[Solomon](https://solomon.yandex-team.ru/admin/projects/market-pers-qa)

[Общие графики](https://grafana.yandex-team.ru/d/uTFttOHmk/pers-qa)

[nginx прода](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketpersqa;ctype=production;prj=market/)

[proto метрики прода](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketpersqa;ctype=production;prj=market/?range=21660000)

[Статистика по моделям](https://grafana.yandex-team.ru/d/RXbhz65iz/pers-qa-stats)

[Статистика по категориям](https://grafana.yandex-team.ru/d/_mzBtwjmz/pers-qa-stats-cat)


### Графики индексации
[Метрики индексации](https://grafana.yandex-team.ru/d/Y32pRg8mk/pers-qa-indexing-metrics)

[Метрики saas](https://saas-mon.n.yandex-team.ru/monitor/?ctype=stable&service=market-pers-qa&kind=proxy&dc=&allserv=)

[Метрики saas - по-машинкам](https://yasm.yandex-team.ru/chart/signals=%7Bquant(saas_unistat-times-stable-market-pers-qa_dhhh,50),quant(saas_unistat-times-stable-market-pers-qa_dhhh,90),quant(saas_unistat-times-stable-market-pers-qa_dhhh,95),quant(saas_unistat-times-stable-market-pers-qa_dhhh,97),quant(saas_unistat-times-stable-market-pers-qa_dhhh,98),quant(saas_unistat-times-stable-market-pers-qa_dhhh,99),quant(saas_unistat-times-stable-market-pers-qa_dhhh,999),const(120),const(100)%7D;hosts=ASEARCH;itype=searchproxy/?top_method=maxavg&top_signal=quant(saas_unistat-times-stable-market-pers-static_dhhh%2C50)&range=21600000)

[Графики топика LogBroker (прод)](https://logbroker.yandex-team.ru/main/topic/saas%2Fservices%2Fmarket-pers-qa%2Fstable%2Ftopics%2Fshard-0-65533/metrics?dc=all&scale=h&autorefresh=true)

[Графики топика LogBroker (тестинг)](https://logbroker.yandex-team.ru/main_prestable/topic/saas%2Fservices%2Fmarket-pers-qa%2Fprestable%2Ftopics%2Fshard-0-65533/metrics?dc=all&scale=h&autorefresh=true)

Графики 4хх и 5хх по всем способам индексации, 2хх через демона, количества инстансов демона с проблемной конфигурацией:

- [прод](https://yasm.yandex-team.ru/panel/vvolokh.pers-qa-saas-stable)
- [тестинг](https://yasm.yandex-team.ru/panel/vvolokh.pers-qa-saas-prestable)

### Графики базы
прод: https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=8878cdcc-f68a-4038-a1e4-67d84bd90e59;dbname=marketsercom2

тестинг: https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=ea880c4a-8594-40f7-b4a0-b7aa7cf9681a;dbname=marketsercom2_test

### Графики кэша
Прод:
- memcached - https://grafana.yandex-team.ru/d/000018137/market-memcached?refresh=1m&orgId=1&var-group=%25market_cache-stable&var-port=21238
- прокся - https://grafana.yandex-team.ru/d/000018053/market-mcrouter?refresh=1m&orgId=1&var-group=%25market_cache-stable&var-port=11238

Тестинг:
- memcached - https://grafana.yandex-team.ru/d/000018137/market-memcached?refresh=1m&orgId=1&var-group=%25market_cache-testing&var-port=21238
- прокся - https://grafana.yandex-team.ru/d/000018053/market-mcrouter?refresh=1m&orgId=1&var-group=%25market_cache-testing&var-port=11238

### Liquibase

Liquibase накатывается в пайплайне релиза.
Также можно использовать скрипт `liquibase.sh`

Для использования скрипта нужно настроить переменные окружения (~/.bashrc)
```
export QA_DB_PWD_TEST=<значение из dev датасорцов>
export QA_DB_PWD_PROD=<значение из dev датасорцов>
```

Формат `./liquibase.sh <env> <command>`
- `<env>` - среда: dev, test, prod
- `<command>` - команда liquibase: updateSQL, update, ...

Пример: `./liquibase.sh dev update`

### Сборка и запуск

Сборка и прогон тестов `ya make -tt`

Локальный запуск можно сделать напрямую и через скрипт. Подробности в [документации](https://wiki.yandex-team.ru/users/ilyakis/maret-java-arcadia-migration/#lokalnyjjzapusk)
В каждом из проектов есть локальные проперти `src/main/resources/properties.d/local/application-local.properties`.
Обычно они настроены достаточно для локального запуска сервиса, но могут быть исключения.

Где брать данные для запуска:
1. Секрет для TVM находится в [секретнице](https://yav.yandex-team.ru), в секрете PERS_TVM.
2. Токены и прочие секретные данные в [датасорцах](https://github.yandex-team.ru/cs-admin/datasources-ng-dev/blob/master/development/etcd.yml)

#### Локальная БД
Для локального запуска необходимо иметь установленную БД:
1. Установить локально PostgreSQL
2. Создать [новую БД и пользователя](https://wiki.yandex-team.ru/users/ilyakis/Prigoditsja/#lokalnajabdpostgresql-sozdanie)
3. Создать новый Data Source PostgreSQL внутри IDEA, прописав информацию из пункта 2
4. Выполнить sql в консоли базы из 3 пункта `sercom.original.sql`, потом `sercom.changelog.sql` (таблицы серкома, которых нет в liquibase Q&A)
5. Выполнить в терминале `./liquibase.sh dev update`


#### Локальный запуск через скрипт
Для запуска нужно сохранить несколько секретов в перменные окружения (удобно в .bashrc, чтобы не вводить каждый раз)
```
export QA_TVM_SECRET=<секрет из секретницы>
export QA_SERVICE_TVM_SECRET=<секрет из секретницы>
export QA_ADMIN_TVM_SECRET=<секрет из секретницы>
export YT_DEV_TOKEN=<взять dev токен к robot-pers-mds-dev из dev датасорцов>
```

Запуск приложения через скрипт `local-start.sh`, который есть в каждом из модулей (pers-qa, pers-qa-admin, pers-qa-tms)
```
# простой запуск
./local-start.sh

# в режиме отладки
./local-start.sh --debug-port=6666
```

#### Локальный запуск напрямую
Локальный запуск - через класс:
* pers-qa - `ru.yandex.market.pers.qa.ApplicationMainPersQA`
* pers-qa-admin - `ru.yandex.market.pers.qa.admin.ApplicationMainPersQaAdmin`
* pers-qa-tms - `ru.yandex.market.pers.qa.ApplicationMainPersQATms`

Переменные окружения, которые нужно ввести в конфигурации idea
```
ENVIRONMENT=local
host.name=localhost
QA_TVM_SECRET=<секрет из секретницы>
QA_SERVICE_TVM_SECRET=<секрет из секретницы>
QA_ADMIN_TVM_SECRET=<секрет из секретницы>
YT_DEV_TOKEN=<взять dev токен к robot-pers-mds-dev из dev датасорцов>
```

JMV args
```
# если хочется, чтобы логи выводились в консоль
-Dlog4j.configurationFile=/home/#USER/arc/arcadia/market/pers/qa/prs-qa/src/main/conf/local/log4j2-test.xml
```

### Запуск джобы

зайти на машинку pers-qa-tms и дернуть curl

`curl -X GET "localhost:8081/tms/run?task=sendNewTelegramAnswers"`

