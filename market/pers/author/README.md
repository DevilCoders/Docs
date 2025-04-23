# pers-author

### Описание

[Памятка дежурному](https://wiki.yandex-team.ru/market/development/pers/duty/)

[Памятка разработчику](https://wiki.yandex-team.ru/users/varvara/market/development/pers/)

[API тестинг](https://pers-author.tst.vs.market.yandex.net/swagger-ui.html#/)

### Выкладка

[Релиз из транка](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/pers-author)

[Выкладка в тестинг из ветки](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/pers-author-branch)

Проверку доработок желательно делать до вливания в транк - через выкатку из бранчи.
Нужно указывать путь пользовательской ветки в арке `users/user_name/branch_name` или `trunk` для выкатки из транка.

При выкатке релиза из транка нужно зайти в релизную машину, и из неё запустить релиз нужной ревизии.

### RTC

[Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_author/)

Логи в ```logs/pers-author/pers-author.log```

Секретница:
- [тест](https://yav.yandex-team.ru/secret/sec-01dyj5b0mwqqvkjs9p7geb05y6/explore/versions)
- [прод](https://yav.yandex-team.ru/secret/sec-01dyj5b01dptsa3vs3xfas2aj9/explore/versions)

После изменения секрета можно накатить его через `persec author test/prod`

### Графики сервиса

[Графана](https://grafana.yandex-team.ru/d/2xFnxdXWk/pers-author?orgId=1&refresh=30s)

[Solomon](https://solomon.yandex-team.ru/admin/projects/market-pers-author)

[nginx прод](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketpersauthor;ctype=production;prj=market/)

[nginx тестинг](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketpersauthor;ctype=testing;prj=market/)

[proto прод](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketpersauthor;ctype=production;prj=market/)

[proto тестинг](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketpersauthor;ctype=testing;prj=market/)

### SAAS

[Метрики saas](https://saas-mon.n.yandex-team.ru/monitor/?service=market_pers_author&ctype=stable_kv)

### Базы

Параметры бызы в [секретнице](https://yav.yandex-team.ru/)

[график yasm прод](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbr3ndvjgf05ta91ghj;dbname=market_pers_author_prod)

[график yasm тестинг](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbsgdmo763cp46soc1n;dbname=market_pers_author_test)

[график solomon прод](https://solomon.yandex-team.ru/?cluster=mdb_mdbr3ndvjgf05ta91ghj&project=internal-mdb&service=mdb&dashboard=internal-mdb-cluster-postgres)

[график solomon тест](https://solomon.yandex-team.ru/?cluster=mdb_mdbsgdmo763cp46soc1n&project=internal-mdb&service=mdb&dashboard=internal-mdb-cluster-postgres)

[управление прод](https://yc.yandex-team.ru/folders/fooqc51fitontalf6vjl/managed-postgresql/cluster/mdbr3ndvjgf05ta91ghj)

[управление тест](https://yc.yandex-team.ru/folders/fooqc51fitontalf6vjl/managed-postgresql/cluster/mdbsgdmo763cp46soc1n)

### Liquibase

Liquibase накатывается в пайплайне релиза.
Также можно использовать скрипт `liquibase.sh`

Для использования скрипта нужно настроить переменные окружения (~/.bashrc)
```
export AUTHOR_DB_PWD_TEST=<значение из pers-датасорцов>
export AUTHOR_DB_PWD_PROD=<значение из pers-датасорцов>
```

Формат `./liquibase.sh <env> <command>`
- `<env>` - среда: dev, test, prod
- `<command>` - команда liquibase: updateSQL, update, ...

Пример: `./liquibase.sh dev update`

### Сборка и запуск

Сборка и прогон тестов `ya make -tt`

Локальный запуск можно сделать напрямую и через скрипт. Подробности в [документации](https://wiki.yandex-team.ru/users/ilyakis/maret-java-arcadia-migration/#lokalnyjjzapusk)

**Важно**: для локального запуска нужно поднять локальную БД postgresql pers_author_db - логин-пароль в конфигах.

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
Локальный запуск - через класс `PersAuthor`
Переменные окружения
```
ENVIRONMENT=local
```

JMV args
```
# если хочется, чтобы логи выводились в консоль
-Dlog4j.configurationFile=/home/#USER/arc/arcadia/market/pers/author/src/main/conf/local/log4j2-test.xml
```
