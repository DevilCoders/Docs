# Pod

**Pod** — это основная и минимальная единица управления деплоя, агрегирующая сущность для [Box](box.md) и [Workload](workload/workload.md). Для Pod доступны такие настройки как FQDN, net/mount/pid ns. Именно Pod'ы создаются и запускаются в датацентрах, настраивается их количество для распределения нагрузки, Pod'ы отображаются в UI Deploy и мониторингах, имеют свою ревизию и т.д.

В этом разделе собрана документация по настройке свойств пода и объектов Деплоя, находящихся на уровне "pod" и ниже.

Спецификация пода представлена следующей [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/data_model.proto?rev=r8357100#L1105-1486).

На этой странице представлено краткое описание происходящего в поде.
За подробностями - в подстраницы раздела (смотри справа).

Краткое описание некоторых важных разделов:

* [pod_agent_payload](../../concepts/pod/podagentpayload/podagentpayload.md) — документация по части спецификации, отвечающей за внутреннее наполнение пода (ресурсы/алгоритм сборки окружения для приложения/параметры запуска приложения).
* [resource_requests](resource-requests.md) — как задать вычислительные и сетевые ресурсы для пода.
* [secrets](../../how-to/secrets.md) — как передать секреты в под.
* [ip6_address_requests](ip6addressrequests.md) - заказ ipv6 адресов и ipv4 туннелей.

Разделы, которые контролируются внешними контроллерами (заполнение их в спецификации ничего не даст, поскольку их потом перезапишет внешний контроллер):

* [dynamic_resources](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/data_model.proto?rev=6605464#L1244-1245) — описывает [динамические ресурсы](../../concepts/dynamic-resources.md) в поде.
* [resource_cache](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/data_model.proto?rev=6605464#L1252-1253) — описывает ресурсный кеш в поде.

## Объекты в поде

Pod'ы, Box'ы, Workload'ы отличаются доступными атрибутами и уровнями изоляции

* **Pod** – агрегирующая сущность. Для нее доступны: FQDN, net/mount/pid ns.
* **Box(s)** – вложенная в Pod сущность. У каждого бокса есть свой mount/pid/ipc/utc/env ns. Транслируется в porto meta container (контейнер без команды запуска).
* **Workload** – пользовательское приложение: команда для запуска и набор проб для проверки живости. Все запущенные в одном боксе WorkLoad'ы будут иметь общую файловую систему.

Пример использования нескольких боксов: если вы хотите в рамках одного Pod'а (чтобы минимизировать походы по сети) запустить несколько Workload'ов, для работы которых требуется сконфигурировать различные окружения.

Ниже представлено упрощенное изображение структуры пода:
![podstruct](../../_assets/concepts/pod/podstruct.jpg)

Обратите внимание, что на схеме кроме пользовательских боксов есть еще 2 инфраструктурных бокса (c PushAgent и с TVM-Tool) – это примеры так называемых sidecars [читать подробнее](sidecars/sidecars.md).

## Что проиcходит в поде. Кратко

В каждом поде Деплоя живет свой pod_agent (демон-процесс).

Задачи pod_agent:

* скачать ресурсы
* собрать из ресурсов вольюмы и боксы
* запустить в боксах ворклоды
* проверять живость ворклодов (через readiness/liveness пробы)

При каждом деплое в Деплой для каждого пода формируется его новая спека для pod_agent со списком ресурсов, боксов и ворклодов.
Эта спека передается в pod_agent, который начинает приводить объекты к требуемому состоянию.

## Порядок обновления ревизий (версий) объектов

Рассматривается ситуация, когда новый деплой проводится без переаллокации подов (inplace update).

Краткие факты:

* бокс может перейти в новую ревизию без пересборки (если описание бокса - ресурсы, лейеры, etc - не изменилось), в этом случае ревизия бокса может стать больше ревизии его ворклода
* бокс не начнет разбираться, пока в нем есть не-остановленные ворклоды
* разные боксы могут находится в разных ревизиях
* ворклод может перейти в новую ревизию без пересборки (рестарта), если описание ворклода - start command, readiness, liveness, env, etc - не изменилось
* разные ворклоды одного бокса могут находится в разных ревизиях

pod_agent старается быть максимально "ленивым" - не пересобирать (перезапускать) объекты, описание которых не изменилось.

Тем не менее, в худшем случае все объекты будут пересобраны. Например, в новом релизе pod_agent добавилась новая системная переменная -> необходимо пересобрать все боксы.

## Сеть и доступные порты

Вы можете использовать любые незанятые порты.

Порты, занятые инфраструктурой:

порт | демон| описание
---: | :--- | :---
1 | pod_agent | публичный read-only api для пользователей
2 | tvm-tool | по умолчанию используется для проверки "живости" tvm-tool - client_port
3 | juggler-subagent | Для связи juggler subagent и хостового juggler agent. Переопределяемый дефолт.
22 | portoshell | ssh
1234  | logbroker | хуки логброкера
12500-13000 | - | резерв инфраструктуры
12500  | Unified Agent | grpc input для получения данных
12501  | Unified Agent | сенсоры для мониторинга в Solomon
12502  | Unified Agent | статус и хуки агента
12503  | Unified Agent monitoring | хуки процесса мониторинга
12510  | TVM | monitoring port
12520  | Error Booster| HTTP input port 
12521  | Error Booster| SYSLOG input port
12522  | Error Booster| SYSLOG HTTP input port

## Налог на инфраструктуру

В рамках вот этой задачи [https://st.yandex-team.ru/DEPLOY-1649](https://st.yandex-team.ru/DEPLOY-1649) к каждому поду будут добавлены следующие лимиты:

1) 0.1 CPU
1) 200 MB RAM
1) 1 GB hdd disk

## SSH в pod

Доступ в pod нужен для отладки, если у сервиса возникают какие-то проблемы с запуском.
Для доступа надо использовать команду `ssh root@HOSTNAME`, где **HOSTNAME** — доменное имя вашего pod'а (доступно в UI на вкладке PODS).

При этом вы окажетесь в файловой системе pod-агента и получите доступ ко всей иерархии контейнеров сервиса.

Особенности нашего SSH:

1. X11-форвардинг не поддерживается. Если по какой-то причине он жизненно необходим, приходите, рассмотрим возможность поддержки.
1. Помимо пользователя root есть возможность зайти в сервис от имени своего пользователя, пользователя loadbase или любого другого. При этом надо учитывать, что у вас должен быть приватный ключ соответствующего пользователя и этому пользователю должен быть разрешён вход в контейнер. Несмотря на то, что этого достаточно для входа, надо понимать, что контейнеры, как правило, ничего не знают о сотрудниках (т.е. логинах) Яндекса, и соответствующего пользователя внутри контейнера вероятнее всего просто не существует. Поэтому вы успешно войдёте в контейнер, но де-факто не будете иметь там никаких прав. Используйте эту возможность, если понимаете, что вы делаете.

## Чтение stdout/stderr логов пользовательских контейнеров {#readingstdoutstderr}

### В UI

Включите [поставку логов через LogBroker](./sidecars/logs/logs.md).
Поддержана поставка stdout/stderr только для start (главного) процесса workload.
Логи будут видны во вкладке "Logs".

### Через dctl

```bash
yanddmi@yanddmi-dev[~]:ya tool dctl status pod tadqrfro2eglqr7g -c man
...
      workloads {
        id: "simple_http_server"
        state: EWorkloadState_ACTIVE
        init {
          zero_return_code_counter: 1
          time_limit {
            consecutive_successes_counter: 1
          }
          last {
            state: EContainerState_EXITED
            stdout: "Hello World from workload.init!\n"
            start_time {
              seconds: 1583484260
            }
            death_time {
              seconds: 1583484261
            }
          }
        }
        start {
          current {
            state: EContainerState_RUNNING
            stdout: "Hello World from workload.start!\n"
          }
        }
        readiness_status {
          container_status {
            zero_return_code_counter: 3
            time_limit {
              consecutive_successes_counter: 3
            }
            current {
              state: EContainerState_WAITING_RESTART
            }
            last {
              state: EContainerState_EXITED
              stdout: "Hello World from workload.readiness!\n"
              start_time {
                seconds: 1583484326
              }
              death_time {
                seconds: 1583484326
              }
            }
          }
          has_readiness: true
        }
...
```

### В контейнере pod'а

Через утилиту portoctl:

```bash
yanddmi@yanddmi-dev[~]:ssh -l root tadqrfro2eglqr7g.man.yp-c.yandex.net
root@man2-9399-1:/$ portoctl get pod_agent_box_server/workload_simple_http_server_init0 stdout[:10240]  # print last 10240 bytes of stdout
Hello World from workload.init!

root@man2-9399-1:/$ portoctl get pod_agent_box_server/workload_simple_http_server_start stdout[:10240]
Hello World from workload.start!
```

### В контейнере box'а

1. через утилиту portoctl
утилита должна присутствовать в пользовательском боксе
(в стандартных `*-app` образах ее нет, есть в расширенных `*-os`)

```bash
yanddmi@yanddmi-dev[~]:ssh -6 root@2a02:6b8:c0a:3324:0:696:c269:2
root@man2-9399-1:/$ portoctl get pod_agent_box_server/workload_simple_http_server_init0 stdout[:10240]  # print last 10240 bytes of stdout
Hello World from workload.init!

root@man2-9399-1:/$ portoctl get pod_agent_box_server/workload_simple_http_server_start stdout[:10240]
Hello World from workload.start!
```

1. При включенной поставке логов через LogBroker stdout/stderr start процесса доступны в виде файлов в боксe [тут](./sidecars/logs/logs.md)

1. При выключенной поставке логов можно перенаправить stdout/stderr в файлы. См поля stdout_file/stderr_file/stdout_and_stderr_limit

## Чтение логов pod_agent

### В контейнере pod'а

pod_agent пишет логи в бинарном виде в `<pod_chroot>/pod_agent/public_volume/eventlog` (с ротацией в `<pod_chroot>/pod_agent/public_volume/eventlog.<file_number>`).
Читать их можно с помощью команды `./pod_agent print_log`, находясь в контейнере pod'а.

Пример: чтение логов в формате `tail -f` с фильтрация DEBUG:

```bash
# ssh в контейнер pod'а
yanddmi@yanddmi-dev[~]:ssh -l root tr5fhuzafc3r2hun.vla.yp-c.yandex.net
root@sas4-3270-1:/$ cd pod_agent

root@sas4-3270-1:/pod_agent$ ./pod_agent print_log -t public_volume/eventlog | grep -v DEBUG
1571927932158368	INFO	TContainerAttemptFeedback	{"state":"EContainerState_EXITED","return_code":0,"stderr":"","stdout":"","fail_reason":"","start_time":1571927921000000,"death_time":1571927921000000,"object_type":"WORKLOAD","container_type":"READINESS","init_num":0,"object_id_or_hash":"logbroker_push_client_workload"}
1571927932158483	INFO	TContainerAttemptFeedback	{"state":"EContainerState_EXITED","return_code":0,"stderr":"","stdout":"","fail_reason":"","start_time":1571927921000000,"death_time":1571927921000000,"object_type":"WORKLOAD","container_type":"READINESS","init_num":0,"object_id_or_hash":"logbroker_monitor_workload"}
```
Для чтения логов в формате `tail -f` используется флаг `-t`. В данном случае просмотрщик логов будет ждать изменения файла с логами и выводить эти изменения на экран. По этому, использование флага `-t` целесообразно только на последнем eventlog файле, куда подовый агент пишет логи в текущий момент.

Пример с интерпретацией: что происходило с workload `simple_http_server` в период с 18:36:40 по 18:41:40:

```bash
# ssh в контейнер pod'а
yanddmi@yanddmi-dev[~]:ssh -l root tr5fhuzafc3r2hun.vla.yp-c.yandex.net
root@sas4-3270-1:/$ cd pod_agent

# {-s|--start-time} VAL     Start time (Unix time in microseconds, ISO8601, or HH:MM[:SS] in the last 24 hours).
# {-e|--end-time} VAL       End time (Unix time in microseconds, ISO8601, or HH:MM[:SS] in the last 24 hours)
# {-r|--human-readable}     Print some fields (e.g. timestamp) in human-readable format, add time offsets
root@vla2-9763-1:/pod_agent$ ./pod_agent print_log public_volume/eventlog -s 18:36:40 -e 18:41:40 -r | grep -v DEBUG | grep simple_http_server

# Успешное выполнение readiness
2019-10-24T18:36:53.086407Z	INFO	THttpAttemptFeedback	{"state":"EHttpGetState_SUCCESS","fail_reason":"","inner_fail_reason":"","start_time":1571931413086067,"death_time":1571931413086377,"object_type":"WORKLOAD","id":"simple_http_server","hook_type":"READINESS"}
2019-10-24T18:37:23.115741Z	INFO	THttpAttemptFeedback	{"state":"EHttpGetState_SUCCESS","fail_reason":"","inner_fail_reason":"","start_time":1571931443115358,"death_time":1571931443115713,"object_type":"WORKLOAD","id":"simple_http_server","hook_type":"READINESS"}
2019-10-24T18:37:53.289725Z	INFO	THttpAttemptFeedback	{"state":"EHttpGetState_SUCCESS","fail_reason":"","inner_fail_reason":"","start_time":1571931473289258,"death_time":1571931473289689,"object_type":"WORKLOAD","id":"simple_http_server","hook_type":"READINESS"}

# workload остановлен
2019-10-24T18:38:10.219309Z	INFO	TObjectStateUpdate	{"ObjectType":"WORKLOAD","OldState":"ACTIVE","NewState":"REMOVED","ObjectIdOrHash":"simple_http_server"}

# обновление дерева workload - новая ревизия
2019-10-24T18:38:13.661437Z	INFO	TTreesUpdateJobUpdateWorkloadTree	{"WorkloadId":"simple_http_server"}

# процесс workload start запустился
2019-10-24T18:38:13.679771Z	INFO	TObjectStateUpdate	{"ObjectType":"WORKLOAD","OldState":"UNKNOWN","NewState":"ACTIVATING","ObjectIdOrHash":"simple_http_server"}

# упал readiness - workload переведен в SEMI_FAILURE
2019-10-24T18:38:18.148485Z	INFO	TObjectStateUpdate	{"ObjectType":"WORKLOAD","OldState":"ACTIVATING","NewState":"SEMI_FAILURE","ObjectIdOrHash":"simple_http_server"}

# результаты выполнения readiness
2019-10-24T18:38:18.148567Z	INFO	THttpAttemptFeedback	{"state":"EHttpGetState_WRONG_ANSWER","fail_reason":"Expected 'Hello my dear @x0leg!' got 'Hello my dear @yanddmi!'","inner_fail_reason":"","start_time":1571931498147399,"death_time":1571931498148392,"object_type":"WORKLOAD","id":"simple_http_server","hook_type":"READINESS"}
2019-10-24T18:38:48.237911Z	INFO	THttpAttemptFeedback	{"state":"EHttpGetState_WRONG_ANSWER","fail_reason":"Expected 'Hello my dear @x0leg!' got 'Hello my dear @yanddmi!'","inner_fail_reason":"","start_time":1571931528237452,"death_time":1571931528237877,"object_type":"WORKLOAD","id":"simple_http_server","hook_type":"READINESS"}
2019-10-24T18:39:18.316001Z	INFO	THttpAttemptFeedback	{"state":"EHttpGetState_WRONG_ANSWER","fail_reason":"Expected 'Hello my dear @x0leg!' got 'Hello my dear @yanddmi!'","inner_fail_reason":"","start_time":1571931558315630,"death_time":1571931558315965,"object_type":"WORKLOAD","id":"simple_http_server","hook_type":"READINESS"}

# workload остановлен
2019-10-24T18:39:41.710674Z	INFO	TObjectStateUpdate	{"ObjectType":"WORKLOAD","OldState":"SEMI_FAILURE","NewState":"REMOVED","ObjectIdOrHash":"simple_http_server"}

# обновление дерева workload - новая ревизия
2019-10-24T18:39:43.671372Z	INFO	TTreesUpdateJobUpdateWorkloadTree	{"WorkloadId":"simple_http_server"}

# процесс workload start запустился
2019-10-24T18:39:43.727581Z	INFO	TObjectStateUpdate	{"ObjectType":"WORKLOAD","OldState":"UNKNOWN","NewState":"ACTIVATING","ObjectIdOrHash":"simple_http_server"}

# readiness успешно завершился - workload переведен в ACTIVE
2019-10-24T18:39:48.039441Z	INFO	TObjectStateUpdate	{"ObjectType":"WORKLOAD","OldState":"ACTIVATING","NewState":"ACTIVE","ObjectIdOrHash":"simple_http_server"}
2019-10-24T18:39:48.039469Z	INFO	THttpAttemptFeedback

# результаты выполнения readiness
2019-10-24T18:39:48.039469Z	INFO	THttpAttemptFeedback	{"state":"EHttpGetState_SUCCESS","fail_reason":"","inner_fail_reason":"","start_time":1571931588038282,"death_time":1571931588039412,"object_type":"WORKLOAD","id":"simple_http_server","hook_type":"READINESS"}
2019-10-24T18:40:18.052669Z	INFO	THttpAttemptFeedback	{"state":"EHttpGetState_SUCCESS","fail_reason":"","inner_fail_reason":"","start_time":1571931618052240,"death_time":1571931618052643,"object_type":"WORKLOAD","id":"simple_http_server","hook_type":"READINESS"}
2019-10-24T18:40:48.238792Z	INFO	THttpAttemptFeedback	{"state":"EHttpGetState_SUCCESS","fail_reason":"","inner_fail_reason":"","start_time":1571931648238406,"death_time":1571931648238766,"object_type":"WORKLOAD","id":"simple_http_server","hook_type":"READINESS"}
2019-10-24T18:41:18.260604Z	INFO	THttpAttemptFeedback	{"state":"EHttpGetState_SUCCESS","fail_reason":"","inner_fail_reason":"","start_time":1571931678260101,"death_time":1571931678260578,"object_type":"WORKLOAD","id":"simple_http_server","hook_type":"READINESS"}
```

Об интерпретации DEBUG логов и трейсов behavior trees читайте на:
[https://a.yandex-team.ru/arc/trunk/arcadia/infra/pod_agent#%D1%87%D1%82%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BB%D0%BE%D0%B3%D0%BE%D0%B2](https://a.yandex-team.ru/arc/trunk/arcadia/infra/pod_agent#%D1%87%D1%82%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BB%D0%BE%D0%B3%D0%BE%D0%B2)

### В контейнере box'а

Также в директорию `<pod_chroot>/pod_agent/public_volume` кладется копия бинарника `pod_agent`.
Директория с логами и бинарником монтируется в каждый `box` в виде `ro` volume `/pod_agent_public`.
Это позволяет читать логи из `box`, не заходя в под:

```bash
$ ssh -6 root@<box_ip>
root@iva1-6443-1:/# /pod_agent_public/pod_agent print_log /pod_agent_public/eventlog -n 10 -r
```

## Гарантии/лимиты на загрузку/верификацию ресурсов

Все операции загрузки/верификации ресурсов производятся в рамках специального meta контейнера.
По умолчанию pod_agent не выставляет квоту (гарантии/лимиты ресурсов) на этот контейнер.
Ее можно редактировать в поле `pod_agent_payload/spec/resources/compute_resources`:

```yaml
  pod_agent_payload:
    spec:
      resources:
        compute_resources:
          vcpu_guarantee: 100
          vcpu_limit: 200
          memory_guarantee: 33554432
          memory_limit: 67108864
          anonymous_memory_limit: 54525952
```

Полное описание - [в proto схеме](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5885026#L700)

{% note info %}

* К вычислительным ресурсам, которые указал пользователь, могут быть добавлены ресурсы, требуемые для запуска [sidecars](sidecars/sidecars.md#table).

* Лимиты по ресурсам можно задать как на весь Deploy Unit, так и на отдельные [Box'ы](https://a.yandex-team.ru/arc_vcs/yp/client/api/proto/pod_agent.proto?rev=c92dec5d0c27ffa14c830bf57eaf5166253be401#L846) и [Workload'ы](https://a.yandex-team.ru/arc_vcs/yp/client/api/proto/pod_agent.proto?rev=c92dec5d0c27ffa14c830bf57eaf5166253be401#L943). Для Workload'ов лимиты можно задать отдельно на каждый стартующий процесс (опциональные [init](https://a.yandex-team.ru/arc_vcs/yp/client/api/proto/pod_agent.proto?rev=c92dec5d0c27ffa14c830bf57eaf5166253be401#L706) скрипты; скрипт запуска основной нагрузки [start](https://a.yandex-team.ru/arc_vcs/yp/client/api/proto/pod_agent.proto?rev=c92dec5d0c27ffa14c830bf57eaf5166253be401#L709)).

* Более подробно про то, какие существуют лимиты по памяти в Porto (Deploy/YP опирается на возможности изоляции ресурсов, предоставляемые Porto), можно почитать [здесь](https://wiki.yandex-team.ru/porto/memory).

* Для мониторинга использования ресурсов (а также выставленных лимитов) можно использовать [unistat ручки](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/docs/ru/containers/metrics-diagnostics.md)

{% endnote %}

### Anonymous memory limit
Следует обратить внимание на отличие **memory_limit** от **anonymous_memory_limit**. Anonymous memory можно грубо описать как вся память, кроме файловых кэшей. Т.е. приложение пользователя не может выделить памяти больше, чем anonymous_memory_limit. Остальная память (`memory_limit - anonymous_memory_limit`) зарезервирована под файловый кэш.

{% note warning %}

* Если выставить `memory_limit == anonymous_memory_limit` либо оставить anonymous_memory_limit пустым, то приложение с утекающей памятью будет способно вытеснить из кэша все файлы. Что может вызвать ряд нежелательных эффектов. Поэтому рекомендуется оставлять зазор между anonymous_memory_limit и memory_limit.
* Для anonymous_memory_limit применимо то же правило, что и для остальных вычислительных ресурсов. Т.е. данный лимит может быть увеличен в случае добавления [sidecars](../pod/sidecars/sidecars.md#table). Например, использование [logbroker](../pod/sidecars/logs/logs.md) добавляет 512Mb к DeployUnit.anonymous_memory_limit.

{% endnote %}

#### Настройки по умолчанию
Если пользователь не выставил anonymous_memory_limit в **Deploy Unit**, то по умолчанию будет зарезервировано **128Mb** под кэш (`DeployUnit.anonymous_memory_limit = DeployUnit.memory_limit - 128Mb`). Для Box/Workload такого резервирования по умолчанию не происходит.
