# Стандартный механизм отгрузки логов

## Принцип работы механизма {#auto-stdout-stderr}

Для стартового контейнера в workload стандартные потоки вывода stdout и stderr записываются в [автоматически ротирующиеся файлы](write.md#stdout_stderr_files) внутри pod'ов. Данные из файлов при помощи pod agent перенаправляются в `logbroker_tools_box` по [gRPC интерфейсу](https://docs.yandex-team.ru/unified_agent/configuration/#grpc_input).

Отгрузкой логов занимается инфраструктурный [sidecar-бокс](../concepts/pod/sidecars/sidecars.md) `logbroker_tools_box`, в котором запущен [Unified Agent](https://docs.yandex-team.ru/unified_agent/). Unified Agent организует обогащение записей метаданными и записывает их в [топик LogBroker](topic.md#topic).
Из топика Logbroker записи попадают и [хранятся](topic.md) в таблицы YT и YDB.

## Включение стандартного механизма {#activation}

Для активации стандартного механизма отгрузки логов, записываемых приложением в [STDERR/STDOUT](write.md#stdout_stderr):

{% list tabs %}

- UI

  Выставить переключатель `Logs` в `Enabled` в настройках выбранного workload'а в UI;

  ![https://jing.yandex-team.ru/files/slamur/Screenshot%20from%202021-11-08%2023-21-29.png](https://jing.yandex-team.ru/files/slamur/Screenshot%20from%202021-11-08%2023-21-29.png)

- Yaml-спецификация

  Указать `transmit_logs: true` через [dctl](../reference/tools/dctl.md) в спецификации workload'a ([proto-спецификация](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r8782046#L777)):

  Пример спецификации:

  ```yaml
  spec:
    deploy_units:
      deploy_unit:
        multi_cluster_replica_set:
          replica_set:
            pod_template_spec:
              spec:
                pod_agent_payload:
                  spec:
                    workloads:
                      - id: 'workload'
                        transmit_logs: true
  ```

{% endlist %}

{% note warning %}

В случае, если отгрузка логов производится исключительно через библиотеки, требуется указать в спеке Deploy Unit [специальный флаг](../concepts/pod/sidecars/logs/logs.md#mandatory-logbroker-box).

{% endnote %}


### Парсинг и форматирование логов {#format}

* Значения полей, совпадающих по наименованию с полями таблиц YT/YDB, выделенных под данные пользователя, перекладываются в соответствующие поля таблиц;
* Все несматченные поля попадают в поле `context`, по значениям которого возможен [поиск через пользовательский интерфейс](gui.md#query).

Подробнее c этим можно ознакомиться в разделе [{#T}](format.md)


## Ресурсы {#resources}

Для функционирования сайдкара `logbroker_tools_box` на каждый под будут [запрошены ресурсы](../concepts/pod/resource-requests.md) из вашей [квоты](../reference/quotas-and-limits.md). 

Доступна возможность настройки величины запроса, подробнее смотрите [{#T}](../concepts/pod/sidecars/logs/logs.md#custom-resources).

## Ограничение потока данных {#limits}

Ограничение потока данных действует на Deploy Unit и задаётся двумя величинами:

- суммарный объём данных в секунду;
- количество сообщений в секунду.

{% note info %}

Ограничения применяются к **оригинальному объёму** передаваемых данных.

Сжатие данных, производимое Unified Agent, применяется уже после отсечения данных по ограничениям.

{% endnote %}

### Абсолютное ограничение {#limits-common}

При использовании стандартного механизма отгрузки логов (независимо, автоматическая отгрузка или через библиотеки), существует **абсолютное ограничение**:

- 1 терабайт в секунду;
- 100500 сообщений в секунду.

### Ограничения для коммунального топика {#limits-common-topic}

Так как коммунальный топик сохраняет данные всех пользователей в одну таблицу, то для него действуют усиленные ограничения:

- при использовании [Runtime version 7](../reference/patchers-revision.md#runtime-version-7) или выше:

- 15 мегабайт в секунду
- 20000 сообщений в секунду

## Ограничение срока хранения данных в YDB {#limits-ydb}

Срок хранения данных в YDB составляет `2 суток`, после чего таблицы с данными удаляются.
