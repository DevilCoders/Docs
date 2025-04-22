### Вспомогательные функции для запуска многопоточных джоб [`mt_jobs`](/arc/trunk/arcadia/maps/analyzer/libs/mt_jobs)
Позволяют рассчитать количество используемых потоков.

Функция `set_threads_count` принимает аргументы:
* `data_size_per_thread` - размер входных данных на один поток
* `mem_per_thread` - размер памяти на один поток; по умолчанию 512Mb
* `threads` - опционально можно передать количество потоков
* `logger` - опционально можно передать логгер
Пример:
```python
job = BinaryCmd(
    'resource', params,
    on_limits_set=mt_jobs.set_threads_count(data_size_per_thread, mem_per_thread, threads, logger)
)
```
