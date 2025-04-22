# xprod-data-schema

Набор утилит для работы с данными проектов x-products, хранящимися в YT.

# Установка
```
pip install -i https://pypi.yandex-team.ru/simple/ xprod-data-schema
```

# Использование в коде

## Настройка

Настройки хранятся в xprod_schema.config

```
# Задание директории, в которой лежат даннные
>>> from xprod_schema import config
>>> config.yt_root = '//home/x-products/testing/master'

# Задание кластера, на котором лежат данные
>>> from xprod_schema import YtCluster
>>> config.yt_cluster = YtCluster.HAHN
# или
>>> from xprod_schema.helpers.yt import get_cluster_by_name
>>> config.yt_cluster = get_cluster_by_name('hahn')
```

## Пути

В пакете описана структура данных, в частности все пути, схемы и параметры таблиц.
Доступ к эти данным идет через объект типа `PathRouter`. 

Объект `xrpod_schema.pathes.pathes` использует данные из конфигурации. Функция get_pathes позволяет получить отдельный инстанс `PathRouter` с другим базовым путем и кластером.

```
>>> from xrpod_schema.pathes import pathes
# это эквивалентно
>>> from xprod_schema.pathes import get_pathes
>>> pathes = get_pathes(root=None, cluster=None)
```

Информация о таблицах содержится в полях объекта `PathRouter`.

```
>>> pathes.impulses
<Table 'config/impulse/impulses' at YtCluster.HAHN://home/x-products/testing/master>
>>> pathes.impulses.path
//home/x-products/testing/master/config/impulse/impulses
>>> str(pathes.impulses)
'//home/x-products/testing/master/config/impulse/impulses'
>>> pathes.impulses.dynamic
True
>>> pathes.impulses.schema
[{...}]
>>> pathes.impulses.in_memory_mode
<InMemoryMode.COMPRESSED: 'compressed'>
```

Для реплицируемых таблиц заданы параметры описывающие с какого на какие кластеры идет репликация.

```
>>> pathes.impulses.replication
<ReplicationConfig master=YtCluster.MARKOV slaves=set([<YtCluster.HAHN: 'hahn'>, ...])>
>>> pathes.impulses.read_cluster
<YtCluster.HAHN: 'hahn'>
>>> pathes.impulses.write_cluster
<YtCluster.MARKOV: 'markov'>
```

Для нереплицируемых таблиц поле `replication` установлено в `None`

```
>>> pathes.status_db.replication
>>> pathes.status_db.read_cluster
<YtCluster.HAHN: 'hahn'>
>>> pathes.status_db.write_cluster
<YtCluster.HAHN: 'hahn'>
```

Для удобства сделаны вспомогательные функции для работы с таблицами, которые самостоятельно определяют кластер, на который направлять запросы и подставляют правильный путь до таблицы.

```
>>> from xprod_schema.helpers.yt import select_rows, insert_rows
>>> select_rows(pathes.partners)
<yt.wrapper.format.RowsIterator object at 0x7fd643b4b8d0>
>>> select_rows(pathes.partners, "WHERE partner_id='some_name'")
<yt.wrapper.format.RowsIterator object at 0x7fd643b4b990>
>>> insert_rows(pathes.partners, [...])
```

## fallback

Чтобы нормально работать с несколькими кластерами YT в нашем переменчивом мире, сделан впомогательный класс `ClustersMonitor`.

Он умеет с некоторой периодичностью проверять живость кластеров и предлагать сменить текущий кластер на что-то более работающее.

```
>>> from xprod_schema.pathes import get_pathes
>>> from xprod_schema.helpers.yt import YtCluster
>>> from xprod_schema.helpers.fallback import ClustersMonitor
>>> def info(new_cluster):
...     print(new_cluster)
... 
>>> cluster = YtCluster.HAHN
>>> clusters = [YtCluster.SENECA_SAS, YtCluster.SENECA_MYT, YtCluster.SENECA_MAN, YtCluster.HAHN, YtCluster.BANACH]
>>> pathes = get_pathes(root='//home/x-products/testing/master')
>>> monitor = ClustersMonitor(pathes=pathes, default_cluster=cluster, fallback_clusters=clusters, replication_master=YtCluster.MARKOV)
>>> monitor.start(callback=info)
```

