# Базовый образ

<details><summary><b>Table of contents</b></summary>

* [Quick start](#quick-start)
    * [RUN_MODE](#run_mode)
    * [Local usage (способ 1)](#local-usage-способ-1)
    * [Local usage (способ 2)](#local-usage-способ-2)
* [Подробно о процессах внутри контейнера](#подробно-о-процессах-внутри-контейнера)
* [`start.sh`](#startsh)
    * [Расширение `start.sh`](#расширение-startsh)
* [Supervisor](#supervisor)
* [Nginx](#nginx)
    * [Точки расширения](#точки-расширения)
* [Node.JS](#nodejs)
* [Другие процессы](#другие-процессы)
    * [Push client](#push-client)
    * [Syslog-ng](#syslog-ng)
    * [Cron](#cron)
    * [Logrotate](#logrotate)
* [Monitorings](#monitorings)
    * [Roquefort](#roquefort)
        * [Кастомные сигналы](#кастомные-сигналы)
    * [Кастомные графики и мониторинги по логам приложения](#кастомные-графики-и-мониторинги-по-логам-приложения)
* [SSL](#ssl)
* [Tools](#tools)
    * [Управление инстансом (закрыть/открыть)](#управление-инстансом)
    * [Установка портальных библиотек](#установка-портальных-библиотек)
    * [Фильтрация логов nginx](#фильтрация-логов-nginx)
* [Developing](#developing)
</details>

## Quick start

```dockerfile
FROM registry.yandex.net/maps/ubuntu_<os_version>-node_<node_version>:<image_version>

# Здесь инструкции, специфичные для вашего проекта

ENV MAPS_NODEJS_APP /usr/local/app/out/app/app.js

CMD ["/start.sh"]
```

Где:
- `<os_version>` - имя версии Убунту, которую хотите использовать;
- `<node_version>` - версия node.js, которую хотите использовать;
- `<image_version>` - версия базового образа.

> Актуальные имена и версии образов доступны в файле [`versions.json`](./versions.json).

Если вам нужно прокинуть переменные окружения в команду запуска, то можно использовать инструкцию [`ENV`](https://docs.docker.com/engine/reference/builder/#env):

```dockerfile
ENV MAPS_NODEJS_APP /usr/local/app/out/src/app.js

CMD ["/start.sh"]
```

> Обратите внимание, что используется `exec`-форма команды [`СMD`](https://docs.docker.com/engine/reference/builder/#cmd), чтобы все сигналы прокидывались указанному процессу. По этой же причине в `/start.sh` выполняется `exec supervisord`.

### RUN_MODE
При старте контейнера можно передать переменную `RUN_MODE`, которая влияет на запуск приложений внутри контейнера:

1. **DEV** — нужен для локальной разработки, стартует только supervisor & nginx (поддерживает https, маска *.local.maps.yandex.TLD)
1. **STAND** — никакие приложения не стартуют, все надо делать "руками"
1. **default** — без этой переменной, стартует стандартный набор приложений (Supervisor, NodeJs, Nginx, Roquefort etc)

### Local usage (способ 1)

Сначала старт контейнера, потом запуск shell внутри.

1. Запустить контейнер.

    С флагом `-d` это происходит в background, то есть текущая консоль сразу же освобождается для ввода следующих команд.
    ```
    docker run -d -p 8080:80 registry.yandex.net/maps/<YOUR PROJECT NAME>:<IMAGE TAG>
    ```
1. Узнать ID запущенного контейнера.

    Если на предыдущем шаге мы запустили контейнер с флагом `-d`, то в результате выполнения команды увидим в консоли
    ID запущенного контейнера. Если запустили без флага, узнать ID можно командой
    ```
    docker ps -l
    ```
1. Запустить shell внутри контейнера

    ```
    docker exec -it <CONTAINER ID> bash
    ```

### Local usage (способ 2)

Сначала запуск shell, потом старт всех процессов.

1. Запустить контейнер.

    Флаг `-d` не используем осознанно, чтобы процесс запустился в foreground, и мы сразу окажемся в shell.
    ```
    docker run -p 8080:80 -it registry.yandex.net/maps/<YOUR PROJECT NAME>:<IMAGE TAG> bash
    ```
1. Стартовать все процессы.

    Проекты, собранные на основе `monitorings` стартуют скриптом `/start.sh`
    ```
    nohup /start.sh > /dev/null 2>&1 &
    ```
    Утилитка [nohup](https://ru.wikipedia.org/wiki/Nohup) запустит скрипт с игнорированием сигналов потери связи
    (SIGHUP), значит команда будет продолжать выполняться в фоновом режиме и после того, как пользователь выйдет из
    системы.

1. Убедиться, что все процессы запущены:

    ```
    supervisorctl status
    ```

    Всё хорошо, когда видим статус `RUNNING` для каждого процесса:

    ```
    cron                             RUNNING    pid 37, uptime 22:42:13
    nginx                            RUNNING    pid 38, uptime 22:42:13
    node                             RUNNING    pid 35, uptime 22:42:13
    push-client                      RUNNING    pid 45, uptime 22:42:13
    syslog-ng                        RUNNING    pid 36, uptime 22:42:13
    ```

## Multi-stage build

Для сборки проекта рекомендуется использовать [multi-stage build](https://docs.docker.com/develop/develop-images/multistage-build/).

Такой подход позволяет:

* улучшить чтение `Dockerfile`.
* уменьшить размер образа, а значит ускорить выкатку проекта.

> Чем меньше слоёв в итоговом образе, тем лучше.

## Подробно о процессах внутри контейнера

В мире docker-разработки принято стартовать контейнер с единственным запущенным процессом внутри — тем самым, который мы указали в `Dockerfile` в последней директиве `CMD`. Однако в Картах необходимо запускать в контейнере сразу несколько процессов. Этим занимается система контроля процессами [`supervisor`](#supervisor), которая запускается внутри [`start.sh`](#startsh).

`supervisor` последовательно стартует в контейнере разные процессы:
* `nginx`
* `syslog`
* `node`
* `cron`
* `roquefort`, `roquefort-custom`, `unistat-proxy`
* `push-client`

Для чего нужен каждый процесс описано ниже.

## `start.sh`

Bash-скрипт, который в контейнере запускается первым. Предназначен для того, чтобы считать переменные окружения при старте контейнера, подставить их значения в шаблоны и на основе их создать настоящих конфиги:

* `nginx.template.conf` -> `/etc/nginx/sites-enabled/nginx.default.conf`
* `accesslog-tskv.template.conf` -> `/etc/nginx/conf.d/01-accesslog-tskv.conf`
* `supervisord.template.conf` -> `/etc/supervisor/conf.d/supervisord.template.conf`
* `push-client.template.yaml` ->  `/etc/yandex/statbox-push-client/custom/nginx-tskv.yaml`

### Расширение `/start.sh`

Если требуется выполнить дополнительные действия при старте контейнера, то можно добавить их в файл [/extend.start.sh](root/extend.start.sh), который будет вызван из `/start.sh`.

## Supervisor

Supervisor — это [система контроля процессов](http://supervisor.readthedocs.io/en/latest/introduction.html). Умеет управлять, контролировать и рестартовать множественные процессы в контейнере.

Конфигурационный файл `supervisord.conf` поделён на секции, каждая конфигурирует отдельный процесс.
Директива `command` указывает на программу, которая стартует этот процесс.

```conf
[supervisord]
nodaemon=true
logfile_maxbytes = 10MB
logfile_backups = 2

[program:nginx]
command=/usr/sbin/nginx
stdout_logfile_maxbytes = 10MB
stderr_logfile_maxbytes = 10MB
stdout_logfile_backups = 2
stderr_logfile_backups = 2
autorestart = true

# .....
```

См. также:
* [Использование вместе с Docker](https://docs.docker.com/engine/admin/using_supervisord/)
* [Как его используют другие команды](http://proft.me/2011/05/28/supervisor-kaznit-nelzya-pomilovat/)


## Nginx

Используется в контейнере в качестве прокси-сервера. Нужен для сбора стандартизированных логов и выключения инстанса от балансировки.

По умолчанию слушает `80` порт, а получив запрос, перенаправляет его в конечную точку пути — в Nodejs-приложение на порт `8080`.

```nginx
server {
    listen [::]:80 default_server;

    location / {
        proxy_pass http://127.0.0.1:8080/;
    }
}
```

Если важно поменять значения этих портов, это можно сделать в настройках окружения Qloud. Создайте в своём окружении две переменные:
```yaml
MAPS_NGINX_PORT: 81
MAPS_NODEJS_PORT: 8686
```

### Точки расширения

У nginx сервера есть три точки расширения:

1. Если нужно увеличить размер тела клиентского запроса — передайте `MAPS_CLIENT_MAX_BODY_SIZE` в директиве `ENV` вашего `Dockerfile`.

1. Если нужно добавить `location` или `rewrite` в дефолтном конфиге это можно сделать положив во время сборки вашего образа файл в `/etc/nginx/include.d/extension.conf`. Например добавить локейшн для раздачи публичных статичных файлов:

    ```nginx
    location /public {
        root /www/public;
    }
    ```

1. Если нужно добавить заголовок при проксировании для корневого локейшена можно этого сделать, замените файл `/etc/nginx/include.d/root_location_extension.conf`. Например:

    ```nginx
    proxy_set_header X-Forwarded-Proto $protocol;
    ```

`MAPS_NGINX_PORT` — порт, на котором должен слушать `nginx`.

* Если не указать, будет использоваться readonly-переменная `QLOUD_HTTP_PORT`, которую в контейнер передаёт Qloud. Обычно равна `80`.
* Если вдруг в Qloud случится непоправимое, и `QLOUD_HTTP_PORT` не придёт, `nginx` будет слушать `80`.

См. также:
* [Настройки proxy-сервера](http://nginx.org/ru/docs/http/ngx_http_proxy_module.html#proxy_pass)
* [Разбираемся в HTTP прокси NGINX, балансировке нагрузки, буферизации и кешировании](http://devacademy.ru/posts/razbiraemsya-v-http-proksi-nginx-balansirovke-nagruzki-buferizatsii-i-keshirovanii/)

## Node.JS

Для запуска Node.js приложения требуется указать путь к файлу через переменную окружения `MAPS_NODEJS_APP`:

```dockerfile
ENV MAPS_NODEJS_APP /usr/local/app/out/app/app.js
```

* `MAPS_NODEJS_APP` — абсолютный путь к файлу, в котором стартует node.js приложение.
* `MAPS_NODEJS_PORT` — порт, на котором должно работать node.js приложение. Если не указать, `nginx` будет ожидать, что node.js приложение слушает `8080` и будет туда проксировать запросы.
* `MAPS_NODEJS_OPTIONS` — дополнительные опции для запуска node.js, по умолчанию пустая строка.

## Другие процессы

### Push client

Отправляет access логи nginx в [YT](https://yt.yandex-team.ru). Подробнее на [вики](https://wiki.yandex-team.ru/logbroker/docs/push-client/).

### Syslog-ng

[Сервер для сбора логов](https://en.wikipedia.org/wiki/Syslog-ng) работает в контейнере и собирает всю информацию о работе запущенных процессов.

### Cron

[Демон-планировщик задач](https://ru.wikipedia.org/wiki/Cron) по расписанию запускает `logrotate`, обрабатывая логи `nginx`.

### Logrotate

[Программа ротации логов](http://www.linuxcommand.org/man_pages/logrotate8.html).

* Сохраняет логи за определенный период времени в отдельный файл.
* Или разделяет лог на части определенного размера.

Ротация логов нужна для контроля размера дискового пространства, занимаемого файлами логов.

В результате работы `logrotate` остается один активный файл журнала, в который "сейчас" происходит запись со стороны сервера, и несколько архивных файлов, сжатых специальным упаковщиком. В итоге имеем следующую структуру:

```sh
$ ls -al /var/log/nginx/
total 3311880
drwxr-xr-x 1 root root       4096 Jan 17 10:30 .
drwxr-xr-x 1 root root       4096 Oct 30 15:10 ..
-rw-r--r-- 1 root adm   534998107 Jan 17 12:08 access-tskv.log
-rw-r--r-- 1 root adm  1169215623 Jan 17 10:30 access-tskv.log.1
-rw-r--r-- 1 root adm   621914897 Jan 17 12:08 access.log
-rw-r--r-- 1 root root 1065178646 Jan 16 23:00 access.log.1
-rw-r--r-- 1 root root      20467 Jan 17 12:07 error.log
```

## Monitorings

### Roquefort

Анализирует логи `nginx` в формате TSKV и отправляет агрегированные события в [Yasm](https://yasm.yandex-team.ru/), используя `unistat`.

#### Кастомные сигналы

В образе есть возможность забирать данные через unistat по кастомным сигналам. Для этого надо:

1. Написать скрипт, который будет возвращать число в `stdout`.
1. Имя файла будет использоваться для формирования названия сигнала.

    Например, файл называется `node_cpu_ammm.sh`, то сигнал будет называться `unistat-node_cpu_ammm`.

1. Все эти скрипты должны быть исполняемыми, т.е. нужно сделать `chmod +x script_name.sh`.
1. Располагаться скрипты должны в директории `/usr/local/checks/`.

Для мониторингов по кастомным сигналам используйте секцию `alerts-raw`:

```json
{
    "alerts-raw": {
        "node-cpu-alert": {
            "signal": "unistat-node_cpu_ammm",
            "warn": [30, 50],
            "crit": [50, null],
            "flaps": {
                "boost": 0,
                "stable": 600,
                "critical": 2400
            }
        }
    }
}
```

**Ограничения**

- Один скрипт — один сигнал.
- Скрипт должен отрабатывать за 50мс.

### Кастомные графики и мониторинги по логам приложения

У вашего приложения есть возможность настроить графики на количество определенных ошибок в логах. Для этого надо:

1. Включить логирование с помощью пакета [`@yandex-int/maps-logger`](https://github.yandex-team.ru/maps/infra/tree/master/packages/maps-logger).
1. В `.qtools.json` в секции `.geoSpecific.monitorings.components[].groups['app-tskv']` добавить соответствующие алерты.
1. При логировании обязательно указывать `group`: `logger.error('Error message', {group: 'module'});`.

Пример конфига можно посмотреть в [документации `qtools`](https://github.yandex-team.ru/maps/infra/blob/master/packages/qtools/docs/geo-specific.md#monitorings).

## SSL

В образ включены Яндексовые сертификаты. Подробнее об этом на [вики](https://wiki.yandex-team.ru/security/ssl/sslclientfix/).

### allCAs.pem
Сертификат лежит по пути: `/etc/yandex/common/allCAs.pem`, чаще всего он нужен для подключения к кластерам в MDB

### InternalRootCA
Сертификат лежит по пути: `/usr/share/yandex-internal-root-ca/YandexInternalRootCA.crt`, так же по умолчанию есть переменная `NODE_EXTRA_CA_CERTS`, которая содержит путь до него. Используется в Node.JS для подключения к внутреним https доменам Яндекса.

## Tools

### Управление инстансом

В нашем базовом образе есть утилита для управления инстансом:  `instancectl`

`instancectl <open|close> [hard]` -  open/close соответсвенно открывает/закрывает инстанс от балансера. Параметр **hard** позволяет закрыть инстанс, так что бы при проведение учений, его случайно не открыли. Использовать его стоит в том случае, если у инстанса проблеы с "железом" и редеплой не помогает.

### Установка портальных библиотек

В образе включен набор скриптов для установки портальных библиотек и их binding-ов для node.js:

* `install_lang_detect.sh`
* `install_libgeobase5.sh`
* `install_libgeobase6.sh`
* `install_libipreg1.sh`
* `install_uatraits.sh`

Их можно применять в Dockerfile вашего проекта:

```Dockerfile
FROM registry.yandex.net/maps/ubuntu_focal-node_16:1.0.2

# ...

RUN apt update && \
    install_libgeobase5.sh && \
    install_uatraits.sh && \
    install_lang_datect.sh

# ...
```

### Фильтрация логов nginx

В образе присутствует скрипт `http_codes.sh` для более быстрого и простого поиска по логам nginx-а:

```
----------------------------------
USAGE: http_codes.sh <http_codes> <add_field>
----------------------------------
http_codes:
    - stat - группировка по кодам ответов с кол-во запросов и процентным соотношением
    - 2xx - статистика по группе кодов с 200 по 299
    - 3xx - статистика по группе кодов с 300 по 399
    - 4xx - статистика по группе кодов с 400 по 499
    - 5xx - статистика по группе кодов с 500 по 599
    - так же можно указывать конкретный выбранный код (429, 499, 301 и т.д.)
add_field: дополнительные поля можно использовать только конкретно указаным кодом ответа
    - hosts - показывает поле vhost для выбранного кода ответа
    - ip - показывает поле ip для выбранного кода ответа
    - request - показывает поле request для выбранного кода ответа
```

Является оберткой над `timetail`, `grep`, `awk`.

## Developing

Checkout [CONTRIBUTING.md](./CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
