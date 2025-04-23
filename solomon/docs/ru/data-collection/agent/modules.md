## Push {#push}
### HTTP push {#http-push}

Агент будет слушать на заданном порту. Формат push-сообщений соответствует [формату](https://wiki.yandex-team.ru/solomon/api/push/) push API Соломона. Если нужно получать метрики по нескольким проектам, в конфигурации можно указывать несколько `Handlers` с разным значением `Endpoint`

Пример конфигурации:

```
Modules {
...
    HttpPush {
        BindAddress: "::"
        BindPort: 10050
        ThreadCount: 2
        Name: "httpPush"

        Handlers {
            Project: "my-project"
            Service: "my-service"

            Endpoint: "/"
        }
    }
}
```

### Graphite push {#graphite-push}

Агент способен принимать метрики в [текстовом формате Graphite](https://graphite.readthedocs.io/en/latest/feeding-carbon.html#the-plaintext-protocol) и конвертировать их в метрики Solomon по заданным правилам.

Конфиг представляет собой текстовое представление proto message, определенного [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/agent/modules/agent/graphite/protos/graphite_config.proto). Правила содержат в себе паттерн, по которому находятся соответствующие метрики, и набор шаблонов, которые определяют метки, которые будут присвоены метрике после преобразования. При этом метки могут содержать как константные значения, так и обращения к частям имени исходной метрики, разделенным точкой (индексация с 1).

Если метрика соответствует нескольким паттернам, будет использован только первый.

Пример:

```
Metrics {
    Pattern: "*.foo.*"
    LabelMappings {
        Label: "label1"
        Template: "$1"
    }

    LabelMappings {
        Label: "label2"
        Template: "$2_with_string"
    }

    LabelMappings {
        Label: "constLabel"
        Template: "helloWorld"
    }
}
```

Результат:
Метрика `bar.foo.baz` будет преобразована в метрику с метками `{"label1": "bar", "label2": "baz_with_string", "constLabel": "helloWorld"}`. Все метрики будут иметь тип `GAUGE`.

Обработку метрик, которые не соответствуют ни одному паттерну из конфига можно задать параметром Mode:
- AS_IS — метрика будет преобразована в метрику с единственной меткой `{"sensor": $metric_name}`;
- IGNORE — метрика будет проигнорирована.

Полный пример конфига:

```
GraphitePush {
        BindAddress: "::"
        BindPort: 10050
        ThreadCount: 4

        Service: "test-service"
        Project: "test-project"

        MappingRules {
            Mode: AS_IS
            Metrics {
                Pattern: "*.foo.*"
                LabelMappings {
                    Label: "label1"
                    Template: "$1"
                }

                LabelMappings {
                    Label: "label2"
                    Template: "$2_with_string"
                 }

                 LabelMappings {
                     Label: "constLabel"
                     Template: "helloWorld"
                 }
            }
        }
    }
```

Ограничения:
- Не больше 10 wildcards в паттерне метрики;
- Имя и значение метки содержат только следующие символы: `[a-zA-Z0-9-_.]`

## Pull {#pull}

{% note warning %}

Обратите внимание: если в Агент из Pull модулей поступают данные метрик без значения ts (кроме типов **RATE** и **HIST_RATE**), то значение ts выставляется как время, выровненное по сетке размера интервала. К примеру, если интервал сбора 15 секунд, а точка приходит во время 17:23:42, то значение ts будет выставлено как 17:23:30.

Значение ts для типов **RATE** и **HIST_RATE** всегда остаётся без изменения

{% endnote %}

### System {#system}
Агент будет периодически собирать системные метрики. Поддерживаемые ОС — Linux и MacOS. Полный список метрик есть [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/solomon/libs/cpp/sysmon/proto/sysmon_metrics.proto). Для MacOS поддерживаются не все из них.

{% cut "подробнее про метрики на macOS" %}

Метрики, отсутствующие на macOS в виду отсутствия объекта измерения в ОС, либо неочевидности способа измерения:

System:
* /System/IoWaitTime
* /SystemIrqTime


Proc:
* /Proc/ProcsSinceBoot

Memory:
* /Memory/Buffer
* /Memory/Cached
* /Memory/SwapCached
* /Memory/ActiveAnon
* /Memory/InactiveAnon
* /Memory/ActiveFile
* /Memory/InactiveFile
* /Memory/Mlocked
* /Memory/Dirty
* /Memory/Writeback
* /Memory/Mapped
* /Memory/Shmem
* /Memory/Committed_AS
* /Memory/CommitLimit
* /Memory/Slab
* /Memory/AnonHugePages
* /Memory/PageTables

Disks:
* /Io/Disks/IOsInProgress
* /Io/Disks/TimeInQueueMillisec
* /Io/Disks/IOMillisec
* /Io/Disks/IOServiceTime

Net:
* Реализован только сбор базовых метрик `SysmonNetIf`, кроме `TxDrop`

{% endcut %}

Если вам не нужно собирать все метрики, часть из них можно убрать, установив нужный уровень в конфиге. Уровень по умолчанию `ADVANCED` для всех разделов. Это сделано для совместимости с sysmond.

На данный момент уровни BASIC и ADVANCED в основном отличаются для сетевых метрик. При BASIC будут собираться только метрики в объеме `SysmonNetIf`

Пример конфигурации:
```
ConfigLoader {
    FileLoader {
        UpdateInterval: "30s"
        ConfigsFiles: [
            "system"
        ]
    }
}
```

Содержимое system:
```
Project: "my-project"
Service: "sys"

PullInterval: "15s"

Modules: [
    { System: {
        Cpu: ADVANCED
        Memory: NONE
        Network: BASIC
        Storage: BASIC
        Io: BASIC
        Kernel: NONE
    }}
]
```

### HTTP pull {#http-pull}

Агент будет периодически опрашивать заданные URL и забирать из них метрики в поддерживаемых форматах [JSON](https://wiki.yandex-team.ru/solomon/api/dataformat/json), [spack](https://wiki.yandex-team.ru/solomon/api/dataformat/spackv1) или [Prometheus text](https://github.com/prometheus/docs/blob/master/content/docs/instrumenting/exposition_formats.md). Для записи метрик лучше использовать [клиентские библиотеки](https://wiki.yandex-team.ru/solomon/libs)

* _Url_ - опрашиваемый url
* _Format_ - формат данных: `JSON`, `SPACK` или `PROMETHEUS`
* _RetryCount_ (опционально) - количество повторных запросов
* _RetryIntervalMillis_ (опционально) - интервал между повторными запросами
* _TimeoutMillis_ (опционально) - таймаут на получение данных от ручки


Пример конфигурации:
```
ConfigLoader {
    FileLoader {
        UpdateInterval: "30s"
        ConfigsFiles: [
            "my_pull_service.conf"
        ]
    }
}
```

Содержимое `my_pull_service.conf`:
```
Project: "my-project"
Service: "my-service"

PullInterval: "15s"

Modules: [
    { HttpPull: {
        Url: "http://localhost:1337/monitoring?format=JSON"
        Format: JSON # or SPACK or PROMETHEUS
    }}
]
```

### Unistat pull {#unistat-pull}

Агент будет периодически опрашивать заданные URL и забирать из них метрики в формате [unistat-ручки Голована](https://wiki.yandex-team.ru/golovan/stat-handle/). При этом теги, записанные в формате `prj=something;ctype=my_ctype;metric_hgram` будут преобразованы в метки `{"prj": "something", "ctype": "metric_hgram"}`. Имя unistat-сигнала будет записано как значение метки `sensor`.

Для гистограмм из-за различия в способе задания интервалов (полуинтервал, задающий корзину, замкнут справа в Соломоне и слева в Головане) точки, попадавшие на границу интервала, будут помещены не в ту корзину.

Известные ограничения:
- следует писать гистограммы с фиксированными границами бакетов, потому что в противном случае с точки зрения Соломона каждая новая граница будет порождать отдельную метрику;
- количество бакетов должно быть меньше либо равно 50.

Пример конфигурации:
```
ConfigLoader {
    FileLoader {
        UpdateInterval: "30s"
        ConfigsFiles: [
            "my_pull_service.conf"
        ]
    }
}
```

Содержимое `my_pull_service.conf`:
```
Project: "my-project"
Service: "my-service"

PullInterval: "15s"

Modules: [
    { Unistat: {
        Url: "http://localhost:1337/unistat"
    }}
]
```

### Python 2 {#python}

Агент будет периодически опрашивать заданный python-модуль, получая из него метрики.

Рассмотрим API на примере написанного модуля:

{% code '../../solomon/agent/examples/modules/pull_module.py' lang='python' %}

{% note warning "На что обратить внимание" %}

* Пользователю следует следить за тем, чтобы код, вызываемый агентом, не мог подвиснуть на неопределенное время. Это может касаться, например, сетевых запросов без разумного таймаута. Иначе пул потоков, выполняющих код модулей, может забиться. В этом случае задачи, которые провисели в очереди на выполнение больше, чем интервал запуска, не будут запускаться, и, как результат, на графиках может появиться no data.
* Хотя при некотором желании из пользовательского модуля можно импортировать сторонние модули, принесенные через pip или каким-то другим способом, эта возможность не поддерживается и не рекомендуется к использованию.

.

{% endnote %}

Пример сервисной конфигурации для данных модулей:

```
Project: "my-project"
Service: "my-service"

Modules: [
    { Python2: {
        FilePath: "modules/examples/pull_module.py"
        ModuleName: "examples"
        ClassName: "MyAwesomePullModule"
    }},

    {
        Python2: {
            FilePath: "modules/examples/pull_module.py"
            ModuleName: "examples"
            ClassName: "MyPoorPullModule"
        }
        PullInterval: "5s"
    }
]
```

### Systemd {#systemd}

Агент опрашивает через dbus указанные сервисы, собирая системные метрики.

* _Pattern_ - **regex**, по которому выбираются сервисы для мониторинга. Парсится библиотекой re2, поддерживаемые операторы можно найти [здесь](https://github.com/google/re2/wiki/Syntax)
* _Cpu_ - собирать CPU метрики сервиса. Значения: **ON**, **OFF**
* _Memory_ - собирать метрики памяти сервиса. Значения: **ON**, **OFF**
* _Network_ - собирать сетевые метрики сервиса. Значения: **ON**, **OFF**

Список собираемых метрик:
Cpu | cpuUsageMs
:-- | :--
Memory | memoryUsageBytes
Network | txBytes, txPackets, rxBytes, rxPackets

Пример сервисной конфигурации:
```
Project: "my-project"
Service: "my-service"

PullInterval: "5s"

Modules: [
    {
        #
        # next section will configure which system metrics will be reported
        # and for what services (units with type 'service').
        # 
        Systemd: {
            Pattern: ".*yandex.*" # regex which will match services by name
            Cpu: ON # report CPU metrics about particular service
            Memory: OFF # do not report memory metrics
            Network: ON # report network metrics
    }}
]
```

{% note warning %}

* Для работы требуется systemd (для ubuntu из коробки версии 16.04+)
* Для сбора network cенсоров версия systemd должна быть не ниже 235
* Для того, чтобы systemd собирал метрики сервиса, в его service файле должны быть взведены следующие флаги в секции Service:

Метрики  | Переменная в .service файле
:--- | :---
CPU      | CPUAccounting
Memory   | MemoryAccounting
Network  | IPAccounting

{% endnote %}

### NvidiaGpu {#nvidia-gpu}

Агент опрашивает через nvidia-smi видеокарты, собирая системные метрики.

* _Path_ - указать кастомный путь к утилите nvidia-smi
* _Gpu_ - собирать GPU метрики видеокарты. Значения: **ON**, **OFF**
* _Memory_ - собирать метрики памяти видеокарты. Значения: **ON**, **OFF**

Список собираемых метрик:
Gpu | Memory
:--- | :---
gpuUsagePercents, gpuTemperatureCelsius | memoryUsagePercents, memoryTemperatureCelsius

Пример сервисной конфигурации:
```
Project: "my-project"
Service: "my-service"

PullInterval: "5s"

Modules: [
    {
        #
        # next section will configure which system metrics will be reported
        # 
        NvidiaGpu: {
            # Path: # custom path to 'nvidia-smi' folder (without trailing slash)
            Gpu: ON # report GPU metrics
            Memory: OFF # do not report memory metrics
    }}
]
```

{% note warning %}

* Для работы требуется утилита nvidia-smi (поставляется в общем пакете с драйвером видеокарты)
* OS: Linux x64 ( nvidia-smi dmon не реализован под Windows)
* Поддерживаются типы карт: Tesla, GRID, Quadro.

{% endnote %}

### Porto {#porto}

{% note warning %}

Для работы этого модуля требуется доступ к porto-сокету

{% endnote %}

Агент будет периодически опрашивать porto API собирая доступные метрики.

Можно собирать метрики как для текущего контейнера, в котором запущен агент (для этого нужно задать `Containerized: true`), так и для списка внешних контейнеров через задание списка маппингов. 

Каждая строчка-маппинг представляет собой регулярку с одной capture-группой. Все контейнеры, имена которых поматчатся этой регуляркой получат метку `name=<значение capture-группы>`. Для контейнеров, которые не поматчатся ни одной регуляркой, метрики собираться не будут.
Если задан пустой список маппингов, будут собраны метрики для всех контейнеров. При этом метка name у них будет соответствовать имени без какого-либо преобразования.

Список собираемых метрик:
* /Containers/CpuUsageMillis
* /Containers/DiskIoReadBytes
* /Containers/DiskIoTimeMillis
* /Containers/DiskIoWriteBytes
* /Containers/Ifs/RxBytes
* /Containers/Ifs/RxDrops
* /Containers/Ifs/TxBytes
* /Containers/Ifs/TxDrops
* /Containers/MajorPageFaults
* /Containers/MemoryUsageBytes
* /Containers/MinorPageFaults
* /Containers/TimeSeconds

Пример сервисной конфигурации для сбора метрик текущего контейнера:
```
Project: "my-project"
Service: "my-service"

PullInterval: "5s"

Modules: [
    { Porto: {
        Containerized: true
    }}
]
```

Пример сервисной конфигурации для сбора метрик произвольных контейнеров:
```
Project: "my-project"
Service: "my-service"

Modules: [
    {
        Porto: {
            Mappings: [
                ".+(yt_.+_nodes).+"
            ]
        }
        PullInterval: "5s"
    }
]
```

Здесь контейнер с именем `ISS-AGENT--9012/9012_vla_yt_arnold_nodes_P6gSGme0toE1` получит метку  name со значением `yt_arnold_nodes`.

## Трансформация данных (c версии Агента 14.8) {#transformations}

{% note warning %}

На текущий момент поддерживается только в Pull модулях

{% endnote %}

Модули поддерживают конфигурацию для трансформации данных (на текущий момент — только меток) в секции **Transformations**. Каждая трансформация указывается внутри отдельного правила, в секции **Rule**. Правил может быть несколько — каждое следующее будет работать на результате выполнения предыдущего.

**Rule** - правило трансформации. Доступные опции:
* _Match_ (опционально) - по каким меткам выбирать метрики, над которыми будет производиться преобразование. Значение: набор меток через запятую в формате [GLOB](https://en.wikipedia.org/wiki/Glob_(programming)). Если **Match** не указан, преобразование будет производиться над всеми метриками.
* _ReplaceMeta_ - правило трансформации меток. Значение: правила трансформации для отдельных меток, через запятую. Поддерживает три операции:
  * `host=-` — удаление метки
  * `host=vla` — добавление/перезапись метки с фиксированным значением
  * `newHost=vla-{{host}}-{{cluster}}` — добавление/перезапись метки с подстановкой значения других меток

  Символы `",", "\", "{", "}", " "` следует экранировать.
  Пример: `ReplaceMeta: "new\ Label={{oldLabel\{\}}}-value"`

Пример (для Pull модуля):
```
Services {
    Project: "test-project"
    Service: "test-service"
    PullInterval: "15s"
    Modules {
        HttpPull {
            Url: "http://localhost:10102/prometheus"
        }
        Transformations {
            Rule {
                Match: "cluster=*, service=*"  # находим метрики с любыми значениями меток cluster и service
                ReplaceMeta: "clusterId=old-{{cluster}}-value, serviceId={{service}}, cluster=-, service=-,  newLabel=fixedValue"
            }

            Rule {
                Match: "clusterId=old-someCluster-value"  # используется метка, которая появилась в результате предыдущего правила
                ReplaceMeta: "anotherLabel=anotherValue"
            }
        }
    }
}
```

{% note warning %}

Обратите внимание: метки, указанные в поле `Match`, обязаны присутствовать в оригинальных данных модуля. К примеру, если указано правило `Match: "cluster=\*, service=\*"`, то метки **cluster** и **service** могут принимать любые значения, но сами метки _обязаны быть_. Это может быть полезно для случаев, когда в данных есть зарезервированные в Соломоне метки **project**, **cluster**, **service** (например, такие может возвращает Prometheus Exporter). Но если в данных нет меток, указанных в правиле `Match`, преобразование не будет выполнено, т.к. ни одна метрика не подходит под соответствие.

{% endnote %}
