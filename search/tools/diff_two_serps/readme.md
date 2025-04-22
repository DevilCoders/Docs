# diff-two-serps

Тулза позволяет задать одинаковый план запросов в две реплики и сравнить выбранные поля ответа.

## Подготовка плана

Для подготовки плана запроса нужно поспользоваться скриптом `gen-plan-basesearch.sh`. Он заходит на указанный хост, включает там event-log, собирает запросы и сохраняет два файла в output-dir: `plan.txt` и `plan_pc_none.txt`. В первом у запросов добавлен `hr=da` для ручного прострела, во втором `pc=none`, то есть ответ приходит в виде несжатого протобуфа. Утилите рекомендуется указывать именно второй файл, так как с ответами от первого есть проблемы с неюникодными символами в ответе (пока не пофикшено).

```
$ ./gen-plan-basesearch.sh
Usage:
    ./gen-plan-basesearch.sh <container-hostname> [output-dir]

$ ./gen-plan-basesearch.sh base.man-web-search-man-web-rj0hbopk-2548.man.yp-c.yandex.net plan_dir

Found process 100 /httpsearch/basesearch -p 80 -d /web/WebTier1.prod.man.cfg -V AbnormalityLog=/dev/null -V Cores=17 -V DNSCachePath=/remote_storage_configs/man/general_dns_cache.proto -V EventLog=/var/log/webruntime/prod/eventlog.log -V IndexDir=primus-WebTier1-0-1072-1617958822 -V LoadLog=/dev/null -V MXNetFile=/models.archive/models.archive -V PassageLog=/dev/null -V RemoteIndexArcConfigPath=/remote_storage_configs/man/primus-WebTier1-0-1072-1617958822.proto -V SelfFqdn=man-web-search-man-web-rj0hbopk-2548.man.yp-c.yandex.net -V ServerLog=/var/log/webruntime/prod/server.log -V UseMultiLevelCacheIndexMapping=True -V ArcLruCacheEnabled=true -V RemoteSearch=True -V MultiLevelCacheIndexMappingSuffix=
Found event log /var/log/webruntime/prod/eventlog.log
Finished downloading event log, removing control...
```

## Отстрел

Во время отстрела по-умолчанию диффуются поля `Head`, `Grouping`, `ErrorInfo` и `SearcherProp(Key=Unanswer_RemoteStorage)`. Добавить поля можно в `util.py:diff_two_serps`, там есть переменная `mask`. Позже для этого можно сделать какой-то простой язык, чтобы снаружи указывать нужные поля.

При отстреле надо указать файл с планом (рекомендуется указывать `plan_pc_none.txt`) и два эндпоинта с портами в формате `<host>:<port>`:

```
$ ./diff_two_serps --help
usage: diff_two_serps [-h] [--base-dir BASE_DIR] [--diff-max DIFF_MAX] [--bad-diff-limit BAD_DIFF_LIMIT] [--retry-on-diff RETRY_ON_DIFF] PLAN_FILE BASE_ENDPOINT PATCHED_ENDPOINT

Sends requests to intsearch/basesearch and compares responses.

positional arguments:
  PLAN_FILE             file with url of format 'http://#ENDPOINT#/your/url/path' on each line
  BASE_ENDPOINT         endpoint to use as base in comparison
  PATCHED_ENDPOINT      endpoint to compare with base

optional arguments:
  -h, --help            show this help message and exit
  --base-dir BASE_DIR   directory to write requests, responses, diffs (default is $PWD)
  --diff-max DIFF_MAX   single diff lines to consider as diff (default 1)
  --bad-diff-limit BAD_DIFF_LIMIT
                        stop shoot after exceeding this limit with non-flap diffs (default 1)
  --retry-on-diff RETRY_ON_DIFF
                        number of retries in case of diff (default 5)
```

Пример запуска: 

```
$ ./diff_two_serps --base-dir ~/tmp/diffs/ ~/tmp/plan_dir/plan_pc_none.txt base.man-web-search-man-web-rj0hbopk-2548.man.yp-c.yandex.net base.man-web-search-man-web-rj0hbopk-1072.man.yp-c.yandex.net
```

Если всё хорошо, то в консоли посыпятся сообщения об отстреле:

```
ERROR:root:1 finished
ERROR:root:101 finished
ERROR:root:201 finished
ERROR:root:301 finished
ERROR:root:401 finished
ERROR:root:501 finished
ERROR:root:601 finished
...
```

В случае диффа на запросе будет напечатана строка вида 
```
ERROR:root:Bad diff for 2930 request (105 lines, 4 retry)
```

Если в конце строки есть слово FLAP, то можно увеличить `--retry-on-diff` до 10 и количество флапов (разных ответов одного сервера на одном запросе) должно сильно уменьшиться. Пример строки с флапом:

```
ERROR:root:Bad diff for 2930 request (105 lines, 4 retry) FLAP
```