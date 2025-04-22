backend
=======

Бэкенд

Структура
=========

Почти классическая структура django приложения, с поправками на Аркадию.

Приложения расположены на одном уровне с проектом.

Чтобы не было `dcsaap/dcsaap/dcsaap` проект называется `backend`, а модуль
проекта называется `project` (где все настройки). В итоге получаем:

 - `dcsaap/backend/project` - путь для модуля с настройками
 - `dcsaap/backend/core` - путь к приложению `core`, где описаны основные модели
 - `dcsaap/backend/api` - путь к приложению `api`, где реализовано api проекта

Все зависимости прописаны в проекте (в том числе и приложения данного проекта):

- `dcsaap/backend/project/ya.make`


Основные комманды
=================

Сборка бинарника
----------------

```
$ make build
```

Появится `./manage/manage` полный аналог `manage.py` для обычного Django
проекта.

Создание миграции
-----------------

```sh
➜ make dev-mkmigrations APP=core
DCSAAP_DIR=`pwd` ./manage/manage makemigrations core
Migrations for 'core':
  core/migrations/0001_initial.py
    - Create model Check
```

В `APP` указываем приложение, для которого нужно создать миграцию

Запуск dev сервера
------------------

Соберет бинарник и запустит dev-сервер:

```
$ make dev-server
```

Накатить миграции
-----------------

Соберет бинарник и запустит миграции:

```
$ make dev-migrate
```

ipython для проекта
-------------------

Соберет бинарник и запустит ipython для проекта:

```
$ make ipython
```

Отлаживание тестов
------------------

Запустит тесты в режиме, в котором можно войти в pdb:
```
$ make debug-tests
```

Для того чтобы открыть pdb из нужной точки теста, в ней нужно послать себе `SIGUSR1`:
```python
import os, signal
os.kill(os.getpid(), signal.SIGUSR1)
```

### Отладка тестов в PyCharm

Есть возможность запука/отладки тестов через PyCharm. Для этого нужно сделать следующие приготовления:
- В директории `billing/dcsaap` запустить `ya ide pycharm`, сгенерируются соответсвуюшие бинарники-интерпретаторы для проекта, в том числе и для тестов.
- Убедиться, что `ya tool tvmknife` доступна и работает - утилита используется в некоторых тестах для создания тикетов.
- `Run -> Edit Configurations -> Edit configuration templates...`, выбираем `Python Tests`, `pytest`. Создадим базовый темплейт для запуска тестов, от него будут наследоваться конфигурации для запуска группы тестов или одного теста.

**Смотрим следующие поля**

Project:
```
billing-dcsaap-backend-tests-small
```

Python Interpreter:
```
Project Default (billing_dcsaap_backend_tests_small_billing-dcsaap-backend-tests-small)
```

Environment variables:
```
DJANGO_SETTINGS_MODULE=billing.dcsaap.backend.project.settings;
SOLOMON_TOKEN=xxx;
YOLO=da;
YA_TEST_RUNNER=true
```

**Запускаем**

Теперь можно попробовать запустить настроенную конфигурацию. Должен работать запуск тестов через кнопку рядом с функцией/классом.
Чтобы запустить все тесты нужно вручную создать конфигурацию, заполняем поля также как в темплейте,
в поле `Target(Module name)` пишем `small`. Если тесты падают с непонятной ошибой, то возможно что-то поменялось в структуре проекта и нужно еще раз запустить `ya ide pycharm`.



Полезности
==========

Как с локальной машины применить миграции в Deploy dev окружение?
----------------------------------------------------------------

Открываем окружение в Deploy:

- https://deploy.yandex-team.ru/stages/billing-dcs-dev-stage/

В Deploy получаем строку подключения для `app` в любом датацентре (`SAS`/`VLA`) (выпадающий список в таблице `FQDN`, `Host`, ...).
Копируем строку подключения и выполняем:

```bash
$ ssh root@billing-dcs-app.3e5navxtovx3b4sr.sas.yp-c.yandex.net "env | grep PG_DB"
PAYSYS_PG_DB_PASS=XXXX
PAYSYS_PG_DB_PORT=6432
PAYSYS_PG_DB_HOST=sas-usb28cf822kcr1jg.db.yandex.net
PAYSYS_PG_DB_USER=balance_dcs_dev
PAYSYS_PG_DB_NAME=balance_dcs_dev
```


В `Makefile`, в цели `dev-q-migrate` обновляем хост и пароль, после чего делаем:

```bash
$ make dev-q-migrate
ya make
Ok
DEPLOY_ENVIRONMENT='development' \
PAYSYS_PG_DB_PASS=xxxx \
PAYSYS_PG_DB_PORT=6432 \
PAYSYS_PG_DB_HOST=sas-usb28cf822kcr1jg.db.yandex.net \
PAYSYS_PG_DB_USER=balance_dcs_dev \
PAYSYS_PG_DB_NAME=balance_dcs_dev \
DCSAAP_DIR=`pwd` DCSAAP_DEBUG=1 NIRVANA_DEFAULT_WORKFLOW_ID='zzz' NIRVANA_DEFAULT_INSTANCE_ID='ooo' NIRVANA_API_TOKEN=yyy ./manage/manage migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, core, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying core.0001_initial... OK
  Applying core.0002_run... OK
  Applying core.0003_auto_20191129_1629... OK
  Applying core.0004_run_error... OK
  Applying core.0005_auto_20191205_1327... OK
  Applying sessions.0001_initial... OK
```
