# Мониторинг состояния кластера и хостов

{% include [monitoring-introduction](../../_includes/mdb/monitoring-introduction.md) %}

Новые данные для графиков поступают каждые {{ graph-update }}.

{% include [note-info-monitoring-auto-units](../../_includes/mdb/note-monitoring-auto-units.md) %}

{% include [alerts](../../_includes/mdb/alerts.md) %}

## Мониторинг состояния кластера {#monitoring-cluster}

Для просмотра детальной информации о состоянии кластера {{ mms-name }}:

1. Перейдите на страницу каталога и выберите сервис **{{ mms-name }}**.

1. Нажмите на имя нужного кластера и выберите вкладку **Мониторинг**.

1. {% include [open-in-yandex-monitoring](../../_includes/mdb/open-in-yandex-monitoring.md) %}

На странице появятся следующие графики:

* **Active Transactions [count]** — количество активных транзакций, для каждого хоста.

* **Batch Requests/sec** — количество пакетных операций, выполненных на каждом хосте за 1 секунду. Подробнее о пакетных операциях см. в [документации {{ MS }}]({{ ms.docs }}/sql/odbc/reference/develop-app/batches-of-sql-statements).

* **CPU** — загрузка процессорных ядер. При повышении нагрузки значение `percent_idle_time` уменьшается.

* **Disk capacity on primary, [bytes]** — использование дискового пространства на [первичной реплике](../concepts/replication.md) (в байтах).

* **Is alive [bool]** — доступность кластера в виде суммы состояний его хостов. Каждый хост в состоянии **Alive** увеличивает общую доступность на 1.

* **Is Primary [bool]** — какой хост является первичной репликой и как долго.

* **Lazy Writes/sec on primary** — скорость физической записи на первичной реплике. {{ MS }} разделяет запись данных для повышения эффективности работы с хранилищем:

    * _Логическая запись_ — изменение данных в RAM.
    * _Физическая запись_ — запись измененных страниц из RAM в хранилище.

    Подробнее см. в [документации {{ MS }}]({{ ms.docs }}/sql/relational-databases/writing-pages).

* **Memory Grants Pending on primary** — количество запросов, ожидающих выделения RAM. Подробнее см. в [документации {{ MS }}]({{ ms.docs }}/sql/relational-databases/memory-management-architecture-guide).

* **Page Life Expectancy [sec]** — время жизни страниц памяти (в секундах) до записи в хранилище. Чем оно больше, тем эффективнее используется буфер, и тем реже кластеру приходится обращаться к хранилищу для выборки нужных данных.

* **Transactions/sec on primary** — среднее количество транзакций, выполненных на первичной реплике за одну секунду.

* **User connections** — количество подключений к кластеру. Несколько подключений всегда будут активны. Они используются самим кластером и службами мониторинга {{ yandex-cloud }}.


## Мониторинг состояния хостов {#monitoring-hosts}

Для просмотра детальной информации о состоянии отдельных хостов {{ mms-name }}:

1. Перейдите на страницу каталога и выберите сервис **{{ mms-name }}**.
1. Нажмите на имя нужного кластера и выберите вкладку **Хосты** → **Мониторинги**.
1. Выберите нужный хост из выпадающего списка.

На этой странице выводятся графики:

* **Active Transactions** — количество активных транзакций для каждой базы данных.

* **Bytes send/received** — скорость обмена данными по сети (байт/с).

* **CPU (processor time)** — загрузка процессорных ядер.

* **Disk Latency** — время ожидания дисковых операций:

    * **avg.\_disk_sec/transfer** — среднее время дисковых операций;
    * **avg.\_disk_sec/write** — среднее время записи;
    * **avg.\_disk_sec/read** — среднее время чтения.

* **Disk bytes** — скорость дисковых операций (байт/с).

* **Disk read/write time** — загрузка диска (в процентах).

* **Memory Grants Pending** — количество запросов, ожидающих выделения RAM.

