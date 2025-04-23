## Установка пакета {#installation}

Мы периодически собираем пакет **yandex-solomon-agent-bin** для разных версий Ubuntu и публикуем их в следующие репозитори:
  * yandex-precise
  * yandex-trusty
  * yandex-xenial
  * yandex-bionic
  * yandex-cloud

Если подключен один из этих репозиториев, то актуальные версии пакетов можно посмотреть в apt:
```bash
$ sudo apt update
$ apt show yandex-solomon-agent-bin
Package: yandex-solomon-agent-bin
Version: 1:13.2
Priority: optional
Section: misc
Maintainer: Sergey Polovko <jamel@yandex-team.ru>
Installed-Size: 163 MB
Homepage: http://www.yandex.ru
Download-Size: 31.0 MB
APT-Sources: http://yandex-cloud.dist.yandex.ru/yandex-cloud stable/amd64/ Packages
Description: https://wiki.yandex-team.ru/solomon/
```

В пакете приезжает только бинарник Агента, пакет с конфигами нужно будет сделать самостоятельно. В такой пакет нужно будет положить два конфига.
1. В зависимости от версии Ubuntu понадобится конфиг для upstart или systemd. За основу можно взять следующие примеры:

    {% list tabs %}

    - Systemd

      ```
      [Unit]
      Description=Solomon agent
      AssertFileIsExecutable=/usr/local/bin/solomon-agent
      AssertFileNotEmpty=<<<PUT_THE_PATH_TO_YOUR_CONFIG_HERE>>>
      After=multi-user.target

      [Service]
      User=nobody
      Group=nogroup

      ExecStart=/usr/local/bin/solomon-agent --config <<<PUT_THE_PATH_TO_YOUR_CONFIG_HERE>>>

      KillMode=mixed
      KillSignal=SIGTERM
      TimeoutStopSec=5
      SendSIGHUP=no
      Restart=on-failure

      [Install]
      WantedBy=multi-user.target
      ```

    - Upstart

      ```
      description "Solomon agent"

      start on runlevel [2345]
      stop on runlevel [!2345]

      respawn
      respawn limit unlimited
      normal exit 0

      kill timeout 5

      setuid nobody
      setgid nogroup

      script
          exec /usr/local/bin/solomon-agent --config <<<PUT_THE_PATH_TO_YOUR_CONFIG_HERE>>>
      end script
      ```

    {% endlist %}

