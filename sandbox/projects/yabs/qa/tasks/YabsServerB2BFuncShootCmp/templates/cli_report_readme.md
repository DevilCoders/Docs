# Полный отчёт с разницей отстрелов

В `report_index.txt` находится grep-friendly индекс, выглядит он примерно так:

```
request.id: 9983; status: failed; handler: page; pre.code: 200; test.code: 200; tags: exts_base_info, exts_query_data, response_data, exts_request_data, logs_data, exts_headers_data; chunk_path: cli_diff/3.diff;
dd if=cli_diff/3.diff ibs=1 skip=0 count=738957 2> /dev/null
dd if=cli_diff/3.requests ibs=1 skip=0 count=3055 2> /dev/null

request.id: 1891800067504; status: failed; handler: count; pre.code: 200; test.code: 200; tags: logs_data; chunk_path: cli_diff/4.diff;
dd if=cli_diff/4.diff ibs=1 skip=0 count=11524 2> /dev/null
dd if=cli_diff/4.requests ibs=1 skip=0 count=3488 2> /dev/null

request.id: 30002; status: passed; handler: ; pre.code: 200; test.code: 200; tags: ;
```

grep команда для поиска упавших тестов с определенным тегом может выглядеть следующим образом:

```bash
$ grep -E "status: failed;.*tags: [a-z,_ ]*exts_query_data" report_index.txt -A 2 -m 5

request.id: 54890; status: failed; handler: meta; pre.code: 200; test.code: 200; tags: exts_query_data, response_data, logs_data; path: cli_diff/0.diff;
dd if=cli_diff/0.diff ibs=1 skip=127015 count=910613 2> /dev/null
dd if=cli_diff/0.requests ibs=1 skip=10159 count=3628 2> /dev/null
--
request.id: 4991; status: failed; handler: meta; pre.code: 200; test.code: 200; tags: exts_base_info, exts_query_data, exts_data, exts_request_data, logs_data, exts_headers_data; path: cli_diff/1.diff;
dd if=cli_diff/1.diff ibs=1 skip=4381561 count=321893 2> /dev/null
dd if=cli_diff/1.requests ibs=1 skip=90402 count=3527 2> /dev/null
```

Каждый запрос (в терминах ШМ это _тест_) записывается в виде одной или трёх срок. Если `status: passed`, то строка одна, если `status: failed`, то строки три. Во второй и третьей строках находятся dd-команды для отображения всех диффов на `failed` тесте в формате [unified diff](https://en.wikipedia.org/wiki/Diff#Unified_format), а так же текста оригинального запроса. Любая раскрашивалка диффа, принимающая unified diff, должна работать:

```bash
$ dd if=cli_diff/3.diff ibs=1 skip=0 count=738957 2> /dev/null | colordiff
```
