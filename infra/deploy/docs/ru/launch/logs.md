# Быстрая настройка логирования приложения

## Введение {#intro}

Y.Deploy позволяет работать с логами сервисов и пользовательских приложений "из коробки" — без дополнительных настроек и кода. [Включите](#activation) стандартный механизм отгрузки логов в UI или в yaml-спецификации.

[Стандартный механизм](../logs/standard-mechanism.md) получает логи из потоков вывода STDERR/STDOUT стартового контейнера, обогащает записи [метаданными](../logs/format.md) (container_id, deploy_unit, pod, и т.д.) и записывает их в [топик LogBroker](#storage), откуда записи попадают в:
* таблицы YT (долгосрочное хранилище для аналитики — 180 дней).
* YDB (для real-time отладки, срок хранения данных составляет `2 суток`, после чего таблицы с данными удаляются). Записи из YDB доступны в графическом интерфейсе Y.Deploy для стейджа на вкладке **Logs**.

{% note info %}

Если вас не устраивает весь [стандартный механизм](../logs/standard-mechanism.md) отгрузки логов, вы можете [вручную развернуть](../logs/index.md#manual-unified-agent) Unified Agent.

{% endnote %}

Логи могут быть в виде обычного plain-text или структурированы в формате JSON. Подробнее c этим можно ознакомиться в разделе [Формат логов](../logs/format.md).

Для настройки удобной фильтрации логов пользовательского приложения (по source, level и т.д.) вы можете использовать [клиентские библиотеки](../logs/write.md#libs), заполняя необходимые поля. Например, чтобы чтобы структурировать stdout/stderr и утилизировать колонку level, вы можете использовать поля `levelStr` или `level`. Вот тут подробное [описание формата](../logs/format.md#schema).

### Хранение логов {#storage}

По умолчанию все логи отгружаются [LogBroker](https://logbroker.yandex-team.ru/docs) в коммунальный топик `deploy/logs` — общее хранилище для всех пользователей. Логи различных стейджей отгружаются в него без какой-либо группировки.

{% note warning %}

Логи сливаются в YT в одну таблицу и доступны всем сотрудникам Яндекса.
[Не пишите в логи персональные данные](https://wiki.yandex-team.ru/security/awareness/skarif/policy/).

{% endnote %}

Вы можете настроить отправку в [самостоятельно настроенный топик](../logs/topic.md#custom-topic) или вообще полностью [кастомизировать UnifiedAgent](https://wiki.yandex-team.ru/users/alexbogo/ua-in-deploy-instuction/). Возможно использование топика, отличного от коммунального — для каждого деплой-юнита выбор топика осуществляется независимо.

Стандартный механизм [автоматически ротирует](../logs/write.md#rotation) лог файлы, подробнее смотрите раздел [{#T}](../logs/write.md).


## Включение стандартного механизма логирования {#activation}

Для включения стандартного механизма отгрузки логов:

{% list tabs %}

- UI Y.Deploy

  1. Перейти в настройки выбранного workload.
  2. Выставить переключатель **Logs** в **Enabled**.

      ![Скриншот с переключателем](https://jing.yandex-team.ru/files/slamur/Screenshot%20from%202021-11-08%2023-21-29.png)

- Yaml-спецификация

  Укажите `transmit_logs: true` через [dctl](../reference/tools/dctl.md) в спецификации workload'a:

  Пример:

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


### Работа с логами {#gui}

В графическом интерфейсе Y.Deploy логи стейджа доступны на вкладке **Logs** . Вы можете [работать с логами в GUI](../logs/gui.md): просматривать, фильтровать записи и формировать простые запросы.

Подробнее о доступе к данным в YT и YDB, смотрите раздел [{#T}](../logs/topic.md).


{% note info %}

Возможно чтение stdout/stderr логов пользовательских контейнеров с помощью dctl или portoctl: [{#T}](../concepts/pod/pod.md#readingstdoutstderr).

{% endnote %}

![https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-00-42.png](https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-00-42.png)

{% note warning %}

На данной вкладке отображаются только логи из [коммунального топика](../logs/topic.md#communal-topic).

{% endnote %}


#### См. также:

* [{#T}](../logs/system-logs.md)
