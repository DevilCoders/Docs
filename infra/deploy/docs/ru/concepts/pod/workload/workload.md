# Workload

**Workload** — это приложение, бинарь, микросервис, скрипт; по сути — пользовательский процесс-демон. В Workload указываются параметры запуска, проверки готовности и живости процесса, логи, unistat url для сбора метрик, сбор корок и локальные переменные окружения. Workload'ы группируются внутри [Box](../box.md). Подробнее об иерархии сущностей в Y.Deploy можно почитать [тут](../../../concepts/entity-hierarchy.md).

Workload обозначается значком ![workload-icon](../../../_assets/icons/workload.png).

В Y.Deploy слой представлен следующей [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5791549#L434-473):

## Граф состояний {#graph}

![workload](../../../_assets/concepts/workload.png)
![legend](../../../_assets/legend.png)

## Start процесс {#start}

`Start` процесс это пользовательский процесс, запускаемый с помощью [porto](https://wiki.yandex-team.ru/porto/) контейнеров.

Из-за этого есть несколько особенностей:

1. Мы постоянно пытаемся перезапустить `start` процесс, если он завершился (независимо от кода возврата)
2. При смерти основного процесса все процессы в контейнере убиваются.
Иными словами, не получится использовать `self daemonize` процессы, которые делают `double fork` и умирают, ибо их дети будут убиты.
В качестве примера, для запуска `nginx` будет недостаточно сделать `service nginx start` или `/usr/sbin/nginx -q -c /conf/nginx/nginx.conf -p /conf/nginx`, надо сделать `/usr/sbin/nginx -q -c /conf/nginx/nginx.conf -p /conf/nginx -g "daemon off;"`

Если вы считаете, что вам нужен `self daemonize` и подобное, напишите об этом в тикет [https://st.yandex-team.ru/DEPLOY-3267](https://st.yandex-team.ru/DEPLOY-3267)

{% note warning %}

Start процесс автоматически (не чаще раза в 10 секунд) перезапускается pod agent'ом и, несмотря на то, что он тоже описан как TContainer, [политика рестартов](../../../concepts/pod/workload/probes.md#ttimelimit) для него не применяется.

{% endnote %}

Если вам нужно в `start command` выполнить несколько команд, то вы можете это сделать несколькими способами:

1. Последовательность команд записать в виде скрипта (предположим, он называется `start.sh`). Этот скрипт приносить в контейнер ресурсом и в `start command` запускать его `/usr/local/gamechanger/prod/start.sh`

    ```yaml
        start: 
            command_line: "/usr/local/gamechanger/prod/start.sh"
    ```

2. Указать команды непосредственно в спецификации workload, начав команду с `bash -c`

    ```yaml
        start: 
          command_line: "bash -c 'while :\ndo\n\nnumber=$((1 + RANDOM % 4))\n\necho Random number is $number\n\nsleep $number\n\ndone'"
    ```

## Сохранение корок (coredumps)

Необходимо добавить в start контейнер workload core_command и добавить ulimit_soft в workload.

При желании core_command можно добавить любому контейнеру (init, readiness, liveness, ...), не только start.

```yaml
workloads:
- id: simple_http_server
  ...
  start:
    command_line: /simple_http_server 80 'Hello my dear devops!'
    core_command: cp --sparse=always /dev/stdin /coredumps/${CORE_EXE_NAME}-${CORE_PID}-S${CORE_SIG}.core
  ulimit_soft:
  - name: core
    value: 10737418240
```

Данный пример будет сохранять корки в `/coredumps` в box.

Так же  можно настроить аггрегатор корок [https://deploy.yandex-team.ru/docs/concepts/pod/sidecars/coredump](https://deploy.yandex-team.ru/docs/concepts/pod/sidecars/coredump)

{% note warning %}

у процессов которые используют SUID дамп не работает

{% endnote %}


## Запись секрета в переменную окружения {#secretenv}

Аналогично [инструкции для box](../box.md#secretenv).

## Системные переменные окружения {#system_env}

Наследуются все [системные переменные box](../box.md#systemenv).

К ним добавляются:

```bash
ПЕРЕМЕННАЯ                     = Пример реального значения # Описание
DEPLOY_WORKLOAD_ID             = workload_id
DEPLOY_CONTAINER_ID            = pod_agent_box_BoxId/workload_WorkloadId_start # Id porto контейнера относительно пода
```

В случае если для ворклода включена поставка логов, добавляются переменные:

```bash
DEPLOY_LOGS_SECRET             = STATIC_SECRET # Секрет для установления сессии с unified agent
DEPLOY_LOGS_DEFAULT_NAME       = chegoryu-test-stage # Дефолтный логнейм для установления сессии с unified agent
DEPLOY_LOGS_ENDPOINT           = localhost:2222 # Точка подключения к unified agent
```

##  Как прочесть env работающего процесса workload? {#cat-environ}

С помощью команды:

```bash
cat /proc/<pid>/environ | tr "\0" "\n"`
```

## Особенности прото схемы workload {#proto-scheme}
Прото схема для workload состоит из двух частей. Первая часть - это [message TWorkload](https://arcanum.yandex-team.ru/svn/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9490796#L781). Изменение любого поля из TWorkload без смены id приведет к пересборке workload с данным id. Вторая часть - это [message TMutableWorkload](https://arcanum.yandex-team.ru/svn/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9490796#L823). Данный message предназначен для аттрибутов ворклоуда, изменение которых не приведет к пересборке.

{% note warning %}

Спецификация подового агента должна обязательно содержать список [mutable_workloads](https://arcanum.yandex-team.ru/svn/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9490796#L43), каждый элемент которого будет соотвествовать элементу из списка [workloads](https://arcanum.yandex-team.ru/svn/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9490796#L37). Элементы из mutable_workloads должны быть уникальны по значению workload_ref поля.

{% endnote %}

## Детали реализации {#details}

Важно, что нет возможности выставить лимиты, гарантии на Workload в целом, а только на контейнер, принадлежащий этой абстракции. Для того, чтобы детально понять, на какие сущности создаются контейнеры, лучше всего воспользоваться первоисточником  [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5791549#L434-473). Контейнеры создаются только на сущности, обладающие свойством [TComputeResources](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5791549#L108).


