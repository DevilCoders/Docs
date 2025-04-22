# Docker Backend
## Mini PGaaS
Новый Distribution (ранее называемый docker registry) не позволяет анонимное использование. Для представления необходимо использовать любой OAuth токен, выданный в Яндексе. Получить токен можно, например, по ссылке:

https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1

Если используется docker cli, то необходимо выполнить команду docker login следующим образом (версии выше  17.06.0-ce-rc4)
```
docker login -u <login> --password-stdin registry.yandex.net
<token_body><Enter>
^D
```

## Использование образов:

* Экспортировать переменную окружения GIT_TAXI_BACKEND_PATH с путем к дереву исходников

```shell
$ export GIT_TAXI_BACKEND_PATH=<backend path>
```

Примечание: переменную можно описать в файле .env, который следует разместить в корне проекта.

```shell
GIT_TAXI_BACKEND_PATH=<backend path>
```

* Сгенерировать образы, ключи и необходимые конфиги

```shell
$ make
```

* Запустить контейнеры

```shell
$ make projects
```

* (опционально) Запустить маппинг имен контейнером в /etc/hosts

```shell
$ make resolver
```

* Погасить контейнеры

```shell
$ make stop
```

### Запуск отдельного контейнера с проектом

Для того, чтобы взаимодействовать с проектом с локальной машины требуется добавить адреса контейнеров в /etc/hosts.

Сделать это можно либо руками, либо воcпользовавшись решением, которое добавляет hostname каждого проекта в соответствующий файл.

Возможное к использованию: [grachev/docker-hosts-updater (один скрипт на go для обновления списка хостов)](https://hub.docker.com/r/grachev/docker-hosts-updater/).

Выбрав способ обновления /etc/hosts можно запустить нужный сервис.

```shell
$ docker-compose up -d billing-accounts
```

```bash
$ curl -I billing-accounts.taxi.dev.yandex.docker/ping
```

### Запуск в изолированном окружении

Можно использовать данное окружение для поднятия всей инфраструктуры и тестирования комплексных задач.

* Запустить машину, из которой будут доступны все поднятые сервисы

```shell
$ make filler
```

## Добавление проектов на базе backend-py3

*Добавить описание проекта в docker-compose.yml*

```yaml
  PROJECT_NAME:
    <<: *billing-backend-py3
    # прописываем если хотим резольвит сервис с локальнй машины
    hostname: <hostname from nginx>> 
    environment:
    - PYTHONPATH=PATH_TO_PACKAGE_ROOT
    - PACKAGE=ORIGINAL_PACKAGE_NAME
    # указываем только при необходимости включить 
    # дочерний пакет из сервиса
    - SUB_PACKAGE=stq3 
    networks:
      backend:
        aliases:
        - SERVICE_URL
```

Пример

```yaml
  billing-accounts:
    <<: *billing-backend-py3
    hostname: billing-accounts.taxi.dev.yandex.docker
    environment:
    - PYTHONPATH=/usr/lib/yandex/taxi-billing-accounts
    - PACKAGE=taxi-billing-accounts
    - ENV=testing
    networks:
      backend:
        aliases:
        - billing-accounts.taxi.dev.yandex.docker
```

Прим: hostname должен быть равен записи в aliases и прописывается в случае, когда вы хотите работать с машиной не используя промежуточное окружение (filler).

*Добавить описание баз, которые использует проект, в config/database.list*

```text
project_folder_name project_key_in_taxi_json scheme_name svc_api_token svc_api_token_ro
```

* project_folder_name - папка проекта из каталога backend-py3. В соответствующей подпапке будет выполнен запуск файла storage/create_shards_psql.py, а шаблон структуры будет взят из файлов psql.
* project_key_in_taxi_json - ключ, который будет запрашиваться из taxi.json.
* scheme_name - имя схемы на шарде. В данную схему будет разложена выбранная база.
* api_token - токен для использования api проекта в режиме "чтение-запись"
* api_token - токен для использования api проекта в режиме "чтение"

Некоторые проекты используют общую базу. Для taxi-billing-accounts и taxi-billing-accounts-stq3 запись в database.list должна бть одна.

Пример

```text
taxi-billing-accounts billing_accounts ba_meta ba_token ba_token_ro
```

## Окружение

По-дефолту проект собирается из исходников и с окружением development.

Если потребуетсяоднять проект из пакетов, то необходимо создать файл .env

```shell
SOURCE=deb|src # поднять из пакетов или исходников
ENV=testing|unstable|stable # выбрать репозитарий
```
`
Если вы поднимаете проект из пакетов, то предварительно необходимо собрать пакеты в каталоге packages и разместить там же полученные deb-файлы.
