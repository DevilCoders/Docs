# Общие сведения

Данная програма необходима для конвертации данных из YT в файлы.

Данные из YT - это генлоги. [Пример](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/stratocaster/mi3/main/last_complete/genlog/0000).

Выходные файлы - это данные, в удобном для репорта виде, которые не относятся к индексу.

Программа пробегается по всем строчкам YT таблицы (последовательно) и для каждой строчки выполняет свою логику конвертации файл.

# Разработчикам

## Требования к дамперам
1. Быть [идемпотентным](https://ru.wikipedia.org/wiki/%D0%98%D0%B4%D0%B5%D0%BC%D0%BF%D0%BE%D1%82%D0%B5%D0%BD%D1%82%D0%BD%D0%BE%D1%81%D1%82%D1%8C)
2. Не модифицировать входные данные

## Создать новый дампер
1. Писать код в поддиректории dumpers
2. Добавить инклюд в файл dumpers/AllDumpers.h в алфавитном порядке
3. Добавить свой дампер в свитч в файле dumpers/DumperGenlogFields.cpp . Нужно для того, чтобы дампер читал как можно меньше лишних данных.
4. Отредактировать main.cpp с вызовом создания своего дампера
5. Написать тест в поддиректории ut или market/idx/generation/tests/yatf/genlog_dumper

# Примеры запуска

### Все дамперы
```
iurik@ps05et:~/bin$ ./genlog_dumper --yt-proxy hume --input //home/market/testing/indexer/planeshift.balalaika-ps05et/mi3/main/20190319_1550/genlog/0000 --output /tmp/genlog_dumper --yt-token-path /etc/datasources/yt-market-indexer
```

### Конкретные дамперы
```
iurik@ps05et:~/bin$ ./genlog_dumper --yt-proxy hume --input //home/market/testing/indexer/planeshift.balalaika-ps05et/mi3/main/20190319_1550/genlog/0000 --output /tmp/genlog_dumper --yt-token-path /etc/datasources/yt-market-indexer --dumper QVAT --dumper WARE_MD5
```

### Статистика
Если вы хотите получить статистику работы дамперов на выходе, то необходимо добавить флаг
```
--summary-path /tmp/genlog_dumper/summary.txt
```
В результате мы получим файлик вида:
```
iurik@ps05et:~/bin$ cat /tmp/genlog_dumper/summary.txt
num_offers	1538633
proto_parse_time	8010
next_row_time	8148
QVAT_WORKER_TIME	317
WARE_MD5_WORKER_TIME	417
```
где
* proto_parse_time - это время затраченное на парсинг proto из YT таблицы для всех офферов
* next_row_time - общее время скачивания данных из YT для всех офферов
* *_WORKER_TIME - общее время работы конкретного воркера для всех офферов

### Уровень логирования
Повышения уровня логирования можно проставить флаг
```
--log-level 7
```

### Локальный режим
Для работы в локальном режимк необхоим флаг  `--local-mode`. В этом режиме для флага `--input` нужно передать путь к папке, где храняться протобуфины офферов. Пример запуска:
```
iurik@ps05et:~/bin$ ./genlog_dumper --input /tmp/dump_genlog_proto --output /tmp/genlog_dumper --local-mode
```
