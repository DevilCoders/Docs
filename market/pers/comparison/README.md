# pers-comparison

### Описание

Работа со сравнениями

Переезжает от https://github.yandex-team.ru/market-java/pers-notify

[Памятка дежурному](https://wiki.yandex-team.ru/market/development/pers/duty/)

[Памятка разработчику](https://wiki.yandex-team.ru/users/varvara/market/development/pers/)

[API тестинг](http://pers-comparison.tst.vs.market.yandex.net/swagger-ui.html)

### Выкладка (RTC)

[Релизная машина](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/pers-comparison)

[Выкладка из ветки в тестинг](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/pers-comparison-branch)

Проверку доработок желательно делать до вливания в транк - через выкатку из бранчи.
Нужно указывать путь пользовательской ветки в арке `users/user_name/branch_name` или `trunk` для выкатки из транка.

При выкатке релиза из транка нужно зайти в релизную машину, и из неё запустить релиз нужной ревизии.

### Nanny

[Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_comparison/)

Логи в nanny по пути ```logs/pers-comparison/pers-comparison.log```

Секретница:
- [тест](https://yav.yandex-team.ru/secret/sec-01eh6z0vtkneygnc88a74c023z/explore/versions)
- [прод](https://yav.yandex-team.ru/secret/sec-01eh6z0tw8axfsqdvpgxf9tgzt/explore/versions)

После изменения секрета можно накатить его через `persec comparison test/prod`

### Графики сервиса

[Графана](https://grafana.yandex-team.ru/d/5bkQabTMk/pers-comparison?orgId=1)

[Solomon](https://solomon.yandex-team.ru/admin/projects/market-pers-comparison)

[proto прод](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketperscomparison;ctype=PRODUCTION;prj=market/)

[proto тесмтинг](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketperscomparison;ctype=testing;prj=market/)

[nginx прода](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketperscomparison;ctype=production;prj=market/)

[nginx тестинга](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketperscomparison;ctype=testing;prj=market/)


### База

### postgres

[управление прод](https://yc.yandex-team.ru/folders/fooqc51fitontalf6vjl/managed-postgresql/cluster/mdbgums1ocen6ik3r4bn)

[управление тестинг](https://yc.yandex-team.ru/folders/fooqc51fitontalf6vjl/managed-postgresql/cluster/mdb3f5ju5o2pjbu6o69l)

[yasm база прод](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbgums1ocen6ik3r4bn;dbname=pers_comparison_production)

[yasm база тестинг](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb3f5ju5o2pjbu6o69l;dbname=pers_comparison_testinng)

[solomon база прод](https://solomon.yandex-team.ru/?cluster=mdb_mdbgums1ocen6ik3r4bn&project=internal-mdb&service=mdb&dashboard=internal-mdb-cluster-postgres)

[solomon база тест](https://solomon.yandex-team.ru/?cluster=mdb_mdb3f5ju5o2pjbu6o69l&project=internal-mdb&service=mdb&dashboard=internal-mdb-cluster-postgres)


### Liquibase

Liquibase накатывается в пайплайне релиза.
Также можно использовать скрипт `liquibase.sh`

Для использования скрипта нужно настроить переменные окружения (~/.bashrc)
Переменные можно взять из [секретницы](https://yav.yandex-team.ru/secret/sec-01ewjaqytmm5sas6bss1whahv4/explore/versions)
```
export COMPARISON_DB_PWD_TEST=<значение из pers-датасорцов>
export COMPARISON_DB_PWD_PROD=<значение из pers-датасорцов>
```

Формат `./liquibase.sh <env> <command>`
- `<env>` - среда: dev, test, prod
- `<command>` - команда liquibase: updateSQL, update, ...

Пример: `./liquibase.sh dev update`


## Сборка и запуск

Сборка и прогон тестов `ya make -tt`

Локальный запуск можно сделать напрямую и через скрипт. Подробности в [документации](https://wiki.yandex-team.ru/users/ilyakis/maret-java-arcadia-migration/#lokalnyjjzapusk)

**Важно**: для локального запуска нужно поднять локальную БД postgresql pers_comparison_db - логин-пароль в конфигах.
```
# sudo -u postgres psql
CREATE DATABASE pers_comparison_db;
CREATE USER pers_comparison WITH ENCRYPTED PASSWORD 'pers_comparison';
GRANT ALL PRIVILEGES ON DATABASE pers_comparison_db TO pers_comparison;
```

[Локальный сваггер](http://localhost:8080/swagger-ui.html)

#### Локальный запуск через скрипт
Запуск приложения
```
# простой запуск
./local-start.sh

# в режиме отладки
./local-start.sh --debug-port=6666
```

#### Локальный запуск напрямую
Локальный запуск - через класс `PersComparison`
Переменные окружения
```
ENVIRONMENT=local
```

JMV args
```
# если хочется, чтобы логи выводились в консоль
-Dlog4j.configurationFile=/home/#USER/arc/arcadia/market/pers/comparison/src/main/conf/local/log4j2-test.xml
```
