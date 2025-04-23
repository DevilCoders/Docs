# Service Repo Client

#  Установка {#install}
Клиент в Аркадии: [https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/service_repo_client](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/service_repo_client)

1. установить ya tool, [инструкция](https://wiki.yandex-team.ru/yatool/distrib/)
1. клонировать код клиента из Аркадии

    ```
    $ ya clone mini-arcadia
    $ cd mini-arcadia
    $ ya make infra/nanny/service_repo_client --checkout
    ```
1. для быстрого доступа к бинарю, добавить в PATH

    ```
    export PATH=$PATH:~/mini-arcadia/infra/nanny/service_repo_client/bin
    ```

### OAuth token {#oauth}

Для доступа к Nanny может понадобиться [OAuth token](https://nanny.yandex-team.ru/ui/#/oauth/)
Передать его можно несколькими способами:

* переменная окружения:

    ```
    export NANNY_OAUTH_TOKEN=your_oauth_token
    ```
* файл:

    ```
    $ mkdir ~/.scli
    $ echo your_oauth_token > ~/.scli/token
    ```
* через параметр

    ```
    $ scli -t your_oauth_token <command>
    ```

###  Конфигурационный файл {#config}

Для переопределения некоторых используемых значений можно задать конфигурационный файл. Файл должен быть в формате YAML (расширение `.yml`)

```
$ mkdir ~/.scli
$ touch ~/.scli/config.yml
```
либо вызывать с параметром

```
$ scli -c path_to_config <command>
```
Формат файла конфигурации / Конфигурация по умолчанию

```
service_repo_client:
    ## опции настраивают процесс выполнения запросов к Nanny API
    attempts: 3 ## количество retry при ошибках
    timeout: 30 ## таймаут на выполнение запроса в секундах
    delay: 1.0 ## минимальная задержка между двумя попытками в секундах
    max_delay: 5.0 ## максимальная задержка между двумя попытками в секундах
```


###  Рабочая директория {#workdir}

```
$ scli -d /path/to/dir <command>
```
По умолчанию используется директория, в которой запущен repo client.

## Использование {#usage}

Получить справку

```
$ scli -h
```

##  Команды {#commands}

###  list {#list}

Выводит список доступных сервисов для пользователя.
Для выполнения команде нужен логин пользователя, он должен соответствовать используемому oauth токену. По умолчанию логин берется из системы (whoami), можно переопределить при помощи опции `--user` или в конфигурационном файле:

```
auth:
    login: <your_login>
```
###  get {#get}

Создает в рабочей директории папку с именем сервиса, скачивает в нее основные аспекты сервиса:

* `info_attrs`
* `auth_attrs`
* `runtime_attrs`
* `cleanup_policy`

Доступны следующие опции:

* `-f/--force` — файлы скачиваются в директорию и перезаписывают локальные изменения.
* `-s/--stdout` — файлы не создаются, все аспекты выводятся в stdout в виде словаря, в котором ключи — названия аспектов, а параметры — сами аспекты (формат — JSON).

Если опция `--force` не используется и папка с именем сервиса уже существует в рабочей директории, завершается с ошибкой:

```
Service dir "service_name" exists already
```
Каждый аспект представлен файлами `attrs.yml`, `template_attrs.yml`, `raw_attrs.json`, `cleanup_policy.json`

{% note warning %}

Если в сервисе используется старая версия `cleanup_policy`, она будет доступна через `info_attrs`, соответствующих файлов создано не будет. Переключиться на использование новой версии `cleanup_policy` можно только через интерфейс Nanny.

{% endnote %}

###  update {#update}

1. Скачивает основные аспекты сервиса.
1. Если версия аспекта на сервере новее, чем локальная, обновляет локальную (перетирая изменения).

###  build {#build}

Компиляция файлов `template_*.yml` с использованием шаблонизатора Jinja2. Результат будет сохранен в `*.yml` и `raw_*.json`.

###  upload {#upload}

Загрузка на сервер файлов сервиса. Будут загружены файлы вида `raw_*.json`.
До начала загрузки аспектов проверяет, является ли версия каждого аспекта актуальной. Если версия не является актуальной, завершается с ошибкой

```
Newer version of info_attrs.json found.
```

#### Порядок загрузки аспектов {#order}

1. `Cleanup Policy`
1. `Auth Attributes`
1. `Runtime Attributes`
1. `Info Attributes`

Если во время загрузки одного из аспектов возникнет ошибка, загрузка остановится. Откат уже загруженных к тому моменту аспектов не выполняется.

#### Конфликты при модификации {#conflicts}

Загрузка может завершиться с ошибкой

```
Concurrent modification error: Wrong service and info attrs snapshot id pair - not found
```

Сообщение означает, что текущая версия `snapshot_id` у `info_attrs` не совпадает с загружаемой, т.е. в сервис были внесены изменения.
После загрузки файлов сервиса на сервер локальные версии файлов будут обновлены с указанием новых `snapshot_id`.

###  dump {#dump}

Аналогично `get -f`.

Доступны следующие опции:

* `--all` – скачать все существующие в Nanny сервисы
* `-p/--progress` – отобразить progress bar во время выполнения
* `-w/--worker WORKER_COUNT` – использовать `WORKER_COUNT` потоков (по умолчанию – 1)

Пример запуска.

Команда копирования всех сервисов в директорию `/home/username/nanny_dump` в 10 потоков, отображать прогресс выполнения.

```
$ scli -d /home/username/nanny_dump dump --all -p -w 10
```

Пример сценария cron.


```
0 */1 * * *    scli -d /home/username/nanny_dump dump --all -w 10 2> /tmp/scli_dump_error.log
```

###  restore {#restore}

Загружает файлы сервиса в Nanny, при условии, что его не существует на сервере, в ином случае вернет ошибку.

## Aux атрибуты {#aux}

С помощью `scli` можно редактировать `aux` атрибуты, доступные для `auth_attrs`, `info_attrs` и `runtime_attrs`.
Атрибуты добавляются в секцию `content`. В качестве ключей и значений следует указывать строки.

Пример для .yaml

```yaml
content:
    aux:
        items:
        -   key: '1'
            value: one
        -   key: '2'
            value: two
        -   key: '3'
            value: three
```

Пример для .json

```json
"content": {
        "aux": {
            "items": [
                {
                    "key": "1", 
                    "value": "one"
                }, 
                {
                    "key": "2", 
                    "value": "two"
                }, 
                {
                    "key": "3", 
                    "value": "three"
                }
            ]
        }, 
```


После загрузки атрибуты можно увидеть в UI Nanny

![auxattrs](https://jing.yandex-team.ru/files/sshipkov/auxattrs.6a3f539.png)

## Jinja2 продвинутое использование {#ninja}

### Создание базового шаблона {#base-template}

```
$ mkdir templates
$ cp -r service_repo_client_demo/static_files/ templates/
$ touch templates/demo_template.yml
```

Содержание шаблона:

```python
engines:
    engine_type: BSCONFIG
instances:
    allocation_ids: []
    chosen_type: INSTANCE_LIST
    extended_allocations: []
    gencfg_groups: []
    instance_list:
    -   host: sg9-00.search.yandex.net
        ipv6_address: 2a02:6b8:0:2502::2509:5c40
        limits:
            cpu_policy: normal
            io_policy: normal
        port: 6123
        tags: []
        weight: 1
    iss_settings:
        instance_cls: ru.yandex.iss.Instance
resources:
    l7_fast_balancer_config_files: {}
    sandbox_bsc_shard:
        {% block shard %}
        chosen_type: SANDBOX_SHARD
        resource_type: ALEMATE_SHARD
        task_id: '56592861'
        task_type: BUILD_ALEMATE
        {% endblock %}
    sandbox_files:
        loop-httpsearch:
            {% block loop_httpsearch %}
            is_dynamic: false
            resource_type: INSTANCECTL
            task_id: '52800393'
            task_type: BUILD_INSTANCE_CTL
            {% endblock %}
    services_balancer_config_files: {}
    static_files:
        Conf.local:
            {% block Conf_local %}
            content: templates/static_files/Conf.local
            is_dynamic: false
            {% endblock %}
        loop.conf:
            {% block loop_conf %}
            content: templates/static_files/loop.conf
            is_dynamic: false
            {% endblock %}
        master.conf:
            {% block master_conf %}
            content: templates/static_files/master.conf
            is_dynamic: false
            {% endblock %}
    template_set_files: {}
    url_files:
        {% block url_files %}
        {}
        {% endblock %}
```


### Создание вложенного шаблона {#create-subtemplate}

```
$ echo "Hello, I'm rendered in {{ service_id }} service" > service_repo_client_demo/static_files/loop.conf

$ cat > service_repo_client_demo/template_runtime_attrs.yml << EOF
{% extends 'templates/demo_template.yml' %}

{% block loop_httpsearch %}
{{ sandbox_file('BUILD_INSTANCE_CTL', 52800393, 'INSTANCECTL') }}
{% endblock %}

{% block loop_conf %}
            content: {{ render('service_repo_client_demo/static_files/loop.conf') }}
            is_dynamic: false
{% endblock %}

{% block master_conf %}
{{ static_file('service_repo_client_demo/static_files/master.conf') }}
{% endblock %}
EOF
```
