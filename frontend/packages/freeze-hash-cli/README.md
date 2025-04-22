# freeze-hash-cli

Инструмент для подсчета хеша в именах файлов фризовой статики.

:warning: На данный момент `freeze-hash-cli` умеет смотреть лишь только в завтрашний день и предсказывать итоговый `url` на `yastatic.net`.

Подробности о смысле существования пакета можно узнать в [документации по выгрузке статики](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/docs/deploy-static.md).

В наличии есть [пакет с hash-функцией](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/freeze-hash).

## Установка

```console
npm i @yandex-si/freeze-hash-cli -reg=https://npm.yandex-team.ru
```

## Использование

```console
npx freeze-hash file1.jpg file2.svg file3.woff2
cat myfile.jpg | npx freeze-hash --no-ext
```

## Команды

### freeze-hash

Считает хеш используя алгоритмы вебпака для файлов, произвольного содержимого или входного потока.

```console
$ npx freeze-hash --help

Calculate hash for static (freeze) files in conventional format

Positionals:
  files  Files for calculating hashes                                                [string]

Freeze Hash Options:
  --format, -f         Webpack loader format          [default: "[sha1:hash:base58:8].[ext]"]
  --content, -c        Content to calculate hash
  --resource-path, -r  Path                                                [default: "a.bin"]
  --no-ext             Drop extension in format (works only for the default one)

Common options:
  --help, -h       Show help                                                        [boolean]
  --version, -v    Show version number                                              [boolean]
  --output-format  Format of the output, could be text for people or json for pipes
                                         [string] [choices: "text", "json"] [default: "text"]
```

Если не передать ни файлы, ни опцию `content`, по умолчанию будет использоваться `/dev/stdin`.

## Опции

* [output-format](#output-format)
* [format][#format]
* [content][#content]
* [resource-path][#resource-path]
* [no-ext][#no-ext]

### output-format

Позволяет управлять форматом вывода данных.

При выставлении опции в значение `json` (`--output-format=json`) результат выполнения будет выведен в `stdout` в виде JSON-объекта, который может быть интерпретирован другой командой.

Если вам не нужно использовать команды в конвейере и вы явно хотите получать результат выполнения в человекочитаемом виде, выставляйте опцию в значение `text` (`--output-format=text`, по умолчанию).

### format

Позволяет управлять алгоритмами расчета хешей.

Пакет для унификации основан на `loader-utils`, и полный список поддерживаемых конструкций можно изучить в официальной документации: https://github.com/webpack/loader-utils#interpolatename

```console
$ echo 42 | npx freeze-hash -f '[emoji:4]'
Freeze (42) = 🤾🏽‍♀️🇸🇴👰🏻😲
```

### content

Параметр позволяет передать содержимое для расчета хеша в качестве параметра.

```console
$ npx freeze-hash --content '42'
Freeze (42) = vMevTJLQ.bin
```

### resource-path

Совместимый с `loader-utils` параметр, с помощью которого можно задать произвольный `resourcePath` при расчете хеша. https://github.com/webpack/loader-utils#interpolatename

```console
$ npx freeze-hash -r /app/dir/file.png -f '[path][name].[ext]?[hash]' -c 42
Freeze (42) = /app/dir/file.png?c183857770364b05c2011bdebb914ed3
```

### no-ext

Вспомогательный флаг, который позволяет сбросить расширение у формата по умолчанию.
Не работает в случае передачи своего формата.

```console
$ npx freeze-hash --no-ext -c 42
Freeze (42) = vMevTJLQ
$ npx freeze-hash --no-ext -c 42 -f '[ext]'
Freeze (42) = bin
```
