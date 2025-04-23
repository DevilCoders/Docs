Утилита rm_attrs
----------------

Генерирует sql-запросы для удаления атрибутов чанками по 1000 записей.

Формируем файлик из трех колонок запросом:
```
SELECT uid, type_id, value FROM attributes WHERE ...
```

Утилита генерирует запросы на удаление в транзакциях по 1000 операторов DELETE. Размер чанка настраивается (-c),

Можно использовать только две колонки (-k) и задать свое условие через командную строку (-w).

Настройка:
```
usage: rm_attrs [-h] [-c CHUNK_SIZE] [-d DELIMITER] [-k] [-w WHERE_CLAUSE]
                input_filename output_filename

Accepts a file with three columns (uid, attr_id, value) as input and forms SQL commands
to remove attributes by chunks. Ignore extra columns in the file

positional arguments:
  input_filename   Input filename or - for stdin
  output_filename  Output filename or - for stdout

optional arguments:
  -h, --help       show this help message and exit
  -c CHUNK_SIZE    Chunk size (default: 1000)
  -d DELIMITER     Column delimiter (default: \t)
  -k               Use only uid and type_id
  -w WHERE_CLAUSE  An additional condition for where clause
```