# hermione-cli

Полезные CLI команды для работы с [Hermione](https://github.com/gemini-testing/hermione).

> :warning: Пакет предназначен для использования внутри [ya make](https://docs.yandex-team.ru/ya-make/). Корректное использование в других окружениях не гарантируется.
>
> Если вам нужна одна из CLI команд данного пакета, то лучше реализовать ее через отдельный плагин к hermione ([пример](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/html-reporter-dumps-plugin/src/hermione/index.ts?rev=r9536408#L18-20)).

## Команды

### `read-tests`

Отличия от чтения тестов с помощью hermione:
- поддерживается возможность отключить все плагины при чтении тестов;
- поддержана возможность сохранять результат чтения тестов в файл;
- поддерживаются опции для разбиения тестов на чанки. Разбивка происходит за счет подключения плагина [hermione-chunks](https://github.com/gemini-testing/hermione-chunks);

```console
$ npx hermione-cli read-tests --help

  Usage: read-tests [options] [paths...]

  Read hermione-tests

  Options:

    -c, --config <path>        Path to hermione configuration file (default: .hermione.conf.js)
    -b, --browser <browser>    Read tests only in specified browser (default: [])
    -s, --set <set>            Read tests only in specified set (default: [])
    -r, --require <module>     Require module before read tests (default: [])
    --grep <grep>              Read tests that match the specified pattern
    --ignore <file-path>       Exclude paths from tests read (default: [])
    --silent                   Flag to disable events emitting while reading tests (default: false)
    --disable-plugins          Flag to disable all plugins from hermione config (default: false)
    --output-file <file-path>  Save results of read tests to passed file
    --use-chunks               Should split tests into chunks
    -h, --help                 output usage information

  Example of usage:
    Read hermione-tests with disabled plugins:
    npx hermione-cli read-tests --disable-plugins

    Save results of read tests to passed file:
    npx hermione-cli read-tests --output-file 'some-path/tests.json'

    Read tests and check that plugin "hermione-chunks" is specified in hermione-config:
    npx hermione-cli read-tests --use-chunks
```
