# testpalm-statistic-reporter-cli

> CLI-утилита для запуска плагинов-репортеров статистики.

## Установка

```shell
npm install @yandex-int/si.ci.testpalm-statistic-reporter-cli
```

## Использование

> :warning: Требуется токен в переменной окружения `TESTPALM_API_TOKEN` для
> доступа к TestPalm.

Если требуется включить плагин, но не передавать ему опции:

```shell
tsr --project-id serp-js --plugin=PLUGIN_NAME
```

Если требуется включить плагин и передать ему опции, то необходимо использовать следующий
синтаксис (отдельно `--plugin` писать не нужно):

```shell
tsr --project-id serp-js --plugin.first.options.some=true --plugin second
```

## Описание аргументов

```shell
Options:
  --help, -h        Show help                                          [boolean]
  --version, -v     Show version number                                [boolean]
  --service-id      Базовый сервис (например, serp-js)       [string] [required]
  --project-id      Идентификатор проекта в TestPalm.        [string] [required]
  --plugin          Описание плагина, который будет использоваться при запуске.
                                                              [array] [required]
```

> :book: Аргументы также можно передать через переменную окружения с префиксом `TSR_`,
> например `TSR_PROJECT_ID=serp-js`.