Отслеживатель можно инициализировать только частью параметров, тогда остальные будут подобраны автоматически.

Для выбора ближайшего кластера YT можно воспользоваться функцией `get_best_cluster`. Она попытается определить текущий датацентр на основе переменных окружения qloud и выбрать клатер YT из того же ДЦ. Если не удастся, будет выбрана одна из Сенек.

При выборе нового кластера используется следующий подход: перебираем все кластера в указанном порядке и берем первый, где есть доступ к нашей корневой директории и где все реплики таблиц отстают от мастера не более чем на десять минут. Если таких кластеров нет, то выбирается первый, где хотя бы есть корневая директория. Если и таких нет, то возвращается `None`.

Проверка выполняется в отдельном потоке с периодичностью в 30 секунд. Монитор имеет свой собственный пул клиентов к YT.

# Использование для административных операций

Для упрощения работы с таблицами сделана утилита `xprod-schema`. Она позволяет создавать, проверять состояние, удалять таблицы.

Например:
```
$ xprod-schema verify replicas
replica markov://home/x-products/testing/master/config/impulse/partners to seneca-man lag is too large (18 hours)
replica markov://home/x-products/testing/master/config/impulse/partners to seneca-sas is empty, replication completely broken
replica markov://home/x-products/testing/master/config/impulse/impulses to seneca-man is empty, replication completely broken
replica markov://home/x-products/testing/master/config/impulse/impulses to seneca-sas is empty, replication completely broken
replica markov://home/x-products/testing/master/config/impulse/impulses_cfgs to seneca-man is empty, replication completely broken
replica markov://home/x-products/testing/master/config/impulse/impulses_cfgs to seneca-sas is empty, replication completely broken
replica markov://home/x-products/testing/master/config/impulse/impulses_status_log to seneca-man is empty, replication completely broken
replica markov://home/x-products/testing/master/config/impulse/impulses_status_log to seneca-sas is empty, replication completely broken
replica markov://home/x-products/testing/master/metrics-db to seneca-man is empty, replication completely broken
replica markov://home/x-products/testing/master/metrics-db to seneca-sas is empty, replication completely broken
```

Всеми командами поддерживаются опции `--verbose` и `--pretend` (и их короткие аналоги `-v` и `-p` соответственно). При указании опции `--pretend` гарантируется, что все действия будут только read-only. Задание опции `--verbose` повышает количество выводимой информации. Чем больше указано опций `--verbose`, тем больше будет вывода.

```
$ xprod-schema -pvvv init tables
check hahn://home/x-products/testing/master/config/impulse/partners is exist
hahn://home/x-products/testing/master/config/impulse/partners already exist
check hahn://home/x-products/testing/master/status-db is exist
hahn://home/x-products/testing/master/status-db already exist
...
```

`xprod-schema init tables` создает и монтирует таблицы на заданном кластере.
`xprod-schema init replicas` создает все необходимые таблицы на всех кластерах и запускает репликацию.
Повторное использование этих команд в любом порядке не ломает состояние схемы.

`xprod-schema drop tables` удаляет таблицы на заданном кластере.
`xprod-schema drop replicas` останавливает репликацию и удаляет реплицируетмые таблицы на всех кластерах.

`xprod-schema verify tables` проверяет соответствие описанного в пакета состояния схемы и фактического состояния на заданном кластере.
`xprod-schema verify replicas` проверяет функционирование репликации и соответствие её описанной схеме.

`xprod-schema repair tables` пытается привести фактическое состояние таблиц к описанному.
`xprod-schema repair replicas` пытается привести фактическое состояние репликации к описанному.
Использование этих команд не должно приводить к потере данных.

`xprod-schema copy dyntables` копирует содержимое динамических таблиц из одного места в другое, реплицируемые таблицы игнорируются.
`xprod-schema copy replicas` копирует содержимое реплицируемых таблиц из одного места в другое.
Эти команды предполагают, что все необходимые таблицы созданы и всё функционирует нормально.
