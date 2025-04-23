Kelvin
======
[![Build Status](https://drone.yandex-team.ru/api/badges/corp-education/backend/status.svg)](https://drone.yandex-team.ru/corp-education/backend)

Чиним drone
----------------------
drone repo repair corp-education/backend # пропавшие хуки
drone repo chown corp-education/backend # ушедшие в отпуск гитхаб юзеры

Начало работы в Ubuntu
----------------------

1. Устанавливаем `git`, `docker`, `fabric`, `postgres`.

        sudo apt-get install git docker.io fabric postgresql

1. Настраиваем `git` и `docker`. Клонируем репозиторий.

    * [Вопросы про github](https://wiki.yandex-team.ru/github/#otvetynachastozadavaemyevoprosy)
    * [Авторизоваться в docker registry](https://wiki.yandex-team.ru/qloud/docker-registry/#avtorizacija)

    Клонируем репозиторий.

        git clone git@github.yandex-team.ru:corp-education/backend.git && cd kelvin

1. Создаем docker-образ для разработки, БД и питон-окружение.

        fab makedev

1. Добавляем в `hosts` запись про домен из сертификата:

        sudo sh -c "echo '127.0.0.1   backend.localhost.yandex.ru' >> /etc/hosts"

Начало работы в Mac OS с помощью docker-compose
-----------------------------------------------

***С поправкой на способы установки может быть повторено на любой системе, но обкатывалось на Mac OS***

***В отличие от остальных способов развертывания, не требует установки в системе postgres, а также
не занимает их порты.***

1. Устанавливаем [docker CE for mac](https://www.docker.com/docker-mac).

2. Устанавливаем `git`, `fabric`

        brew install git fabric

3. Настраиваем `git` и `docker`. Клонируем репозиторий.

    * [Вопросы про github](https://wiki.yandex-team.ru/github/#otvetynachastozadavaemyevoprosy)
    * [Авторизоваться в docker registry](https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#avtorizacija)

    Клонируем репозиторий.

        git clone git@github.yandex-team.ru:corp-education/backend.git && cd kelvin

4. Добавляем в `hosts` запись про домен из сертификата:

        sudo sh -c "echo '127.0.0.1   moe-backend.localhost.yandex.ru:8080' >> /etc/hosts"

5. Создаем файл `my.conf.local` в `src/kelvin/settings` и добавляем туда настройки баз данных:

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'corp_education',
        'USER': 'corp_education',
        'PASSWORD': 'corp_education',
        'HOST': 'postgres',
        'PORT': '5432',
        'CONN_MAX_AGE': 600,
    }
}

STATIC_ROOT = '<path_to_kelvin>/static/'
MEDIA_ROOT = '<path_to_kelvin>/media/'
```

*Далее в Workflow используем версии команд с `dc_`*


Начало работы в Mac OS
----------------------

1. Устанавливаем [docker CE for mac](https://www.docker.com/docker-mac).

1. Устанавливаем `virtualenv`
        pip install --user virtualenv

1. Устанавливаем `git`, `fabric`, `postgres`.

        brew install git fabric postgresql

1. Запускаем postgresql

        postgres -D /usr/local/var/postgres

1. Создаем пользователя postgres.

        createuser postgres -s

1. Настраиваем `git` и `docker`. Клонируем репозиторий.

    * [Вопросы про github](https://wiki.yandex-team.ru/github/#otvetynachastozadavaemyevoprosy)
    * [Авторизоваться в docker registry](https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#avtorizacija)

    Клонируем репозиторий.

        git clone git@github.yandex-team.ru:corp-education/backend.git && cd kelvin

1. Настраиваем прокси сервер для работы с ipv6.

    Выполняем команду

        sudo ifconfig lo0 add 10.10.10.10/32

    Если раньше стоял `squid` - смело сносим его

        brew uninstall --force squid

1. Создаем docker-образ для разработки, БД и питон-окружение.

        fab makedev

    Если раньше уже выполняли эту команду, то следует запускать ее без пересоздания БД

        fab makedev:create_db=False


1. Добавляем в `hosts` запись про домен из сертификата:

        sudo sh -c "echo '127.0.0.1   moe-backend.localhost.yandex.ru:8080:8080' >> /etc/hosts"

1. Настройка PyCharm

    1. Создаем Docker c настройками
        * API URL `unix:///var/run/docker.sock`

    1. Настройки - проект - интерпретатор -- Add remote
        * Выбираем docker
        * Server        `Docker`
        * Image name    `mac:latest`
        * Python path   `python`

1. Запускаем сервер:
        fab dc_runserver

1. Если не запущены миграции, запускаем:
```sh
        docker ps
        # > CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
        # > ec27e2405032        backend_app         "python src/manage.p…"   26 seconds ago      Up 25 seconds       0.0.0.0:8080->8080/tcp   backend_app_run_a33602578946
        # > 7c9b995cf2b5        postgres:10         "docker-entrypoint.s…"   27 seconds ago      Up 26 seconds       5432/tcp                 backend_postgres_1

        docker exec -it backend_app_run_a33602578946 sh

                # > внутри sh
                python src/manage.py migrate

                # > создаем юзера
                python src/manage.py shell

                # from kelvin.accounts.models import User
                # User(username='specdev01', is_superuser=True, is_staff=True, is_content_manager=True).save()
```

1. Открываем приватную вкладку и логинимся [https://passport-test.yandex.ru/](https://passport-test.yandex.ru/) и логинимся `specdev01:specdev`
1. Открываем в том же окне в соседней вкладке [https://backend.localhost.yandex.ru:8080/admin](https://backend.localhost.yandex.ru:8080/admin)


Workflow
--------

1. Запуск разработческого сервера:

        fab runserver

    или:

        fab honcho

    Сервер должен быть доступен по адресу [https://backend.localhost.yandex.ru:8080/admin](https://backend.localhost.yandex.ru:8080/admin)

1. Для переопределения настроек проекта локально создайте файл `src/kelvin/settings/my.conf.local`
и пропишите их там. После каждого изменения этого файла необходимо перезапускать `runserver`.

1. При запуске на Mac OS нужно убедиться, что файлы `requirements*.txt` не были
обновлены. Если кто-то из них изменился - запускаем `fab makelocalimage`.

1. Запуск тестов:

        fab test_all


Текущие проблемы
----------------

* В директории создаются новые файлы `root`-пользователем (нельзя просто
редактировать его)
* На маке, при запуске скрипта экспорта курсов, файлы ресурсов не тянутся в
архив (проблема с сетью, по wget к ним тоже не достучаться из контейнера)

    Текущее решение заключается в отключении проксирования. Подробное описание
    на [GitHub](https://github.yandex-team.ru/corp-education/backend/pull/134)

* **Mac OS only** Если возникли проблемы с ipv6 трафиком - пробуем следующие шаги

    Удаляем старый `squid`

        brew uninstall --force squid

    Смотрим список запущенных контейнеров

        docker ps

    Среди них должен быть контейнер `squid` и у него должен быть проброшен порт 3128
    (0.0.0.0:3128->3128/tcp). Если его нет - запускаем его старт

        fab runsquid

    Если раньше не делали, добавляем к интерфейсу адрес 10.10.10.10

        sudo ifconfig lo0 add 10.10.10.10/32

* **Mac OS only** Если возникли проблемы с доступностью `tvm`

    Эти проблемы связаны с IPv6, с которым [docker CE for mac](https://www.docker.com/docker-mac) сейчас работает плохо.

    Решением может быть исключение `kelvin.common.middleware.TVMMiddleware` из списка миддлварей.
    Для этого необходимо добавить в файл `my.conf.local` в `src/kelvin/settings` следующий код:

    ```
    TVM_MIDDLEWARE = 'kelvin.common.middleware.TVMMiddleware'

    MIDDLEWARE = tuple(filter(
        lambda x: x != TVM_MIDDLEWARE, MIDDLEWARE
    ))
    ```

* **Mac OS only** Проблемы с TLS соединением при клонировании репозитория

    При подключении к VPN меняется сетевой интерфейс. Еще раз выполните

        sudo ifconfig lo0 add 10.10.10.10/32


Сборка образов и релиз
----------------------
:))
Релиз собирается автоматически при push-е в ветку `stable` (см. `.drone.yml`):

- Еще раз прогоняются тесты.
- Автоматически генерируется новый тег в формате `<major>.<minor>.<patch>`:
  * В качестве базового тега будет взят последний из репозитория.
  * Если pull request был из `master`, то инкрементируется `minor` версия.
  * Если pull request был из какого-то другого бранча, то инкрементируется `patch` версия.
- Создается релиз на [странице проекта](https://github.yandex-team.ru/corp-education/backend/releases) в GitHub и тикет в StarTrack
- Собираются докер-образы:
  * `registry.yandex.net/corp-education/kelvin-admin:<tag>`
  * `registry.yandex.net/corp-education/kelvin-api:<tag>`
  * `registry.yandex.net/corp-education/kelvin-celery:<tag>`

Fabric команды
--------------

- Создание docker-образа, виртуального окружения и базы данных для начала разработки.

        fab makedev

- Скачивание docker-образа для локальной разработки

        fab makelocalimage

- Создание виртуального окружения проекта

        fab makevenv

- Создание БД для разработки (по умолчанию называется `pelican`)

        fab makedb

- Консоль в docker-образе

        fab bash

- Применение миграций

        fab migrate

- Запуск девелоперского джанго-сервера

        fab runserver

- Запуск девелоперского джанго-сервера в docker-compose

        fab dc_runserver

- Одновременный запуск сервера и селери (при дефолтном виртуальном окружении)

        fab honcho

- Одновременный запуск сервера и селери в docker-compose

        fab dc_honcho

- Открытие джанго-консоли

        fab shell

- Запуск юнит-тестов из kelvin-а

        fab test

- Запуск юнит-тестов из kelvin-а в docker-compose

        fab dc_test

- Запуск только тестов, помеченных <name>
(пометка с помощью декоратора @pytest.mark.<name>)

        fab dc_test:match='<name>'

- Остановка тестов после n ошибок

        fab dc_test:maxfail=n

- Запуск интеграционных тестов из kelvin-а

        fab test:test_type='integration'

- Запуск интеграционных тестов из kelvin-а в docker-compose

        fab dc_test:test_type='integration'

- Запуск всех тестов в проекте

        fab test_all

- Запуск всех тестов в проекте в docker-compose

        fab dc_test_all

- Запуск юнит-тестов с построением coverage-отчета в html

        fab coverage

- Запуск юнит-тестов с построением coverage-отчета в html в docker-compose

        fab dc_coverage

- Сборка и пуш в registry образа

        fab build

- Проверка соответствия кода стандарту PEP 8

        fab pep8_all

- Проверка соответствия кода стандарту PEP 8 в docker-compose

        fab dc_pep8_all

- Проверка соответствия измененного кода (diff c локальным master) стандарту PEP 8

        fab pep8
