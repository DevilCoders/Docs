# pers-basket

### Описание 

Вишлист пользователя

[Страница на Wiki](https://wiki.yandex-team.ru/market/development/pers/basketlist/)

[Памятка дежурному](https://wiki.yandex-team.ru/market/development/pers/duty/)

[Памятка разработчику](https://wiki.yandex-team.ru/users/varvara/market/development/pers/)

[API (тестинг)](http://pers-basket.tst.vs.market.yandex.net:34510/swagger-ui.html)

### Выкладка

[Релиз из транка](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/pers-basket-arc)

[Выкладка в тестинг из ветки](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/pers-basket-branch)

Проверку доработок желательно делать до вливания в транк - через выкатку из бранчи.
Нужно указывать путь пользовательской ветки в арке `users/user_name/branch_name` или `trunk` для выкатки из транка.

При выкатке релиза из транка нужно зайти в релизную машину, и из неё запустить релиз нужной ревизии.

### RTC

[Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_basket/)

Логи в ```logs/pers-pay/pers-pay.log```

Секретница:
- [тест](https://yav.yandex-team.ru/secret/sec-01f33rgvemc03w8mbes6jw0ww5/explore/versions)
- [прод](https://yav.yandex-team.ru/secret/sec-01f33rjfm9tz96bpdbw1q0egjz/explore/versions)

После изменения секрета можно накатить его через `persec basket test/prod`

### Графики

[Solomon](https://solomon.yandex-team.ru/admin/projects/market-pers-basket)

[Основные метрики pers-basket](https://grafana.yandex-team.ru/d/000010115/pers-basket?orgId=1)

[nginx прода](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketpersbasket;ctype=production;prj=market/)

[proto метрики прода](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketpersbasket;ctype=production;prj=market/?range=21660000)


### Графики базы
- [тестинг](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbnap2qksn9ilev398a;dbname=pers_basket_testing)
- [прод](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbelojljkrsf9vnnai2;dbname=pers_basket_production)


### Управление БД
- [Тестинг](https://yc.yandex-team.ru/folders/foonpvfuma884c21dkih/managed-postgresql/cluster/mdbnap2qksn9ilev398a)
- [Прод](https://yc.yandex-team.ru/folders/foonpvfuma884c21dkih/managed-postgresql/cluster/mdbelojljkrsf9vnnai2)


### Liquibase

Liquibase накатывается в пайплайне релиза.
Также можно использовать скрипт `liquibase.sh`

Для использования скрипта нужно настроить переменные окружения (~/.bashrc)
```
export BASKET_DB_PWD_TEST=<значение из dev датасорцов>
export BASKET_DB_PWD_PROD=<значение из dev датасорцов>
```

Формат `./liquibase.sh <env> <command>`
- `<env>` - среда: dev, test, prod
- `<command>` - команда liquibase: updateSQL, update, ...

Пример: `./liquibase.sh dev update`


### Сборка и запуск 

Сборка и прогон тестов `ya make -tt`

Локальный запуск можно сделать напрямую и через скрипт. Подробности в [документации](https://wiki.yandex-team.ru/users/ilyakis/maret-java-arcadia-migration/#lokalnyjjzapusk)

[Локальный сваггер](http://localhost:8080/swagger-ui.html)

#### Локальная БД
Для локального запуска необходимо иметь установленную БД:
1. Установить локально PostgreSQL
2. Создать [новую БД и пользователя](https://wiki.yandex-team.ru/users/ilyakis/Prigoditsja/#lokalnajabdpostgresql-sozdanie)
  - БД pers_basket_db
  - пользователь/пароль pers_basket
3. Создать новый Data Source PostgreSQL внутри IDEA, прописав информацию из пункта 2
4. Выполнить в терминале `./liquibase.sh dev update`


#### Локальный запуск через скрипт
Для запуска нужно сохранить несколько секретов в перменные окружения (удобно в .bashrc, чтобы не вводить каждый раз)
```
export BASKET_DB_PWD_TEST=<значение из dev датасорцов>
```

Запуск приложения
```
# простой запуск
./local-start.sh

# в режиме отладки
./local-start.sh --debug-port=6666
```

#### Локальный запуск напрямую
Локальный запуск - через класс `ru.yandex.market.pers.PersBasketMain`
Переменные окружения
```
ENVIRONMENT=local
```

JMV args
```
# если хочется, чтобы логи выводились в консоль
-Dlog4j.configurationFile=/home/#USER/arc/arcadia/market/pers/static/src/main/conf/local/log4j2-test.xml
```
