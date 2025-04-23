# yml2tsv-cli

> CLI для [yml2tsv](https://github.yandex-team.ru/search-interfaces/ci/blob/master/packages/yml2tsv).

## Установка

```shell
npm install @yandex-int/si.ci.yml2tsv-cli --registry=https://npm.yandex-team.ru
```

## Использование

```shell
yml2tsv --config=cfg.json --output=output.json --error=error.json
```

## Локальный запуск

Из корня search-interfaces/ci выполните установку в глобальный скоуп:

```shell
npm install -g ./packages/yml2tsv-cli
```

Пакет будет установлен через симлинк, можно использовать в любой директории:

```shell
cd ~/Downloads
DEBUG=* yml2tsv […]
```

Правда, после этого вместо симлинок напихаются настоящие пакеты в `node_modules`, но вы что-нибудь придумаете.

## Описание аргументов

```console
Конвертация тест-сьюта из YAML-формата в JSON

Options:
  --help, -h        Show help                                          [boolean]
  --version, -v     Show version number                                [boolean]
  --config, -c      Путь к конфигурационному файлу.                   [required]
  --output, -o      Путь к файлу, в который будет сохранён результат
                    преобразования. По умолчанию stdin.
  --error, -e       Путь к файлу, в который будет сохранена ошибка (JSON). По
                    умолчанию stderr.
  --formatter, -f   Форматтер, который будет использоваться при генерации
                    результатов преобразования.
                    [choices: "default", "multi", "united"] [default: "default"]
  --group-size, -s  Максимальное число проверочных действий при использовании
                    потесткейсовой раздачи (multi). В united-форматтере
                    обозначает максимальное число тест-кейсов в одной группе.
                                                                   [default: 10]
  --group-time, -t  Максимальное время в секундах, требуемое на выполнение всех
                    проверочных действий в группе.               [default: 2700]
  --plugins, -p     Плагины (например: alternative-queries-plugin).
                                                           [array] [default: []]
  --resources, -r   Список подключаемых ресурсов в формате JSON (пример:
                    --resources.name=path/to/file)                 [default: {}]
```

## Обновление кубика в Nirvana

1. Найти в [списке][latest-yml2tsv] последнюю релевантную операцию (кубик).
1. В выпадушке справа нажать **Clone**, создастся черновик.
1. На вкладке _Overview_ обновить _Version number_. В качестве версии кубика используется версия пакета `yml2tsv-cli`.
1. На вкладке _Options_ обновить _job-command_:

    1. Указать новую версию пакета в команде `npx`

1. Обновить входные и выходные данные, а также опции, если это нужно.
1. Сверху справа нажать галочку без щитка (_Save changes and Approve_).
1. Пометить оригинальную операцию устаревшей, выбрав _Optional_.

> :warning: Важно выбрать именно _Optional_, а не _Mandatory_. В последнем случае, упадут все **уже запущенные** графы, т.к. эта опция означает «нельзя больше запускаться на старой версии».

[latest-yml2tsv]: https://nirvana.yandex-team.ru/operations/1/filter?@filterName=customFilter&tags=ExprTagsIn(yml2tsv)&deprecation=ExprFlowchartBlockTypeDeprecation(active)&@sorting=official:true,created:true
