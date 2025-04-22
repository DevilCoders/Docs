# Скрипт клонирования регулярных задач

## Описание

Автоклонирование повторяющихся задач в **Startrek** служит для автоматизации рутинной работы.

* `clone-issue.js` - модуль для клонирования регулярных задач.
* `clone-issue-cli.js` - CLI обёртка для удобной работы из терминала.

## Запуск

```bash
export STARTREK_TOKEN={{OAUTH-TOKEN}}
node script/clone-issue.js
```

Описание параметров `node script/clone-issue.js --help`

Пример запуска

```bash
node lib/clone-issue-cli/clone-issue-cli.js -q 'Filter: 666666666' --range 14 --fields 'followers, storyPoints, queue, tags, components, abcService' --prev-line-pattern 'Предыдущее дежурство:' --next-line-pattern 'Следующее дежурство:' --summary-date-format 'interval' --set-current-sprint --set-opened-issue-links
```

### Примечания

Запрос в Startrek должен вернуть только один тикет, иначе будет ошибка.

Чтобы клонирование прошло корректно, необходимо клонируемую задачу заранее настроить.
Проставить спринт, фолловеров, компоненты и тд.

Чтобы заголовок задачи устанавливался верный, необходимо придерживаться следующего формата: **Заголовок — Дата**.

> _— (\u2014) длинное тире (EM DASH)_, [подробнее](https://www.artlebedev.ru/kovodstvo/sections/97/).

## Запуск клонирования шедулером в Sandbox

Автоклонирование задач можно запустить шедулером в **Sandbox**. Задача **TRENDBOX_CI_JOB** отвечает за запуск.

>**Примечание**
>
>Для работы автоклонирования необходим **STARTREK_TOKEN**, который в Sandbox берётся из **vault** по **овнеру** задачи (**env.STARTREK_TOKEN**).

### Настройка задачи

* **Package name** – @yandex-int/trendbox-ci.cli
* **Package version** – canary
* **NPM registry** – `http://npm.yandex-team.ru`
* **bin** – trendbox

Конфигурация **TRENDBOX_CI_JOB** для клонирования задач:

```json
{
  "debugShell": true,
  "language": "node_js",
  "env": "node_js=8 DEBUG=*",
  "lifecycle": {
    "prepare": [
      "nvm install $node_js",
      "trendbox checkout -c $checkout_config --dir sources",
      "cd sources",
      "hash -r"
    ],
    "script": [
      "node script/clone-issue.js -q 'Filter: 666666666' --range 14 --fields 'followers, storyPoints, queue, tags, components, abcService' --prev-line-pattern 'Предыдущее дежурство:' --next-line-pattern 'Следующее дежурство:' --summary-date-format 'interval' --set-current-sprint --set-opened-issue-links"
    ]
  },
  "checkout": {
    "type": "git",
    "url": "https://github.yandex-team.ru/search-interfaces/ci.git",
    "branch": "master"
  }
}
```

### Запущенные шедулеры

[Список на Sandbox](https://sandbox.yandex-team.ru/schedulers?page=1&order=-id&pageCapacity=20&task_type=TRENDBOX_CI_JOB)

## TODO

* Научить шаблонизировать описание.