* **Packets send/received** — количество обработанных сетевых пакетов:

    * **packets_received_discarded** — количество отброшенных пакетов.

        Пакеты отбрасываются по следующим причинам:

        * ошибки при передаче;
        * ошибки форматирования;
        * недостаток места в хранилище.

        Хотя отбрасывание некоторых пакетов неизбежно, растущее значение этой характеристики может указывать на проблемы в работе кластера.

    * **packets_outbound_errors** — количество ошибок при отправке пакетов.
    * **packets_received_errors** — количество ошибок при получении пакетов.
    * **packets_received_persec** — интенсивность приема данных из сети (пакетов/с).
    * **packets_sent_persec** — интенсивность отправки данных в сеть (пакетов/с).

* **Page Life Expectancy** — время жизни страниц памяти до сброса в хранилище (в секундах). Чем больше значение этой характеристики, тем эффективнее используется буфер, и тем реже кластеру приходится обращаться к хранилищу для чтения или записи нужных данных.

* **SQL Errors [count]** — количество ошибок при обработке SQL-запросов:

    * **User_Errors** — ошибки пользователей;
    * **Kill_Connection_Errors** — серьезные ошибки, которые привели к закрытию соединения;
    * **Info_Errors** — количество информационных событий, связанных с ошибками;
    * **DB_Offline_Errors** — ошибки, связанные с недоступностью баз данных;
    * **Total** — общее количество ошибок на хосте.

* **Space used/available** — использование дискового пространства (в байтах).

    * **avg._disk_sec/transfer** — среднее время операций ввода-вывода.
    * **avg._disk_sec/write** — среднее время записи.
    * **avg._disk_sec/read** — среднее время чтения.

* **User connections** — количество подключений к хосту. Несколько подключений всегда будут активны. Они используются самим кластером и службами мониторинга {{ yandex-cloud }}.

## Настройка алертов в {{ monitoring-full-name }} {#monitoring-integration}

{% list tabs %}

- Консоль управления

    1. В консоли управления выберите каталог с кластером, для которого нужно настроить алерты.
    1. В списке сервисов выберите ![image](../../_assets/monitoring.svg) **{{ monitoring-short-name }}**.
    1. В блоке **Сервисные дашборды** выберите:
        * **{{ mms-name }} — Cluster Overview** для настройки алертов кластера;
        * **{{ mms-name }} — Host Overview** для настройки алертов хостов.
    1. На нужном графике нажмите на значок ![options](../../_assets/horizontal-ellipsis.svg) и выберите пункт **Создать алерт**.
    1. Если на графике несколько показателей, выберите запрос данных для формирования метрики и нажмите **Продолжить**. {% if audience == "external" %}Подробнее о языке запросов см. [документацию {{ monitoring-full-name }}](../../monitoring/concepts/querying.md). {% endif %}
    1. Задайте значения порогов `Alarm` и `Warning` для срабатывания алерта.
    1. Нажмите кнопку **Создать алерт**.

{% endlist %}

{% include [other-indicators](../../_includes/mdb/other-indicators.md) %}

Рекомендуемые значения порогов для некоторых метрик:

| Метрика                                      | Обозначение                                      | `Alarm`                    | `Warning`                  |
|---------------------------------------------:|:------------------------------------------------:|:--------------------------:|:--------------------------:|
| Объем использованного хранилища              | `mdb_volume_space.available_space_bytes`         | `10% от размера хранилища` | `20% от размера хранилища` |
| Утилизация CPU                               | `win_cpu.percent_idle_time`                      | `10`                       | `20`                       |
| Количество запросов, ожидающих выделения RAM | `mdb_performance_counters.memory_grants_pending` | `2`                        | `1`                        |

Текущий размер хранилища можно посмотреть в [детальной информации о кластере](cluster-list.md#get-cluster).

## Состояние и статус кластера {#cluster-health-and-status}

{% include [health-and-status](../../_includes/mdb/monitoring-cluster-health-and-status.md) %}

Для просмотра состояния и статуса кластера:

1. Перейдите на страницу каталога и выберите **{{ mms-name }}**.
1. Наведите курсор на индикатор в столбце **Доступность** в строке нужного кластера.

### Состояния кластера {#cluster-health}

{% include [monitoring-cluster-health](../../_includes/mdb/monitoring-cluster-health.md) %}

### Статусы кластера {#cluster-status}

{% include [monitoring-cluster-status](../../_includes/mdb/monitoring-cluster-status.md) %}
