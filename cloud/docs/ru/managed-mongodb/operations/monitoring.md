# Мониторинг состояния кластера и хостов

{% include [monitoring-introduction](../../_includes/mdb/monitoring-introduction.md) %}

{% include [monitoring-period](../../_includes/mdb/monitoring-freq.md) %}

{% include [note-monitoring-auto-units](../../_includes/mdb/note-monitoring-auto-units.md) %}

{% include [alerts](../../_includes/mdb/alerts.md) %}

## Мониторинг состояния кластера {#cluster}

Для просмотра детальной информации о состоянии кластера {{ mmg-name }}:

1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ mmg-name }}**.
1. Нажмите на имя нужного кластера и выберите вкладку **Мониторинг**.

1. {% include [open-in-yandex-monitoring](../../_includes/mdb/open-in-yandex-monitoring.md) %}

На странице появятся следующие графики:

* **Asserts total** — количество срабатываний [assert](https://docs.mongodb.com/manual/reference/command/serverStatus/#mongodb-serverstatus-serverstatus.asserts) в кластере.
* **Average operation time per host** — среднее время выполнения команд каждым хостом (в микросекундах).
* **Average operations time on primary** — среднее время выполнения команд на первичных репликах (в микросекундах).
* **Average operations time on secondaries** — среднее время выполнения команд на вторичных репликах (в микросекундах).
* **CPU usage per host** — степень использования vCPU на каждом хосте (в тысячных долях).
* **CPU usage per host, top 5 hosts** — 5 хостов с наибольшей утилизацией vCPU (в процентах).
* **Configured oplog size per host** — размер журнала операций (oplog) на каждом хосте кластера (в гигабайтах).
* **Connections per host** — среднее количество подключений к каждому хосту.
* **Data size on primary, top 5 databases** — размер пяти наибольших баз данных на первичной реплике (в байтах).
* **Disk read per host, top 5 hosts** — 5 хостов с наибольшей нагрузкой на чтение из дисковой подсистемы (байт/с).
* **Disk space usage per host, top 5 hosts** — 5 хостов с наибольшим использованием места в хранилище (выводится два графика: в байтах и в процентах).
* **Disk usage per host, top 5 hosts** — 5 хостов с наибольшей нагрузкой на подсистему I/O хранилища (байт/с).
* **Disk write per host, top 5 hosts** — 5 хостов с наибольшей нагрузкой на запись в дисковую подсистему (килобайт/с).
* **Documents affected on primary** — среднее количество затронутых запросами документов на первичной реплике.
* **Documents affected on secondaries** — среднее количество затронутых запросами документов на всех вторичных репликах.
* **Documents affected per host** — среднее количество документов, затронутое запросами на каждом хосте.
* **Hosts available for read** — количество хостов, принимающих запросы на чтение.
* **Hosts available for write** — количество хостов, принимающих запросы на запись.
* **Index size on primary, top 5 indexes** — размер пяти наибольших индексов на первичной реплике (в байтах).
* **Memory usage per host** — объем оперативной памяти, использованной каждым хостом (в байтах).
* **Memory usage per host, top 5 hosts** — 5 хостов с наибольшим использованием оперативной памяти (в процентах).
* **Network data received per host, top 5 hosts** — 5 хостов с наибольшей сетевой нагрузкой на чтение (килобайт/с).
* **Network data sent per host, top 5 hosts** — 5 хостов с наибольшей сетевой нагрузкой на запись (килобайт/с).
* **Network usage per host, top 5 hosts** — 5 хостов с наибольшей суммарной сетевой нагрузкой (килобайт/с).
* **Open cursors total** — количество открытых в кластере курсоров.
* **Oplog window** — временной диапазон, за который хранятся данные репликации в коллекции oplog каждого хоста.
* **Page faults per host** — количество [отказов страниц]({% if lang=="ru" %}https://ru.wikipedia.org/wiki/Отказ_страницы{% endif %}{% if lang =="en" %}https://en.wikipedia.org/wiki/Page_fault{% endif %}) на каждом хосте.
* **Queries on secondaries** — среднее количество запросов каждого типа, выполненных на вторичных репликах.
* **Queries on primary** — среднее количество выполненных на первичных репликах запросов каждого типа.
* **Read operations count, top 5 collections** — 5 коллекций с наибольшим количеством времени, затраченным на выполнение операций чтения.
* **Readers/writers active queue per host, top 5** — суммарный размер пяти наибольших очередей для каждого хоста:
    * с запросами на чтение;
    * с запросами на запись.
* **Replicated queries** — среднее количество реплицированных запросов в кластере.
* **Replication lag per host and write_concern wait** — задержки репликации на каждом хосте и ожидание [подтверждения записи](https://docs.mongodb.com/manual/reference/write-concern/) (в секундах).
* **Scan and order per host** — количество сортировок данных без использования индекса на каждом хосте.
* **Scanned / returned** — показывает соотношения:
    * `scanned_docs / returned_docs` — количество просканированных документов к количеству возвращенных;
    * `scanned_keys / returned_docs` — количество просканированных ключей индекса к количеству возвращенных документов.
* **TTL indexes activity** — использование индексов при обработке документов с истекшим сроком жизни (Time to Life, TTL).
* **TTL indexes total** — общее количество [индексов TTL](https://docs.mongodb.com/manual/core/index-ttl/).
* **Total operations count on cluster** — общее количество выполненных в кластере операций.
* **Total operations time on cluster** — общее время выполнения операций в кластере (в миллисекундах).
* **WiredTiger cache pages evicted on primary** — среднее количество страниц оперативной памяти, вытесненных на первичной реплике.
* **WiredTiger cache state on primary** — использование кеша WiredTiger на первичной реплике (в байтах).
* **WiredTiger checkpoint time on primary** — время создания контрольных точек WiredTiger на первичной реплике (в миллисекундах).
* **WiredTiger concurrent transactions on primary** — среднее количество параллельных транзакций на первичной реплике.
* **WiredTiger transactions state on primary** — среднее количество транзакций каждого уровня на первичной реплике.
* **Write conflicts per host** — количество конфликтов записи на каждом хосте.
* **Write operations count, top 5 collections** — 5 коллекций с наибольшим количеством времени, затраченным на выполнение операций записи.

## Мониторинг состояния хостов {#hosts}

Для просмотра детальной информации о состоянии отдельных хостов {{ mmg-name }}:

1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ mmg-name }}**.
1. Нажмите на имя нужного кластера и выберите вкладку **Хосты** → **Мониторинги**.
1. Выберите нужный хост из выпадающего списка. Возле имени хоста будет показана его роль (`PRIMARY` или `SECONDARY`) и тип (`MONGOCFG`, `MONGOD`, `MONGOINFRA`, `MONGOS`).

На этой странице выводятся графики, показывающие нагрузку на отдельный хост кластера:

* **CPU** — загрузка процессорных ядер. При повышении нагрузки значение **Idle** уменьшается.
* **Memory** — использование оперативной памяти (в байтах). При высоких нагрузках значение параметра **Free** уменьшается, остальные — растут.
* **Disk Bytes** — скорость дисковых операций (байт/с).
* **Disk IOPS** — интенсивность дисковых операций (операций/с).
* **Network Bytes** — скорость обмена данными по сети (байт/с).
* **Network Packets** — интенсивность обмена данными по сети (пакетов/с).

## Настройка алертов в {{ monitoring-full-name }} {#monitoring-integration}

{% list tabs %}

- Консоль управления

    1. В [консоли управления]({{ link-console-main }}) выберите каталог с кластером, для которого нужно настроить алерты.

    1. В списке сервисов выберите ![image](../../_assets/monitoring.svg) **{{ monitoring-short-name }}**.

    1. В блоке **Сервисные дашборды** выберите:

        * **{{ mes-name }}** для настройки алертов кластера;
        * **{{ mes-name }} — Host Overview** для настройки алертов хостов.

    1. На нужном графике нажмите на значок ![options](../../_assets/horizontal-ellipsis.svg) и выберите пункт **Создать алерт**.

    1. Если на графике несколько показателей, выберите запрос данных для формирования метрики и нажмите **Продолжить**. {% if audience == "external" %}Подробнее о языке запросов см. [документацию {{ monitoring-full-name }}](../../monitoring/concepts/querying.md). {% endif %}

    1. Задайте значения порогов `Alarm` и `Warning` для срабатывания алерта.

    1. Нажмите кнопку **Создать алерт**.

{% endlist %}

{% include [other-indicators](../../_includes/mdb/other-indicators.md) %}

Рекомендуемые значения порогов для некоторых метрик:

| Метрика                         | Обозначение                     | `Alarm`                  | `Warning`                |
|---------------------------------|:-------------------------------:|:------------------------:|:------------------------:|
| Доступность БД на запись        | `can_write`                     | `Равно 0`                | —                        |
| Задержка репликации             | `replset_status-replicationLag` | `180`                    | `30`                     |
| Объем использованного хранилища | `disk.used_bytes`               | 90% от размера хранилища | 70% от размера хранилища |

Текущий размер хранилища можно посмотреть в [детальной информации о кластере](cluster-list.md#get-cluster).

{% if audience != "internal" %}
Полный список поддерживаемых метрик см. в [документации {{ monitoring-name }}](../../monitoring/metrics-ref/index.md#managed-mongodb).
{% endif %}

### Отслеживание перехода в read-only {#read-only-alert}

Чтобы отслеживать степень заполнения хранилища на хостах кластера и получать уведомления в случае скорого исчерпания свободного места:

{% if audience == "external" %}
1. [Создайте алерт](../../monitoring/operations/alert/create-alert.md).
{% else %}
1. Создайте алерт.
{% endif %}
1. Добавьте метрику состояния `disk.free_bytes`.

    Для этого создайте запрос в конструкторе запросов:

    `service={{ mmg-name }}` → `name=disk.free_bytes` → `host=*` → `resource_id=*` → `resource_type=cluster`.

1. Задайте в параметрах алерта значения порогов для оповещения:
   * **Условие срабатывания** — выберите условие `Меньше или равно` для размера свободного дискового пространства, при котором сработает алерт.

       Рекомендуемые значения порогов в зависимости от объема хранилища:
  
       | Объем хранилища, ГБ | `Alarm`     | `Warning`        |
       |---------------------|-------------|------------------|
       | ⩽ 600               | `1G` (1 ГБ) | `1500M` (1,5 ГБ) |
       | > 600               | `6G` (6 ГБ) | `10G` (10 ГБ)    |

   * **Дополнительные настройки** → **Функция агрегации** — выберите значение `Минимум` (минимальное значение метрики за период).

## Состояние и статус кластера {#cluster-health-and-status}

{% include [health-and-status](../../_includes/mdb/monitoring-cluster-health-and-status.md) %}

Для просмотра состояния и статуса кластера:

1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ mmg-name }}**.
1. Наведите курсор на индикатор в столбце **Доступность** в строке нужного кластера.

### Состояния кластера {#cluster-health}

{% include [monitoring-cluster-health](../../_includes/mdb/monitoring-cluster-health.md) %}

### Статусы кластера {#cluster-status}

{% include [monitoring-cluster-status](../../_includes/mdb/monitoring-cluster-status.md) %}
