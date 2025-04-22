# yql_formatter

Наколеночный yql formatter.

```
usage: yql_formatter [-h] [--in-place] [--convert-to-camelcase {on,off}] target

positional arguments:
  target

options:
  -h, --help            show this help message and exit
  --in-place, -i
  --convert-to-camelcase {on,off}, -cc {on,off}, default=on
```

Что делает:
- приводит все зарезервированные слова YQL к каноничному виду (`select` -> `SELECT`, `listnotnull` -> `ListNotNull`)
- переименовывает все snake_case $-выражения в camelCase: `$do_stuff` -> `$doStuff`, `$ALL_CAPS` -> `$ALL_CAPS` (не трогает). Это можно отключить с помощью `--convert-to-camelcase off`.
    - кидает ворнинг, если в изначальном файле есть и `$do_stuff`, и `$doStuff`.
- по умолчанию создаёт для `{query}.sql` файл вида `{query}_output.sql`, но можно передать параметр `--in-place`/`-i`, и тогда файлы будут перезаписаны.
- умеет обрабатывать и один файл, и папку (берёт все файлы с расширениями `.yql` и `.sql`).

Чем отличается от родного форматтера YQL:
- не трогает whitespace
- родной форматтер не умеет переименовывать snake_case в camelCase.