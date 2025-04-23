# metrics-per-process

Небольшая либка для определения суммарного memory, cpu, threads, i/o, connections, etc… нескольких процессов на основе psutil, код взят из https://github.com/sensu-plugins/sensu-plugins-process-checks/blob/master/bin/metrics-per-process.py и немного пропатчен для расширения функциональности

## Получение списка процессов

### По условиям: имя, user, переменные среды (новая функциональность)

```python
>>> import metrics_per_process as mp
>>> mp.find_pids(process_names=[‘foo’, ‘bar’], users=[‘max’, ‘sam’], process_env={'TAG_ENV_VAR': 'whatever', 'VAR_THAT_SHOULD_NOT_BE': None})
[5546, 3455, 5423, 6543, 5433]
```
* Если process_names/users/env не указано, берутся любые names/users/env
* Ходит в /proc

### По имени (изначальная функциональность)
```python
>>> import metrics_per_process as mp
>>> mp.find_pids_from_name('foo')
[5546, 3455, 5423, 6543, 5433]
```
* Ходит в /proc


## Получение статистики по процессам

### Статистика по pid, один процесс (изначальная функциональность)
```python
>>> import metrics_per_process as mp
>>> mp.stats_per_pid(pid=5445)
{'memory.lib': 0, 'io_counters.read_count': 57969436, 'ctx_switches.voluntary': 31976, 'memory.dirty': 0, 'memory.rss': 43364352, 'memory.vms': 276250624, 'memory.shared': 2371584, 'conns.unix_sockets.total': 1, 'memory.percent': 0.13856976163566506, 'memory.text': 8192, 'cpu.percent': 0.0, 'cpu.user': 3.44, 'cpu.system': 2.99, 'io_counters.write_bytes': 91990548480, 'fds': 7, 'ctx_switches.involuntary': 735, 'threads': 1, 'io_counters.read_bytes': 314886582272, 'io_counters.write_count': 27335152, 'memory.data': 116027392}
```
* Если нет процесса или закончился по время измерения - вернёт пустой dict


### Статистика по pids, много процессов (изначальная функциональность)
```python
>>> import metrics_per_process as mp
>>> mp.multi_pid_process_stats(pids=[5453, 5434, 3423])
Counter({'io_counters.read_bytes': 417521979392, 'io_counters.write_bytes': 159438630912, 'memory.vms': 1640751104, 'memory.data': 683687936, 'memory.rss': 241745920, 'io_counters.read_count': 93026314, 'io_counters.write_count': 43896027, 'memory.shared': 8151040, 'ctx_switches.voluntary': 230550, 'memory.text': 49152, 'ctx_switches.involuntary': 9371, 'fds': 50, 'cpu.system': 25.92, 'cpu.user': 21.659999999999997, 'conns.unix_sockets.total': 6, 'threads': 6, 'total_processes': 6, 'memory.percent': 0.7724933722241383})
```
* Все метрики суммированы по процессам
* Если нет процесса или закончился по время измерения - просто не будет учтён.
* если метрика в сумме 0, то её не будет в выхлопе.


### Расширенная статистика по процессам, полученным по условиям, с добавлением скорости изменения метрик (новая функциональность)
```python
>>> import metrics_per_process as mp
>>> mp.get_processes_stats_ex(process_names=[‘foo’, ‘bar’],
                           users=[‘max’, ‘sam’],
                           process_env={'TAG_ENV_VAR': 'whatever', 'OTHER_VAR': None},
                           interval_sec=1,
                           keep_important_metrics=True,
                           include_connections=True)

Counter({'fetch_time': '1.19604', 'io_counters.read_bytes': 422418259968, 'io_counters.write_bytes': 160601030656, 'memory.vms': 811999232, 'memory.data': 335605760, 'memory.rss': 115433472, 'io_counters.read_count': 93567893, 'io_counters.write_count': 44179119, 'memory.shared': 4857856, 'ctx_switches.voluntary': 220626, 'memory.text': 24576, 'ctx_switches.involuntary': 8847, 'io_counters.write_bytes_per_sec': 3760.8026340704605, 'fds': 25, 'cpu.system': 22.87, 'cpu.user': 21.840000000000003, 'total_processes': 11, 'threads': 11, 'io_counters.write_count_per_sec': 7.345317644668868, 'ctx_switches.voluntary_per_sec': 7.345317644668868, 'io_counters.read_count_per_sec': 7.345317644668868, 'conns.unix_sockets.total': 3, 'memory.percent': 0.3688649308034677, 'cpu.percent': 0.0, 'io_counters.read_bytes_per_sec': 0.0})
```

* Добавляет скорость изменения всех метрик приведённую к value per sec, измеренную за интервал interval_sec (постфикс _per_sec). Наиболее важны здесь write_bytes_per_sec, read_bytes_per_sec
* Если process_names/users/env не указано, берутся любые names/users/env
* если метрика в сумме 0, то её не будет в выхлопе. Можно поставить keep_important_metrics=True, тогда обязательно добавятся некоторые важные метрики, даже если 0. Какие - см код.
* include_connections - можно попросить не считать сетевые/unix соединения, т.к. в некоторых случах это занимает чуть большее время
* Добавляется служебная метрика fetch_time - сколько времени в секундах занял анализ.
* Если процесс закончился во время интервала измерения - не будет учтён

## Грабли и особенности
### Может привирать i/o per_sec если часто завершаются дочерние процессы

Проблема такая: i/o счётчики (write_bytes, read_bytes, write_count, read_count) кумулятивные, берутся из /proc. Например, есть демон, скажем massindexer. Он запускает множество child процессов, те порождают своих child и пока работают child процессы, у каждого из них свои собственные счётчики i/o. Скорость изменения по каждому процессу считается, суммируется, и всё хорошо.

Но когда child завершаются, все байты write/read которые накопились у child, мерджатся в счётчики parent - происходит резкий скачок счётчиков у parent. У зомби-процессов это ещё интереснее - пока они висят как зомби, счётчики у них свои, а сливаются в parent они только после завершения зомби. К счётчикам самих зомби доступа нет. Т.е. если зомби висят по несколько минут, а потом умирают, получается непредсказуемое резкое увеличение счётчиков у родительского процесса, в зависимости от того, сколько начитали/написали за свою жизнь зомби.

В итоге: данные по скорости i/o иногда врут. В случае, для которого делалось это расширение - https://st.yandex-team.ru/MARKETINDEXER-7232 - оказалось достаточного медианного фильтра на данные по времени. Поэтому проблема актуальна, нужно с осторожностью доверять данным по скорости i/o


### Оптимизирован принцип получения данных от процесса
Используется as_dict вместо просто вызова функций - это значительно снижает время анализа


### Подпёрты различия версий psutil
Подпёр, т.к. наступил на эти грабли, запуская в разных средах и разных сборках - после версии 2.0.0 названия функций в psutil поменялись.


