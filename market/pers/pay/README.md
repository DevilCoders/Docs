# pers-pay
Вы пишете отзывы - мы вам за это благодарны, и делимся баллами в плюсе.

### Описание

[Памятка дежурному](https://wiki.yandex-team.ru/market/development/pers/duty/)

[Памятка разработчику](https://wiki.yandex-team.ru/users/varvara/market/development/pers/)

[API тестинг](https://pers-pay.tst.vs.market.yandex.net/swagger-ui.html#/)

### Выкладка

[Релиз из транка](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/pers-pay)

[Выкладка в тестинг из ветки](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/pers-pay-branch)

Проверку доработок желательно делать до вливания в транк - через выкатку из бранчи.
Нужно указывать путь пользовательской ветки в арке `users/user_name/branch_name` или `trunk` для выкатки из транка.

При выкатке релиза из транка нужно зайти в релизную машину, и из неё запустить релиз нужной ревизии.

### RTC

[Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_pay/)

Логи в ```logs/pers-pay/pers-pay.log```

Секретница:
- [тест](https://yav.yandex-team.ru/secret/sec-01ezyvg748n44zm6bkjhjs2fbd/explore/versions)
- [прод](https://yav.yandex-team.ru/secret/sec-01ezyvg81tpsb2me9838kxg16j/explore/versions)

После изменения секрета можно накатить его через `persec pay test/prod`

### Графики сервиса

[Графана](https://grafana.yandex-team.ru/d/NmD-7_QGk/pers-pay?orgId=1&refresh=30s)

[Solomon](https://solomon.yandex-team.ru/admin/projects/market-pers-pay)

[nginx прод](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketpersperspay;ctype=production;prj=market/)

[nginx тестинг](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketpersperspay;ctype=testing;prj=market/)

[proto прод](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketperspay;ctype=production;prj=market/)

[proto тестинг](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketperspay;ctype=testing;prj=market/)

[Статистика по платным отзывам](https://grafana.yandex-team.ru/d/slSlY-rMk/pers-pay-stats?orgId=1&refresh=1m&from=now-7d&to=now)

### Базы

Параметры бызы в [секретнице](https://yav.yandex-team.ru/)

[график yasm прод](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbqivcovldg19k4vce2;dbname=market_pers_pay_prod)

[график yasm тестинг](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb19nphpkm1vd0k5evf;dbname=market_pers_pay_test)

[график solomon прод](https://solomon.yandex-team.ru/?cluster=mdb_mdbqivcovldg19k4vce2&project=internal-mdb&service=mdb&dashboard=internal-mdb-cluster-postgres)

[график solomon тест](https://solomon.yandex-team.ru/?cluster=mdb_mdb19nphpkm1vd0k5evf&project=internal-mdb&service=mdb&dashboard=internal-mdb-cluster-postgres)

[управление прод](https://yc.yandex-team.ru/folders/fooqc51fitontalf6vjl/managed-postgresql/cluster/mdbqivcovldg19k4vce2)

[управление тест](https://yc.yandex-team.ru/folders/fooqc51fitontalf6vjl/managed-postgresql/cluster/mdb19nphpkm1vd0k5evf)

### Liquibase

Liquibase накатывается в пайплайне релиза.
Также можно использовать скрипт `liquibase.sh`

Для использования скрипта нужно настроить переменные окружения (~/.bashrc)
```
export PAY_DB_PWD_TEST=<значение из pers-датасорцов>
export PAY_DB_PWD_PROD=<значение из pers-датасорцов>
```

Формат `./liquibase.sh <env> <command>`
- `<env>` - среда: dev, test, prod
- `<command>` - команда liquibase: updateSQL, update, ...

Пример: `./liquibase.sh dev update`

### Сборка и запуск

Сборка и прогон тестов `ya make -tt`

Локальный запуск можно сделать напрямую и через скрипт. Подробности в [документации](https://wiki.yandex-team.ru/users/ilyakis/maret-java-arcadia-migration/#lokalnyjjzapusk)

**Важно**: для локального запуска нужно поднять локальную БД postgresql
```
# sudo -u postgres psql для локального подключения к БД
CREATE DATABASE pers_pay_db;
CREATE USER pers_pay WITH ENCRYPTED PASSWORD 'pers_pay';
GRANT ALL PRIVILEGES ON DATABASE pers_pay_db TO pers_pay;
```

[Локальный сваггер](http://localhost:8080/swagger-ui.html)

#### Локальный запуск через скрипт
Для запуска нужно сохранить несколько секретов в перменные окружения (удобно в .bashrc, чтобы не вводить каждый раз)
```
export PAY_TVM_SECRET=<секрет из секретницы>
```


Запуск приложения
```
# простой запуск
./local-start.sh

# в режиме отладки
./local-start.sh --debug-port=6666
```

#### Локальный запуск напрямую
Локальный запуск - через класс `PersPay`
Переменные окружения
```
ENVIRONMENT=local
PAY_TVM_SECRET=<секрет из секретницы>
```

JMV args
```
# если хочется, чтобы логи выводились в консоль
-Dlog4j.configurationFile=/home/#USER/arc/arcadia/market/pers/pay/src/main/conf/local/log4j2-test.xml
```
