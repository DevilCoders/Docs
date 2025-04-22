## Тестирование Darkspirit с помощью Docker compose
 
### Пререквизиты
 * Docker (docker engine ver. >= 18.06.0)
 * Docker-compose
 * SSH ключи добавлены на staff
 * Залогин в яндексовом [Docker Disrtibution](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)
    * Если у вас Mac и не получается настроить oauth-аутентификацию - прочтите [это](https://github.com/docker/for-mac/issues/3774#issuecomment-582005196)

### Проверка миграций БД, работа со схемой
1. СУБД поднимается в сервисе `db`
2. Миграции накатываются зависящим от него "сервисом" `db-migrate`

* В рамках старта сервиса `db` также создается пользователь БД `ds` при помощи 
  [setup-скрипта](./db/setup/01_create_user.sql)
  * Состояние БД сохраняется в папке `db_volume` в корневой директории проекта, для быстрого рестарта сервиса.
    При необходимости обнулить БД нужно удалить эту директорию. 
* Для накатки миграций используется тот же инструмент, что используют DBA в продакшн: 
  [pyliquibase](https://a.yandex-team.ru/arc/trunk/arcadia/billing/balance/sql-liquibase/py)
  * Пакет с `pyliquibase` собран из [PR](https://a.yandex-team.ru/review/1249160/files/1) с правилами для сборки 
    (и исправлением нескольких багов)
* Сервис `db-migrate` дожидается успешного запуска базы через проверку успешного подключения 
  пользователем `ds` при помощи [wait-скрипта](./darkspirit/deploy/usr/bin/wait-for-dbuser)

#### Запуск
```bash
$ docker-compose run db-migrate
Starting darkspirit_db_1 ... done
...
+ wait-for-dbuser --user ds --password tiger --dsn //db:1521/XEPDB1
INFO:__main__:DB is not ready  
...
+ pyliquibase --changelogdir=/sql --changelogfile=changelog.xml --driver=DBOracle --username=ds --password=tiger --dsn=//db:1521/XEPDB1 --defaultSchemaName=ds --contexts=local update
2020-05-08 09:12:18,859: /usr/local/lib/python2.7/dist-packages/liquibase/dbtools.pyc [INFO] Connection to //db:1521/XEPDB1 established.
...
2020-05-08 09:12:20,599: /usr/local/lib/python2.7/dist-packages/liquibase/dbtools.pyc [DEBUG] Database connection closed.
$
```

#### Подключение изнутри Docker compose
```bash
$ docker-compose exec db bash
# Внутри интерактивной bash сессии
$ sqlplus ds/tiger@//localhost:1521/XEPDB1

SQL*Plus: Release 11.2.0.2.0 Production on Fri May 8 09:42:47 2020

Copyright (c) 1982, 2011, Oracle.  All rights reserved.


Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

SQL>
```

#### Подключение снаружи через port forwarding
На примере `sqlplus`:

```bash
$ sqlplus ds/tiger@//localhost:15210/XEPDB1

SQL*Plus: Release 19.0.0.0.0 - Production on Fri May 8 12:44:47 2020
Version 19.3.0.0.0

Copyright (c) 1982, 2019, Oracle.  All rights reserved.


Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production
```

N.B. Рекомендую утилиту [rlwrap](https://linux.die.net/man/1/rlwrap) при работе с `sqlplus`
  для использования истории и редактирования введённого в prompt. 

### Запуск тестов изнутри Docker compose
Тесты запускаются в "сервисе" `tests`

* 4. Скопировать секреты для доступа в MDS из YaVault: [secrets](../secrets/README.md)

* Сервис `tests` дожидается:
  * успешного запуска базы через проверку успешного подключения пользователем `ds` при помощи скрипта
   [wait-for-dbuser](./darkspirit/deploy/usr/bin/wait-for-dbuser);
  * успешного применения миграций через проверку специального `changeset` в
  [footer.sql](../sql-liquibase/sql/DS/footer.sql), который применяется последним, при помощи скрипта
   [wait-for-migrate](./darkspirit/deploy/usr/bin/wait-for-migrate);

#### Запуск тестов с нуля
```bash
$ docker-compose run -d db-migrate  # Если БД уже налита - можно пропустить этот шаг
Creating network "darkspirit_default" with the default driver
Creating darkspirit_db_1 ... done
darkspirit_db-migrate_run_3d494e6275ff
$ docker-compose run tests
...
+ wait-for-dbuser --user ds --password tiger --dsn //db:1521/XEPDB1
...
+ wait-for-dbmigrate --user ds --password tiger --dsn //db:1521/XEPDB1
...
+ py.test --application-config-file application-test-docker.cfg.xml tests
...
===================================================================== 21 passed, 62 warnings in 145.07 seconds ======================================================================
```

### Локальный запуск тестов поверх БД в Docker compose
* Поднимаем контейнеры с зависимостями (можно сделать один раз и гонять тесты сколько нужно):
```bash
docker-compose up -d db db-migrate tvmtool
```
* Запускаем тесты локально, как обычно, по инструкции из [README.md](../tests/README.md) тестов
* Для использования локальной БД передаем в тесты аргумент `--application-config-file application-test-local.cfg.xml`

```bash
(venv2) [prez@OSX ~/work/darkspirit (docker-compose *)]$ py.test --application-config-file application-test-local.cfg.xml tests
...
===================================================================== 21 passed, 62 warnings in 148.42 seconds ======================================================================
```

Таким же образом можно настроить и запуск из IDE, например для PyCharm нужно настроить конфигурацию запуска следующим образом:
* Additional Arguments: --application-config-file application-test-local.cfg.xml
* Python Interpreter: Project Default (virtualenv с зависимостями для DarkSpirit и самим DarkSpirit)
* Переменные окружения как указано в [README.md](../tests/README.md)
* Working Directory: /path/to/darkspirit (обязательно корневая директория проекта)

### Запуск сервиса darkspirit
Обычный запуск:
```bash
docker-compose up -d darkspirit
```
Debug запуск с автоматической перезагрузкой flask кода по мере его изменения:
```bash
FLASK_DEBUG=1 docker-compose up -d darkspirit
```

API будут доступны через localhost и порт указанный в `docker-compose.yml` файле


## Сборка релизной версии

Для этого есть Makefile в корне проекта:

```bash
make push_image version=0.666
```

Будет произведена сборка базового образа, а также
сборка релизной версии, на основе этого базового образа,
создан тег и отправлен в репозиторий.

## Выкатка релизной версии

Для этого в задачах Makefile есть две задачи: **deploy_testing** и
**deploy_stable** - они создают релизные тикеты Deploy двух типов. Тестинг
реагирует на оба тикета, продакшен только на второй.

Т.е. запуск вот этого:

```bash
make -o push_image deploy_stable version=0.666
```

Приведет к созданию тикета, который Deploy может накатить.
Естественно, что автоматом на stable ничего не накатится,
и правило будет настроено с политикой подтверждений.
