# testout

Инструмент для парсинга и фильтрации test.out.txt.

# Использование

```bash
Usage: @yandex-int/testout [errors] <test.out.txt path or url> [options]

test.out.txt reformatter

Options:
  -V, --version                 output the version number
  -l, --level [level]           log level filter (default: "WARNING")
  -f, --sources <sources>       sources filter with minimatch syntax (default: [])
  -o, --output-format [format]  log, json, push-client (default: "log")
  -s, --show-stacktraces        show stacktraces
  -w, --wrap                    wrap long lines
  -h, --help                    output usage information
  --task-type                   sandbox task type for push-client formatter
  --task-id                     sandbox task id for push-client formatter

Commands:
  *
  errors
```

### Примеры

Все записи с log level >= info за исключением темплара, показывать стектрейс:

```bash
testout ./test.out.txt -l info -f '!templar' -s
```

Краткая сводка по ошибкам:

```bash
testout errors https://proxy.sandbox.yandex-team.ru/935289013/test.out.txt
```
