# Maps base docker image

Базовый докер-образ Я.Карт представляет собой готовую платформу для построения "типичного" сервиса бэкенда карт.
Написан с прицелом на запуск и эксплуатацию сервиса в [RTC](https://wiki.yandex-team.ru/maps/dev/core/instrukcija-po-sozdaniju-servisov-v-rtc/).
Для создания сервиса в Няне (RTC) рекомендуется использовать [Sedem](https://docs.yandex-team.ru/sedem/).

Содержимое базового образа размещено в [Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/baseimage/).
Актуальную стабильную версию базового образа можно найти в любом докерфайле в `maps`, который наследуется от базового, например, [в инфраструктурном тестовом сервисе](https://a.yandex-team.ru/arc_vcs/maps/infra/teaspoon/docker/Dockerfile#L1).

## Основные компоненты { #components }
Базовый образ представляет собой докер-образ на основе Ubuntu (на текущий момент поддерживаются версии на основе Trusty Tahr и Bionic Beaver), содержащий базовые инфраструктурные компоненты, используемые в Картах:
- [supervisord](http://supervisord.org) - менеджер процессов
- nginx - reverse-proxy, используется в связке с yacare для обслуживания http-запросов
- [yacare](../yacare/index.md) - fastcgi-фреймворк на C++ для создания http-приложений (сервантов)
- [pycare](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/pycare) - экспериментальный asyncio-фреймворк на python для создания http-приложений
- [ecstatic](https://wiki.yandex-team.ru/maps/dev/core/ecstatic/) - распределенная система доставки и управления данными на основе торрентов
- [ratelimiter-agent](https://wiki.yandex-team.ru/geo-infra/ratelimiter2-manual/) - агент для подсчета и квотирования запросов
- [roquefort](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/roquefort/README.md) - инструмент для анализа логов nginx и построения метрик на их основе
- [tvmtool](https://wiki.yandex-team.ru/geo-infra/tvm2usage/) - агент системы аутентификации одного сервиса перед другим сервисом
- [push-client](https://wiki.yandex-team.ru/logbroker/docs/push-client/) - инструмент для поставки логов в Logbroker
- [yasm-subagent](https://wiki.yandex-team.ru/golovan/) - агент сервиса для построения графиков
- [metric-collector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/metric_collector/README.md) - прокси-утилита для сбора метрик из нескольких источников для Голована (yasm)
- [unified-agent](http://docs.yandex-team.ru/unified_agent/) - универсальный агент для передачи и обработки потоков данных, используется в качестве альтернативы `syslog-ng`, `push-client` и `logrotate`
- syslog-ng - система менеджмента логов
- logrotate - утилита для ротации логов
- cron - утилита для запуска скриптов по расписанию

## Настройка
### Рекомендуемая структура директории сервиса в Аркадии { #folder-structure }
Все сервисы в бэкенде Карт имеют одинаковую структуру директорий в Аркадии.
Это упрощает навигацию по коду и уменьшает вероятность ошибок при создании новых сервисов.
Мы рекомендуем придерживаться этой структуры при заведении новых сервисов.

Ниже представлен ряд шаблонов, описывающих рекомендуемую структуру.
Подробнее про отдельные компоненты:
- [template_generator](#template-generator)
- [juggler/checks](#juggler-checks)
- [README.md](https://wiki.yandex-team.ru/maps/dev/core/instrukcija-po-sozdaniju-servisov-v-rtc/#napisatreadmekservisu)
- [sedem_config](https://docs.yandex-team.ru/sedem/)

#### Примерное содержимое директории сервиса { #structure-exmaple }
**N.B.**: На текущий момент директория `sedem_config` должна обязательно находиться рядом с директорией `docker`,
содержащий докерфайл. Иначе возможны проблемы при сборке докер-образа с помощью SEDEM'а.
**N.B. 2** `pkg.json["meta"]["version"]` должно быть в точности равно `"{revision}"`,
в противном случае Sedem не сможет работать с такими образами (в т.ч. релизить).

```bash
.
├── bin
│   ├── ...
│   └── ya.make
├── docker
│   ├── Dockerfile
│   ├── install
│   │   ├── etc
│   │   │   ├── template_generator
│   │   │   │   ├── config.d
│   │   │   │   │   └── 50-service-setup.yaml
│   │   │   │   └── templates
│   │   │   │       ├── etc
│   │   │   │       │   └── runner
│   │   │   │       │       └── runlast.d
│   │   │   │       │           └── 99_rerun-hooks.sh
│   │   │   │       └── ...
│   │   │   └── ...
│   │   └── juggler
│   │       └── checks
│   │           └── custom_check
│   │               └── MANIFEST.json
│   └── pkg.json
├── README.md
├── sedem_config
│   ├── alerts.yaml
│   ├── __all__.yaml
│   ├── filters.yaml
│   └── metrics_convertors.yaml
└── ya.make
```

#### Шаблон для докерфайла сервиса { #dockerfile-template }
```Dockerfile
FROM registry.yandex.net/maps/core-base-bionic:XXXXXXX
MAINTAINER John Doe <johndoe@yandex-team.ru>

COPY install /

RUN yacare enable service-name  # if applicable
```

### run.sh { #runsh }
Точкой входа в контейнер (docker-entrypoint) является скрипт [`run.sh`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/baseimage/install/etc/runner/run.sh).
Именно его Sedem указывает в Няне в качестве точки старта.

Внутри `run.sh` зашит четкий порядок запуска компонент базового образа:
- [шаблонный генератор](#template-generator)
- скрипты из директории `/etc/runner/run.d` (в лексикографическом порядке)
- supervisord
- скрипты из директории `/etc/runner/runlast.d`
- **контейнер запущен**

При завершении контейнера (SIGTERM) порядок будет такой:
- скрипты из директории `/etc/runner/stop.d`
- остановка supervisord
- скрипты из директории `/etc/runner/exit.d`
- **контейнер остановлен**

В качестве языка скриптов (внутри `/etc/runner/*.d`) поддерживается **только** bash
(у файла должно быть расширение .sh), наличие executable-bit и shebang **не требуется**.

### template generator { #template-generator }
Для конфигурирования образа и подстройки конфигов в зависимости от сервиса, окружения и других параметров в образ включен [шаблонный генератор](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/baseimage/template_generator).

Шаблонный генератор использует jinja-шаблоны. При запуске шаблонный генератор опирается на 2 директории:
- `/etc/template_generator/config.d/` - директория с конфигами сервиса, на основе которых (в том числе) происходит шаблонизация
- `/etc/template_generator/templates/` - директория с jinja-шаблонами, расположенными согласно их итоговому пути в ФС (т.е. результат шаблонизации `templates/etc/sample-config` окажется в `/etc/sample-config`)

#### Конфигурация шаблонов { #templates-configuration }
Конфиги из `config.d` читаются в лексикографическом порядке. Из базового образа приезжает [дефолтный конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/baseimage/install/etc/template_generator/config.d/00-default-config.yaml), который содержит полный список доступных настроек со значениями по-умолчанию.

Основные секции настроек:
- `enabled` - включение/отключение компонент
  - `nginx` - запускает nginx + roquefort (см. [секцию про nginx](#nginx-configuration))
  - `yacare_app` - (см. [секцию про yacare](#yacare-setup))
  - `yasm_agent` - запускает yasm-subagent (см. [секцию про yasm subagent](#yasm-subagent))
  - `push_client` - запускает пуш-клиент (не во всех окружениях, см. [секцию про push-client](#push-client))
  - `ecstatic` - запускает [ecstatic-client](https://wiki.yandex-team.ru/maps/dev/core/ecstatic/)
  - `ratelimiter` - запускает агента рейтлимитера (см. [секцию про ratelimiter](#ratelimiter))
  - `tvmtool` - запускает [tvmtool](https://wiki.yandex-team.ru/geo-infra/tvm2usage/)
  - `cron` - запускает cron
- `app` - настройки приложения (специфичные для yacare-приложения [описаны отдельно](#yacare-setup))
  - `name` - имя приложения, используется в конфигах nginx (например формате access-tskv лога).  
    **Внимание**: для не-yacare приложения по-умолчанию подставляется значение prj instance тэга Няни
- `nginx` - настройки nginx (см. [секцию про nginx](#nginx-configuration))
- `logrotate` - настройки запуска logrotate
  - `period` - интервал в секундах между проверками условий ротации логов
- `logs` - настройки ротации логов
  - `maxsize` - максимальный размер лога, после чего происодит принудительная ротация
  - `rotate` - кол-во версий лога, не считая текущего, которые нужно хранить
  - `compress` - "сила" сжатия
- `push_client` - настройки пуш-клиента (см. [секцию про push-client](#push-client))
- `unified_agent` - настройки unified-agent (см. [секцию про unified-agent](#unified-agent))

#### Изменение настроек { #settings-modification }
Для того, чтобы изменить какой-либо параметр, нужно в образе сервиса подложить конфиг со своими настройками, например такой:
```
# 50-service-setup.yaml
enabled:
    ecstatic: true
    yasm_agent: true

app:
    autostart: true
```

#### Выбор конфигов под окружение { #per-environment-config }
Вывод имени окружения производится по следующим правилам:
1. Берется суффикс имени Няня-сервиса `MAPS_CORE_SERVICE_PRESTABLE -> prestable` и сохраняется в jinja-переменную `ENVIRONMENT_NAME`
2. Из имени окружения выводится тип окружения [по следующим правилам](https://a.yandex-team.ru/arc/trunk/arcadia/maps/tools/template_generator/lib/template_generator.py?rev=5199754#L23), например `prestable -> stable, stable -> stable`, и сохраняется в jinja-переменную `ENVIRONMENT_TYPE`
3. Помимо типа окружения поддерживается легаси тип окружения (**deprecated**), например `stable -> production`, который доступен в jinja-переменной `ENVIRONMENT_TYPE_SYNONYM`

Для привязки настроек к окружению шаблонный генератор поддерживает 2 способа:
1. через jinja-шаблон конфига в `templates`, содержащий следующую конструкцию
    ```
    @@ if ENVIRONMENT_NAME == "stable"
    ...
    @@ endif
    ```
2. через набор конфигов для каждого окружения в `templates`, с именами, соответствующими окружениям, в которых должны использоваться конфиги:
    ```
    $ ls /etc/template_generator/templates/etc/service-settings
    settings.stable.conf  settings.testing.conf
    ```
    При этом содержимое итоговой директории `/etc/service-settings/` будет, например, таким:
    ```
    $ ls -l /etc/service-settings/
    settings.conf -> /etc/service-settings/settings.testing.conf  # symlink to config for testing enviroment
    settings.stable.conf
    settings.testing.conf
    ```
    Конфиг, на который будет указывать симлинка, выбирается по следующим правилам:
    - Если есть конфиг, содержащий в имени `ENVIRONMENT_NAME`, например, `settings.prestable.conf`, то берется он
    - Если есть конфиг, содержащий в имени `ENVIRONMENT_TYPE`, например, `settings.stable.conf`, то берется он
    - Если есть конфиг, содержащий в имени `ENVIRONMENT_TYPE_SYNONYM`, например, `settings.production.conf`, то берется он
    - Если есть конфиг, содержащий в имени `default`, например, `settings.default.conf`, то берется он
    - Если ни один конфиг не подошел, то симлинка не выставляется

    (Описанная логика реализована [тут](https://a.yandex-team.ru/arc/trunk/arcadia/maps/tools/template_generator/lib/template_generator.py?rev=5199754#L175))

### Конфигурация nginx { #nginx-configuration }
Базовый образ содержит все необходимые конфиги nginx'а для интеграции с yacare и roquefort. Доступные параметры задаются в конфиге [шаблонного генератора](#template-generator) в секции `nginx`.
- Отключение nginx автоматически отключает roquefort
- По-умолчанию, nginx запускает кол-во воркеров равное числу доступных ядер (гарантированных);
  можно указать конкретное число, переопределив `worker_processes` в конфиге шаблонного генератора
- nginx пишет access.log в tskv-формате, если yacare-app включен в конфиге шаблонного генератора;
  обычный access.log из коробки не поддерживается
- Параметр `all_temporaries_in_ram` заставляет nginx использовать `/dev/shm` для хранения временных файлов
  (отключать не рекомендуется, если вы не уверены, что вам это не нужно)
- Для включения логгирования tvm id предусмотрен параметр `log_src_tvm_id`

### Настройки приложения yacare { #yacare-setup }
Базовый образ из коробки поддерживает запуск yacare-приложений.

Флаг `yacare_app` в секции `enabled` конфига шаблонного генератора включает серванта и его [juggler'ные проверки](#juggler-checks).

Параметры yacare-приложения в секции `app`:
- `autostart` - автозапуск на старте контейнера, вызов (`yacare start`) в `runlast.d` секции (**не подойдет**, если сервису для работы нужны данные, доставляемые экстатиком, см. [секцию про работу с хуками экстатика](#ecstatic-hooks))
- `name` - автоматически генерируется yacare при сборке приложения ya make'ом; явно указывать не требуется
- `required_datasets` - список датасетов, необходимых для запуска приложения, см. [секцию про работу с хуками экстатика](#ecstatic-hooks)

### Push-client { #push-client }
Базовый образ содержит конфиг пуш-клиента для отправки tskv-логов nginx в logbroker. По-умолчанию, пуш-клиент запускается только в stable и prestable окружениях.
Это поведение регулируется секцией `push_client` в конфиге [шаблонного генератора](#template-generator):
- `config_files` - указывает конфиг-файлы для stable/prestable окружений и запускает пуш-клиент в этих окружениях
- `config_files_testing` и `config_files_datatesting` - указывает конфиг-файлы соответственно testing / datatesting окружений (по-умолчанию пуш-клиент в этих окружениях не запускается, т.к. пути к конфигам отсутствуют)

**Всем сервисам, использующим push-client, [необходимо обязательно](https://clubs.at.yandex-team.ru/security/14726) включить TVM-авторизацию. [Инструкция по включению TVM-авторизации в push-client](https://wiki.yandex-team.ru/geo-infra/how-to/faq/#instrukcijapovkljuchenijutvm-avtorizaciivpush-client)**

### Unified-agent { #unified-agent }

Для использования `unified_agent` в качестве замены `push_client`/`syslog-ng`/`logrotate` достаточно добавить в базовую конфигурацию `template_generator` поле `enabled.unified_agent: true`. В результате будут настроены следующие маршруты:
 - `unified_agent` установится в качестве `syslog` клиента в систему (на чтение логов из `/dev/log` и на *ipv4/v6* `:514` порту),
 - при наличии `nginx` его логи *error*/*access* будут автоматически собираться `unified_agent`-ом на диск, и для заданных в `unified_agent.nginx_access_tskv.environments_enabled` окружений (по умолчанию *stable*, *prestable*, *dataprestable*, *experiments*) *access*-лог *nginx*-а будет отгружаться в `logbroker`,
 - `unified_agent` настроится в качестве источника данных для *access*-метрик `roquefort`.

В дополнение к этому поддерживается настройка отправки пользовательских логов в топики `logbroker`-а (с диспетчеризацией по `syslog`-тэгу). Для настройки необходимо добавить следующие конфигурации:

`aradia/<service-path>/docker/install/etc/template_generator/config.d/50-*-setup.yaml`
```yaml
unified_agent:
  env_client_id:
    stable: 123456 # stable tvm-id
    # testing: <testing tvm-id>  # if service sends logs from testing to YT
  default_syslog_channels:
    - tag: TAG  # YCR_LOG_DECLARE(TAG, ...)
      channel: ch_yacare_service-log
```

**NB: should go away soon**

`arcadia/<service-path>/docker/install/etc/template_generator/templates/etc/yandex/unified_agent/conf.d/04-*-log.yml`
```yaml
storages:
  - name: log_storage
    plugin: fs
    config:
      directory: /var/log/yandex/unified_agent/storages/<service>-log  # place your service-name
      max_partition_size: 1gb
      data_retention:
        by_age: 7d
        by_size: max
channels:
  - name: ch_yacare_service-log  # the same as in 50-*-setup.yaml config
    channel:
      pipe:
        - storage_ref:
            name: log_storage
      output:
@@ if ENVIRONMENT_NAME in ('stable', 'prestable')  # 'testing' if service has `-testing` topic
        plugin: logbroker
        config:
          endpoint: logbroker.yandex.net
          ha: { }
# if your service sends logs in testing, specify the topic here as well
# for example create maps/<service>-topic-testing in Logbroker
          topic: maps/<service>-topic
          tvm_ref:
            name: tvm_to_logbroker
            destination_id: logbroker
@@ else
        plugin: dev_null
@@ endif
```

### Yasm subagent { #yasm-subagent }
По-умолчанию в няне уже работает yasm-агент на хост-системе: раз в 5 секунд он ходит в контейнер на стат-ручки `:7033/yasm_stats` и `:8033/yasm_stats` и забирает метрики roquefort'а и yacare.

Однако иногда нужно отправлять метрики из скриптов или других периодических процессов, которые не висят в памяти и не могут отвечать на стат-ручку. Для этого в базовый образ встроена возможность запуска субагента, который умеет принимать сигналы, отправленные ([push-ем](https://wiki.yandex-team.ru/golovan/userdocs/push-api/)).

Для запуска subagent'а нужно включить его в настройках [шаблонного генератора](#template-generator) и выставить в Няне в instance spec `YASM subagent policy` равную `Don't start YASM subagent but bind its directory from host into container filesystem`.

### Ratelimiter
Флаг в секции `enabled` управляет запуском локального агента рейтлимитера.

Для yacare-сервисов, флаг включается автоматически. Остальным нужно делать вручную.

В отдельной секции `ratelimiter` можно дополнительно задать:
- `excluded_environments` - список окружений сервиса, в которых рейтлимитер выключен явно (**значение по-умолчанию:** `[datavalidation]`)

### Утилиты
#### Работа с персистентными разделами { #persistent-volumes }
Многим сервисам необходимо наличие персистентного раздела с данными (volume), который сохраняется между редеплоями.
Обычно таких разделов 2:
- для логов - монтируется в директорию `/logs`
- для данных - монтируется в `/persistent`

В базовый образ встроен bash-скрипт, который умеет линковать произвольную директорию в указанный раздел.
По-умолчанию, директория `/var/log` уже слинкована в раздел `/logs`.

Если сервису необходимы другие персистентные директории, их можно самостоятельно слинковать в `/persistent`, например, директория с данными экстатика:
```
$ cat etc/runner/run.d/02_link-persistent-volumes.sh
#!/bin/bash
. /usr/lib/yandex/maps/base-image-util/link-persistent-volume.sh

linkToVolume /persistent /var/lib/yandex/maps/ecstatic
```

#### Работа с хуками экстатика { #ecstatic-hooks }
На старте контейнера бывает нужно выполнить switch-хуки экстатика, чтобы проставить необходимые для сервиса симлинки на данные.
Для этого базовый образ предоставляет bash-функцию `rerunHook`, с помощью которой можно перезапускать хуки экстатика:
```
$ cat etc/template_generator/templates/etc/runner/runlast.d/99_rerun-hooks.sh
#!/bin/bash
. /usr/lib/yandex/maps/ecstatic-support/rerun-hook.sh

rerunHook switch yandex-maps-graph-activator || :
```

Кроме того, в самих хуках бывает полезно знать, сможет ли сервис стартовать, или каких других данных не хватит. Для этого есть функция `areRequiredDatasetsAvailable`, которая позволяет узнать, все ли датасеты экстатика, необходимые для запуска сервиса, засвитчились:
```
#!/bin/bash
. /usr/lib/yandex/maps/ecstatic-support/switchlib.sh

if areRequiredDatasetsAvailable ; then
    log "Restarting services..."
    sudo -n yacare restart service || :
fi
```

Список датасетов функция `areRequiredDatasetsAvailable` получает из конфигов шаблонного генератора:
```
app:
    autostart: false
    required_datasets:
        - yandex-maps-coverage5-trf
        - yandex-maps-coverage5-geoid
        - yandex-maps-geodata5
        - yandex-maps-geobase-tzdata
        - yandex-maps-graph-activator
```

Также, для работы с `preserved_data` есть функция `areRequiredPreservedDatasetsAvailable`,
которая работает аналогично функции `areRequiredDatasetsAvailable`.

Для ее конфигурации надо в конфиге шаблонного генератора прописать следующее:
```
app:
    autostart: false
    required_preserved_datasets:
        - yandex-maps-coverage5-trf
        - yandex-maps-coverage5-geoid
        - yandex-maps-geodata5
        - yandex-maps-geobase-tzdata
        - yandex-maps-graph-activator
```

#### Работа с пакетами { #packages }
**Disclaimer**: установка пакетов в карточные докер-образы **не рекомендуется** (более правильным будет собираться из сорцов в аркадии).

Базовый образ поставляется со сконфигуренным apt'ом и набором предустановленных пакетов. Полный список пакетов можно посмотреть в докерфайлах: [для bionic](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/baseimage/bionic.Dockerfile?rev=6261122#L15) и [для trusty](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/baseimage/trusty.Dockerfile?rev=6224213#L13).

Если есть необходимость добавить какой-либо пакет в ваш образ, рекомендуется сначала убедиться, что его нельзя собрать из сорцов, затем проконсультироваться с командой инфраструктуры: возможно, пакет стоит добавить в базовый образ.

Также существует bash-функция `stubPackage`, которая может пригодиться, если у пакета есть зависимости, которые хочется подменить, либо вовсе не ставить:
```
# Dockerfile
source /usr/lib/yandex/maps/base-image-util/stub-package.sh; \
    stubPackage provide yandex-maps-ecstatic-tool; \
    stubPackage provide yandex-maps-ecstatic-common; \
    stubPackage provide yandex-maps-ecstatic-client
```

### juggler'ные проверки { #juggler-checks }
В директориях `/juggler/checks` и `/juggler/checks-available` размещаются джагглерные проверки.

Из коробки работают:
- `supervisord-fatal-programs` - проверяет, что все процессы под supervisord запущены и работают
- `tvmtool-health-check` - чек живости tvmtool'а
- `ecstatic-*` - проверки работоспособности ecstatic-agent'а (если включен)
- проверки, которые автоматически генерит yacare, например, `<service>-alive` и `<service>-load`
- проверки на [`ratelimiter-agent`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ratelimiter2/agent_troubleshooting.md) (если включен)

Кастомные проверки сервиса нужно также размещать в `/juggler/checks`. [Пример кастомной проверки.](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer/docker/install/juggler/checks/jams_uploader/MANIFEST.json)

## Сборка coredump'ов процессов в RTC { #rtc-coredumps }
Создание корок разрешено для процессов от `root`, `www-data` и `ecstatic` во всех окружениях, кроме stable и prestable.
Чтобы включить сбор корок и для stable / prestable, нужно в Няне в instance spec добавить переменную окружения `USE_COREDUMPS=true`.

Помимо этого надо настроить, чтобы корки собирались не на хост-систему, а прямо в контейнер. Для этого нужно иметь вольюм `/cores` (это захардкожено в Няне). В целом можно руководствоваться [инструкцией](https://wiki.yandex-team.ru/runtime-cloud/nanny/coredumps/).
Там же можно настроить ротацию: рекомендуется выбрать размер равный размеру вольюма, количество корок побольше, а ttl=300, так как старые корки в любом случае удаляются только по приходу новых.

## Релизный цикл { #releases }
1. Выкатка teaset в testing
2. Выкатка teaset в stable
3. Запуск таски MAPS_BASE_IMAGE_UPDATER. В параметрах таски надо руками указать ревизию базового для релиза

## Текущие версии в production { #versioning }
[график в golovan](https://yasm.yandex-team.ru/template/panel/base_image_version/)
