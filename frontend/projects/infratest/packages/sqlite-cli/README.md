# sqlite-cli

Утилита для манипуляций с SQLite-базами данных.

## Установка

```bash
$ npm install @yandex-int/sqlite-cli --registry=http://npm.yandex-team.ru
```

## Использование

```bash
sqlite-cli --help

Usage: sqlite-cli [options] [command]

Options:
  -V, --version    output the version number
  -h, --help       output usage information

Commands:
  merge [options]
```

### merge

Команда для объединения нескольких SQLite-баз данных. Объединение без потери данных осуществляется только для таблиц, в которых все первичные ключи "естественные", то есть не образуются путём автоинкремента.

```bash
sqlite-cli merge --help

Usage: merge [options]

Options:
  -i, --input <input>    input database to be merged
  -o, --output <output>  output database
  -h, --help             output usage information
```