2. Конфиг для самого Агента (см. [Конфигурирование](#configuration) ниже)

## Сборка из исходников {#build}

Исходники Агента [лежат в Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent), поэтому, чтобы его собрать, нужно иметь копию Аркадии или сделать [селективный чекаут](https://wiki.yandex-team.ru/yatool/clone/).

Допустим, можно сделать селективный чекаут:
```bash
$ svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone
$ cd arcadia
$ ./ya make --checkout -r solomon/agent/bin
```

Бинарник Агента, полученный в результате сборки, будет доступен по пути `solomon/agent/bin/solomon-agent`.

## Поддерживаемые режимы {#modes}
Агент поддерживает два режима работы (в т.ч. одновременно): **Pull** и **Push**.
- В режиме **Pull** Агент собирает данные в локальное хранилище и запускает http сервер, к которому обращается Solomon Fetcher (см. [HttpServer](#httpserver)). Сервер отдает сенсоры через ручку `/storage/read`, [см. раздел про настройки Фетчера](#settings-ui).  Этот режим подходит для подавляющего большинства пользователей.
- В режиме **Push** Агент сам отправляет данные в Solomon через [PUSH API](https://wiki.yandex-team.ru/solomon/api/push/). Этот режим нужен только в специфических ситуациях, когда Pull по какой-то причине не подходит. Если вы считаете, что это ваш случай, [проконсультируйтесь](mailto:solomon@yandex-team.ru) с командой Соломона перед использованием.  Информация о хостах, на которые нужно отправлять данные, указывается в конфиге (см. [Push](#push))

## Конфигурирование {#configuration}

Конфигурация Агента выполняется посредством одного **конфига Агента** (путь к этому файлу передается через параметр `--config` при запуске Агента) и одного или нескольких **сервисных конфигов**. Конфиг Агента обрабатывается один раз при старте демона, конфиги сервисов перечитываются (или в случае python динамически генерируются) в соответствии с настройками [ConfigLoader'а](#configloader). Если перечитывать/динамически генерировать сервисные конфиги не требуется, то можно всю конфигурацию описать в одном конфиге Агента (см. [ConfigLoader::Static](#configloader)).
В Аркадии есть [примеры](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent/examples) конфигов для различных режимов использования Агента.

### Конфиг Агента {#config-file}

Структура конфига Агента задана в виде [protobuf-сообщения](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent/protos/agent_config.proto). Файл конфига - текстовое представление данной структуры в форматах proto или json. На пример конфига можно посмотреть [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent/examples/example.conf).
Конфиг Агента состоит из следующих секций:

#### Labels
**Labels** — значения общих лейблов, которые будут добавляться в отправляемые сенсоры. В формате `key=value`:

{% cut "пример" %}

```
Labels: [
    "host=test-host",
    "key1 = value1",
    "key2=value2"
]
```

{% endcut %}

##### Logger
**Logger** - настройки логирования, доступные опции:

- _LogTo_ - куда записывать лог. Допустимые значения `STDERR`, `FILE`, `SYSLOG`
- _Level_ - минимальный уровень логирования. доступные уровни в порядке возрастания: `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`
- _LogFile_ - полный путь к файлу лога, если был выбран `LogTo: FILE`

{% cut "пример" %}

```
Logger {
  LogTo: FILE
  Level: INFO
  LogFile: "/some/path/to/log/file"
}
```

{% endcut %}

#### HttpServer
**HttpServer** - (Pull режим) настройки HTTP-сервера, посредством которого будут отдаваться сенсоры в Solomon

- _BindAddress_, _BindPort_ - адрес и порт, на котором будет слушать Агент
- _MaxConnections_ - максимальное количество соединений
- _OutputBufferSize_ - размер буфера для формирования ответа
- _MaxQueueSize_ - максимальный размер очереди для ожидающих запросов
- _ThreadPoolName_ - пул, который будет использоваться для обслуживания запросов (опционально, по умолчанию Default). Если задан пул отличный от Default, то его нужно определить в секции [ThreadPoolProvider](#threadpoolprovider)
- {% cut "DEPRECATED поля" %}

- _ThreadsCount_ - количество потоков (DEPRECATED 1:7.0)

{% endcut %}

{% cut "пример" %}

```
HttpServer {
    BindAddress: "::"
    BindPort: 8080
    MaxConnections: 10
    OutputBufferSize: 4194304
    ThreadPoolName: "Io"
    MaxQueueSize: 100
}
```

{% endcut %}

#### AuthProvider
**AuthProvider** - настройки методов аутентификаци/авторизации, далее — auth (опциональная секция).

Данная секция позволяет указать различные auth методы, которые будут использоваться в других секциях, например: **Push**, **HttpServer**, **Registration**.

Параметры:
- _ThreadPoolName_ (опционально) - тредпул, который будет использоваться для выполнения запросов на обмен токенов. По умолчанию: пул **Default**.
- _AuthMethods_ - перечисление auth методов. Возможные варианты:
  - TvmConfig:
    - _ClientId_ — id TVM приложения, от которого пушатся данные
    - _SecretFile_ — путь к файлу c секретом
    - _Cluster_ — тип кластера Соломона. Агент сам подставит нужный TvmId для заданного кластера. Текущие значения:
      - `PRODUCTION`
      - `PRESTABLE`
      - `TESTING`
      - `CLOUD_PROD`
      - `CLOUD_PREPROD`
    - _CustomDstId_ (опционально) — вместо использования `Cluster` можно явно указать id TVM приложения
  - MetadataServiceConfig — Агент сам получит IAM токен из [метаданных виртуальной машины Облака](https://cloud.yandex.ru/docs/compute/operations/vm-info/get-info)
    - _InstanceType_ - тип вм: `UNDERLAY` или `OVERLAY`
    - _Url_ - вместо _Instancetype_ можно указать прямой url к сервису метаданных
    - _UpdatePeriod_ (опционально) — как часто должны ротироваться токены. По умолчанию: `"1h"` (1 час)
  - IamConfig:
    - _ServiceAccountId_ — id сервисного аккаунта (не логин)
    - _KeyId_ - id авторизационного ключа
    - _PublicKeyFile_ — путь к файлу со значением публичного ключа
    - _PrivateKeyFile_ — путь к файлу со значением приватного ключа
    - _Cluster_ — тип кластера Соломона. Агент сам подставит нужный grpc endpoint для заданного кластера. Текущие значения:
      - `CLOUD_PROD`
      - `CLOUD_PREPROD`
      - `CLOUD_GPN`
    - _CustomGrpcAddress_ (опционально) — вместо использования `Cluster` можно явно указать gRPC адрес, по которому происходит выдача IAM токенов
    - _UpdatePeriod_ (опционально) — как часто должны ротироваться токены. По умолчанию: `"1h"` (1 час)
  - OAuthConfig:
    - _SecretFile_ - путь к файлу со значением токена
{% cut "пример" %}

```
AuthProvider {
    ThreadPoolName: "Default"  # можно указать другой thread pool

    AuthMethods: [
        {
            Name: "iam_gpn"
            IamConfig {
                ServiceAccountId: "<service_account_id>"
                KeyId: "<key_id>"
                PublicKeyFile: "public.key"
                PrivateKeyFile: "private.key"
                Cluster: CLOUD_GPN
            }
        }
    ]
}
```

{% endcut %}

#### Push
**Push** - настройки Push режима Агента, при котором данные отправляются напрямую в Соломон

- _Endpoints_ (с 16.5) — перечисление хостов/кластеров, на которые будут отправляться данные
  - _Type_ — тип кластера Соломона. Агент сам подставит нужный Url для заданного кластера. Текущие значения:
    - `PRODUCTION`
    - `PRESTABLE`
    - `TESTING`
    - `CLOUD_PROD`
    - `CLOUD_PREPROD`
  - _Url_ (взаимоисключающий с Type) — `http(s)://fqdn[:port][/path]` (например, `https://localhost:6666/my/endpoint?param1=value1`).
      **Важно!** При использовании `Url` вместо `Type` придётся прописать дополнительные параметры для IAM или TVM авторизации
  - _AuthMethod_ — название auth метода. См. [AuthProvider](#authprovider)


- _Shards_ — перечисление шардов локального хранилища, данные из которых будут отправляться
- _AllShards_ — `true` или `false`. Указывает на то, что данные нужно отправлять из всех шардов (взаимоисключающее к _Shards_)
- _Cluster_ - значение кластера, отправляется вместе с данными каждого шарда в связке ` (project; cluster; service) `
- _PushInterval_ - (опционально) интервал по отправке данных, по умолчанию — `"15s"`. См. про [интервалы в Агенте](#time-grid)
- _RetryInterval_ - (опционально) интервал, через который Агент снова попытается отправить данные при неудачных запросах, по умолчанию `"3s"`
- _RetryTimes_ - (опционально) количество попыток отправить данные при неудачных запросах, по умолчанию `3`
- _MaxInflight_ - (опционально) максимальное количество одновременно отправляемых запросов (по умолчанию: 100)
- _RequestQueueSizeLimit_ - (опционально) максимальное количество запросов в очереди Http клиента. Если размер очереди доходит до лимита, новые запросы не добавляются в очередь, пока ранее добавленные запросы не обработаются
- _ShardKeyOverride_ - (опционально) правило для конструирования ключей новых шардов из данных другого шарда
  - _Project_ - правило для конструирования нового значения **project**
  - _Cluster_ - правило для конструирования нового значения **cluster**
  - _Service_ - правило для конструирования нового значения **service**
  Каждое поле может быть задано в явном (`Service: "new_service_value"`) или параметризованном виде (`Cluster: "{{folder_id}}"`).
  Если у вас есть данные для шарда ` (project=MyProject; cluster=MyCluster; service=MyService) ` (иногда значение `cluster` может быть опущено), то перед их отправкой в Соломон Агент может сгруппировать сенсоры в новые шарды, ключи которых конструируются с помощью опции **ShardKeyOverride**. Если правило **ShardKeyOverride** задано в параметризированном виде (например, `Project: "{{cloud_id}}"`), то для создания нового значения **project** Агент будет искать метку **cloud_id** и после вставит её значение в **project** (**Важно:** если найти метку не удалось, Агент выставит значение из ключа начального шарда*. В данном примере — `MyProject`). Если же правило указано явно, то значением будет являться то, что указано в правиле. Сгруппированные в новые шарды сенсоры отправляются в Соломон с новыми значениями **project, cluster, service**.
  \* Значение **cluster** в push режиме Агент берёт из поля `Cluster` Push конфига.

    {% cut "пример конфига" %}

    ```
    ShardKeyOverride {
      Project: "{{project_id}}" # value of a "project" label will be substituted with the value of a "project_id" label
      Cluster: "cluster_value"  # value of a "cluster" label will be set to "cluster_value" for all sensors
      Service: "{{service_id}}" # value of a "service" label will be substituted with the value of a "service_id" label
    }
    ```

    {% endcut %}

    {% cut "пример разбиения" %}

    ```json
    {"sensors": [
    {
      "kind": "GAUGE",
      "labels": {
        "sensor": "sensor1",
        "project_id": "project1",
        "service_id": "service1"
      },
      "value": 123
    },
    {
      "kind": "COUNTER",
      "labels": {
        "sensor": "sensor2",
        "project_id": "project2",
        "service_id": "service2"
      },
      "value": 456
    },
    {
      "kind": "COUNTER",
      "labels": {
        "sensor": "sensor3",
        "project_id": "project1",
        "service_id": "service1"
      },
      "value": 456
    }
    ]}
    // => (project=project1; cluster=cluster_value; service=service1): [sensor1, sensor3]
    // => (project=project2; cluster=cluster_value; service=service2): [sensor2]
    ```

    {% endcut %}

- _ThreadPoolName_ - (опционально) пул, который будет использоваться для обслуживания запросов (по умолчанию: Default). Если задан пул отличный от Default, то его нужно определить в секции [ThreadPoolProvider](#threadpoolprovider)

- {% cut "DEPRECATED поля" %}

  - _Hosts_ (DEPRECATED с 16.5) — перечисление хостов, на которые будут отправляться данные
    - Новая запись:
      - _Url_ — `http(s)://fqdn[:port][/path]` (например, `http://solomon-prestable.yandex.net/push`)
    - Старая запись (!!**DEPRECATED**!!):
      - _Host_ — `[http(s)://]fqdn[:port]` (значение path всегда равно `/push`)
      - _Port_ — значение порта

{% endcut %}

{% cut "пример" %}

```
AuthProvider {
    AuthMethods: [
        {
            Name: "push"
            OAuthConfig {
                SecretFile: "/path/to/oauth.secret"
            }
        }
    ]
}

Push {
  # Data from all specified shards will be sent to all specified hosts
  Endpoints: [
      {
          Type: PRODUCTION
          AuthMethod: "push"
      },
      {
          Url: "http://localhost:6666"
      }
  ],
  AllShards: true
  # OR
  # Shards: [
  #     {
  #         Project: "my_project"
  #         Service: "my_service"
  #     }
  # ]
  Cluster: "my_cluster"
  PushInterval: "15s" # How often should push data (Default: "15s")
  RetryInterval: "1s" # Retry delay on failed requests (Default: "3s")
  RetryTimes: 3 # How many times should resend data (Default: 3)
  ThreadPoolName: "Io"
}
```

{% endcut %}

Важно: при Push режиме Агент сам должен выставлять значение метки _host_. Это можно сделать через конфиг, указав `Labels: [ "host=host_value" ]`, или выставив на машине env `SA_HOST`.

#### Storage
**Storage** - настройки локального хранилища для собираемых сенсоров
- _Limit_ — настройки лимитов хранилища
- _Total_ — максимальное количество памяти, которое Агент может использовать для хранения данных по всем шардам. В формате `1B, 1KiB, 1MiB, 1GiB`
- _ShardDefault_ — максимальное количество памяти, которое Агент может использовать для хранения данных одного шарда
- _Shard_ — настройки лимитов хранилища, для конкретного шарда (имеют больший приоритет, чем _ShardDefault_)
- _Project_ — проект, для которого определён данный шард
- _Service_ — сервис, для которого определён данный шард
- _Limit_ — максимальное количество памяти, которое Агент может использовать для хранения данных этого шарда. В формате `1B, 1KiB, 1MiB, 1GiB`
- _AggregationOptions_ - настройки предагрегации сенсоров на стороне Агента
- _AggregationInterval_ - интервал, в течение которого будут агрегироваться сенсоры, в формате `"<number><unit>"`. См. про [интервалы в Агенте](#time-grid)
    На текущий момент:
    * агрегация поддерживается только для сенсоров типов **GAUGE** и **IGAUGE** (причина описана в [SOLOMON-3486](https://st.yandex-team.ru/SOLOMON-3486#5c9a0fb1aeebac001ffb2484) )
    * функция агрегации — сумма
    * Если в Агент отправляются данные с проставленным значением ts, то это значение должно лежать в текущем интервале агрегации. Если в данных нет значения ts, то Агент сагрегирует эти данные в текущем интервале.

- {% cut "DEPRECATED поля" %}

  - _BufferSize_ - размер in-memory буфера используемого для хранения накопленных данных, задается в количестве блоков (устарело с версии 1:13.5)

  {% endcut %}

{% cut "Возможные вопросы" %}

  **Q:** У нас на машине `128MiB` памяти. Если выставить это значение в настройках Агента, правда ли, что больше `128MiB` он потреблять не будет?
  **A:** В текущей версии Агента лимиты _Limit_ и _Shard_ ограничивают лишь память, которую Агент может использовать для хранения данных, но не ограничивают память, которую Агент использует во время их обработки. Например, если лимит хранилища выставлен в `75MiB`, в хранилище лежит ровно `75MiB` данных и Агенту прислали новый набор данных на `10MiB`, то память, используемая Агентом на момент обработки этих данных, будет выше `75MiB`. Но кол-во данных, которое после обработки будет лежать в хранилище, лимит в `75MiB` не превысит.

  **Q:** Что произойдёт, если я попытаюсь записать в Агент больше данных, чем указано в ограничении? Например, лимит хранилища выставлю в `3MiB`, а данных пришлю `5MiB`.
  **A:** Агент не будет записывать эти данные, т.к. они не влезут в хранилище. Агент также сообщит об этом в лог с уровнем WARN.

  **Q:** Что произойдёт, если места в хранилище уже нет, но я хочу записать новые данные, которые в него влезают? Например, лимит шарда — `75MiB`, размер новых данных — `10MiB`.
  **A:** Агент будет вымывать самые старые данные, которые были записаны в этот шард, и запишет новые.

  **Q:** Что если места в каждом шарде хватает, но общий лимит подходит к концу? Например, `Total: 10MiB, ShardDefault: 3MiB`, 3 шарда заполнены полностью, а в 4-ый пишется `2MiB` данных.
  **A:** В данном случае, чтобы записать данные в 4ый шард, Агент должен освободить место из предыдущих трёх — на текущий момент такая функциональность не поддерживается, поэтому Агент пропустит запись и сообщит об этом в лог с уровнем ERROR.

  **Q:** Есть ли разница между тем, записывать данные по частям или одним большим куском?
  **A:** Хранилище Агента представляет собой кольцевой буфер, в котором каждый набор данных, записанный за один запрос, кладётся в отдельную ячейку. Все последующие манипуляции с данными происходят на уровне ячеек. К примеру, если Агенту будет нужно вымыть старые данные, то удалять он будет самую старую ячейку. При записи, если за один раз в Агент прислали больше данных, чем может влезть в хранилище, Агент отклонит запись сразу всей ячейки.

  **Q:** Как работают лимиты хранилища с агрегацией?
  **A:** В текущей версии Агент в режиме агрегации за указанный в настройках период сначала накапливает значения агрегатов, а потом записывает их в хранилище, поэтому лимиты влияют на то, сколько финальных агрегатов будет записано. Размер накапливаемых данных до записи не учитывается.

{% endcut %}

{% cut "пример" %}

```
Storage {
    # BufferSize: 128 # (DEPRECATED: SOLOMON-3475)
    Limit {
        Total: "100MiB"
        ShardDefault: "10MiB"
    }

    # Overrides ShardDefault for specific shards
    Shard {
        Project: "my_project",
        Service: "my_service",
        Limit: "75MiB"
    }

    Shard {
        Project: "my_project",
        Service: "another_service",
        Limit: "20MiB"
    }

    AggregationOptions {
        AggregationInterval: "2s"
    }
}
```

{% endcut %}

#### ConfigLoader
**ConfigLoader** - настройки загрузчика service-конфигов. Доступно 3 вида загрузчиков:
- FileLoader - загружает конфиги с локальной файловой системы, доступные опции:
  - _UpdateInterval_ - определяет как часто нужно перечитывать конфиги, задается в виде строки следующего формата: `"<number><unit>"`. См. про [интервалы в Агенте](#time-grid)
  - _ConfigsFiles_ - список путей к файлам с service-конфигами
  - _ConfigsDir_ - путь к директории, относительно которой нужно искать файлы, указанные в ConfigFiles
  - _LoadFromDir_ - путь к директории, все файлы из которой будут загружены как service-конфиги
- Python2Loader - запускает python-модуль для генерации service-конфига
  - _UpdateInterval_ - определяет как часто нужно запускать модуль для генерации конфигов, задается в виде строки следующего формата: `"<number><unit>"`. См. про [интервалы в Агенте](#time-grid)
  - _FilePath_ - путь к python-файлу с модулем
  - _ModuleName_ - уникальное имя для python-модуля
  - _ClassName_ - определяет имя класса, который будет загружен из указанного python-файла
  - _Params_ - набор строковых key=value параметров, которые будут переданы в конструктор python-модуля в виде kwargs
- Static - статические (не обновляемые) сервис-конфиги

{% cut "пример" %}

```
ConfigLoader {
    FileLoader {
        UpdateInterval: "30s"
        ConfigsFiles: [
            "/full/path/to/a/service1.conf",   # make sure to place comma here
            "/full/path/to/a/service2.conf"    # never place comma here!
        ]
    }

    Python2Loader {
        UpdateInterval: "30s"
        FilePath: "/full/path/to/a/config_loader.py"
        ModuleName: "my_module",
        ClassName: "MyConfigLoader"

        # additional params (dict string => string)
        Params {
          key: "key1"
          value: "value1"
        }
        Params {
          key: "key2"
          value: "value2"
        }
    }
    Static {
        Services {
            # same content as in separate service config (see examples bellow)
            Project: "project-a"
            Service: "service-b"
            # ...
        }
    }
}
```

{% endcut %}

#### Python2
**Python2** - глобальные настройки встроенного интерпретатора
  - _IgnorePycFiles_ - позволяет принудительно отключить использование файлов с скомпилированным байкодом

{% cut "пример" %}
```
Python2 {
    IgnorePycFiles: true
}
```

{% endcut %}

#### ManagementServer
**ManagementServer** - настройки HTTP-сервера, который отдаёт информацию о работе самого Агента. Полезно для отладки
  - _BindAddress_, _BindPort_ - адрес и порт, на котором будет слушать сервер
  Доступные ручки:
  `/modules(/json)?` — статус загруженных модулей в HTML/JSON;
  `/counters(/json|/spack)?` — служебные метрики Агента в HTML/JSON/SPACK
  `/config(/plain)` — корневой конфиг, с которым был запущен Агент (`/config` — HTML страница, `/config/plain` — plain text)

#### Modules
**Modules** - настройки модулей Агента (stateful-модулей)
- HttpPush - модуль позволяющий push-ить в Агент сенсоры в одном из поддерживаемых Solomon форматов: [json](https://wiki.yandex-team.ru/solomon/api/dataformat/json/) или [spack](https://wiki.yandex-team.ru/solomon/api/dataformat/spackv1/)
  - _Name_ - опциональное человекочитаемое имя для данного модуля (будет отображаться на странице в management UI)
  - _BindAddress_, _BindPort_ - адрес и порт, на котором будет слушать HTTP-сервер
  - _ThreadPoolName_ - пул, который будет использоваться для обслуживания запросов (опционально, по умолчанию Default)
  - _Handlers_ - настройки ручек обрабатывающих входящие запросы
    - _Endpoint_ - путь ручки
    - _Project_, _Service_ - обязательные метки, которые будут добавляться ко всем сенсорам обрабатываемым данной ручкой
  - {% cut "DEPRECATED поля" %}

      - _ThreadCount_ - количество потоков (DEPRECATED с 1:7.0)

  {% endcut %}
- GraphitePush - модуль позволяющий push-жить в Агент сенсоры в [текстовом формате Graphite](https://graphite.readthedocs.io/en/latest/feeding-carbon.html#the-plaintext-protocol)
  [читать подробнее](modules.md#graphite-push)

{% cut "пример" %}

```
Modules {
    HttpPush {
        Name: "MyPushModule"
        BindAddress: "::"
        BindPort: 8082
        ThreadPoolName: "Io"

        Handlers {
            Project: "my-project"
            Service: "my-service"
            Endpoint: "/push-to-me"
        }
    }
}
```

{% endcut %}

[Подробнее про встроенные модули](modules.md)

#### ThreadPoolProvider
**ThreadPoolProvider** - настройки пулов потоков (опциональная секция).
  Данная секция позволяет управлять настройками используемых пулов потоков различными компонентами Агента (http-сервер, puller, pusher и тд). Если данная секция отсутствует Агент будет использовать пул с именем `Default`, 4 потоками и неограниченной очередью задач на выполнение.
  Доступные настройки каждого пула:

- _Name_ - уникальное имя пула потоков. Пул с именем `Default` используется другими компонентами по-умолчанию (если не указан любой другой пул).
- _Threads_ - количество потоков в пуле
- _MaxQueueSize_ - размер очереди задач на выполнение (0 - неограниченная очередь).

{% cut "пример" %}

```
ThreadPoolProvider {
  ThreadPools: [
    {
      Name: "Io"
      Threads: 8
      MaxQueueSize: 128
    },
    {
      Name: "Default"
      Threads: 4
    }
  ]
}
```

{% endcut %}

### Service-конфиг {#service-file}

Структура service-конфига задана в виде [protobuf-сообщения](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent/protos/service_config.proto). Файл конфига - текстовое представление данной структуры в форматах proto или json. На пример конфига можно посмотреть [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent/examples/service.example.conf).
Конфиг состоит из следующих секций:

1. _Project_ - имя проекта
2. _Service_ - имя сервиса
3. _Labels_ - дополнительные метки, которые нужно добавить к каждому сенсору
4. _PullInterval_ - определяет как часто нужно вызывать pull-модули, задается в виде строки следующего формата: `"<number><unit>"`. Данная опция может быть предопределена в настройках конкретного pull-модуля. См. про [интервалы в Агенте](#time-grid)
5. _Modules_ - настройки pull-модулей для данного сервиса. На данный момент поддерживаются 5 [pull-модуля](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent/modules/pull):

- http - скачивает сенсоры по указанному URL в одном из поддерживаемых Solomon форматов: [json](https://wiki.yandex-team.ru/solomon/api/dataformat/json) или [spack](https://wiki.yandex-team.ru/solomon/api/dataformat/spackv1) или prometheus
- porto - собирает основные сенсоры из portod
- python2 - позволяет написать произвольный модуль для сбора сенсоров на python
- system - собирает системные сенсоры текущего хоста (аналогичные тем, которые собирает [sysmond](https://wiki.yandex-team.ru/solomon/sysmond/))
- unistat - умеет забирать сенсоры в unistat-формате Голована

{% note warning %}

Пара `(project, service)` должна быть уникальной в рамках всей конфигурации Агента. Другими словами, не должно быть двух и более service-конфигов (сгенерированных python-скриптом или загруженных из файлов) с одинаковыми значениями `project` и `service`.

{% endnote %}

### Service-конфиг в админке Соломона {#settings-ui}
В поле **Fetch URL** необходимо указать `/storage/read?project=<project>&service=<service>`, где `project` и `service` соответствуют значениям, указанным ранее в конфиге Агента.

## Авторизация в Push режиме доставки данных {#auth}
См. [Push](#push) > Endpoints > Авторизация

Примеры конфигурации — [тут](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent/examples/push/push-auth)

{% cut "DEPRECATED способ (до 16.5)" %}

Агент поддерживает переменные окружения, через которые выставляется значение токена, отправляемого вместе с данными в push режиме доставки данных:
- _SA_AUTH_TYPE_ - тип токена. Поддерживаемые типы: **OAuth**, **IAM** (case-insensitive)
- _SA_AUTH_TOKEN_ - значение токена.

{% endcut %}

### Как получить credentials {#credentials}

{% cut "OAuth" %}

1. Зарегистрировать [роботного пользователя](https://wiki.yandex-team.ru/diy/zombik/)
2. Залогиниться под роботным пользователем (совет: используйте incognito mode в своем браузере)
3. Открыть ссылку [https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1c0c37b3488143ff8ce570adb66b9dfa](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1c0c37b3488143ff8ce570adb66b9dfa)
4. Убедиться в том, что у робота есть права на чтение (Read) и обновление (Update) в вашем проекте

![](https://jing.yandex-team.ru/files/jamel/Project_Solomon__Solomon__Admin_2019-03-29_16-47-08.png)


{% endcut %}

{% cut "IAM" %}

1. [Документация Облака](https://cloud.yandex.ru/docs/iam/operations/authorized-key/create)
2. У сервисного аккаунта должен быть permissioin `monitoring.data.write` в Облаке, в которое будут пушиться данные

{% endcut %}

{% cut "TVM" %}

1. [Документация TVM](https://wiki.yandex-team.ru/passport/tvm2/quickstart/)
2. В настройках проекта в Соломоне нужно выдать права пользователю `tvm-{id_приложения}`. Например, `tvm-666666`.

{% endcut %}

## Интервалы в Агенте {#time-grid}

Интервалы обновления конфигов, сбора данных из модулей и т.п. в Агенте выровнены по сетке. Это значит, что Агент будет запускать действие только тогда, когда текущее время кратно интервалу.

Допустим, Агент собирает данные из модулей каждые 15 секунд. Тогда сервис-конфиг будет иметь вид:

```
Project: "some_project"
Service: "some_service"

PullInterval: "15s"

Modules: [
...
]
```

Если Агент с таким конфигом будет запущен в `13:17:03`, то он не будет запрашивать модуль сразу, а дождётся  кратного времени `13:17:15`. Таким образом, времена опроса Агентом будут:

```
13:17:15
13:17:30
13:17:45
...
и т.д.
```

* Аналогично для `UpdateInterval` в секции `ConfigLoader`, `PushInterval` в секции `Push` и др.
* Исключения: интервалы ретраев


## Примеры конфигурации {#config-examples}
Примеры конфигурации для ознакомления с Агентом можно найти [в репозитории](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent/examples)

## Отладка {#debug}
Проверить наличие данных в Агенте после их сбора:
```bash
$ curl -g "http://[::1]:9666/storage/read?project=my_project&service=my_service&pretty=true"
```

Также может быть полезно получать сенсоры о работе самого Агента: количество потребляемой памяти, uptime, cpu и пр. Подробнее см. настройку [ManagementServer](#managementserver).
