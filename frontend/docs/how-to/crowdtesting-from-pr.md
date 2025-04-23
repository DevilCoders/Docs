# Краудтестирование в пулл-реквестах

Этот документ содержит инструкции, которые позволят тестировать пулл-реквест на асессорах, если у вас уже настроены процессы раздачи заданий на асессоров [по схемам serp-овых команд](https://wiki.yandex-team.ru/search-interfaces/infra/crowdtest/).

## Шаги внедрения

1. Возможность залипания на бете пулл-реквеста через продакшен.
2. Доступность статики из внешней сети.
3. Синхронизация тест-кейсов в проект для пулл-реквеста.
4. Создание флагов, добавленных в пулл-реквесте.
5. Создание экспериментов для изменившихся в пулл-реквесте тест-кейсов.
6. Настройки селективности.

### Шаг 1. Возможность залипания на бете пулл-реквеста через продакшен

[Подробная инструкция с шагами](./experiment-sticky.md).

### Шаг 2. Доступность статики из внешней сети

Если вы используете пакет `static-uploader` для работы со статикой, то достаточно добавить в конфиг (`.config/static/index.js`) вашего сервиса опцию `usePublicUrl` со значением `true` в секцию `s3`. Подробнее о формате конфига можно узнать из [документации](../../packages/static-uploader/README.md).

## Шаг 3. Синхронизация тест-кейсов в проект для пулл-реквеста

При условии, что у вас уже настроен `palmsync`, достаточно добавить:

1. пакет `@yandex-int/si.ci.testpalm-cli` в зависимости сервиса
2. следующие npm-скрипты в `package.json` сервиса:

```json
// package.json
"testpalm:synchronize:master": "palmsync synchronize",
"testpalm:synchronize:pr": "npm run testpalm:synchronize:pr:clone && npm run testpalm:synchronize:pr:palmsync",
"testpalm:synchronize:pr:clone": "npx @yandex-int/si.ci.testpalm-cli clone <TESTPALM_BASE_PROJECT_NAME> <TESTPALM_BASE_PROJECT_NAME>-$TRENDBOX_PULL_REQUEST_NUMBER",
"testpalm:synchronize:pr:palmsync": "palmsync synchronize -p <TESTPALM_BASE_PROJECT_NAME>-$TRENDBOX_PULL_REQUEST_NUMBER",

"ci:testpalm:synchronize": "npm run testpalm:synchronize:master",
"ci:testpalm:synchronize:testing": "npm run testpalm:synchronize:pr",
```

Обратите внимание на плейсхолдер `<TESTPALM_BASE_PROJECT_NAME>` его нужно заменить на название вашего основного проекта в TestPalm. Например, `uslugi` или `granny`.

## Шаг 4. Создание флагов, добавленных в пулл-реквесте

Необходимо добавить два конфига в сервис со следующим содержимым. В качестве примера используются конфиги из сервиса `ydo`. Подробнее о всех доступных полях можно узнать из документации [`expflags-cli`](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/expflags-cli).

```js
// .config/expflags/create.js
module.exports = {
    handlers: ['USLUGI'],
    platforms: ['desktop', 'touch'],
};

// .config/expflags/sync.js
module.exports = {
    // Опции, которые будут переданы при запуске.
    options: {
        validation: {
            validateValuesType: true,
        },
    },
    handler: 'USLUGI',
    service: 'uslugi',
    component: 'templates',
    source: 'uslugi',
};
```

## Шаг 5. Создание экспериментов для изменившихся в пулл-реквесте тест-кейсов

Необходимо добавить плагин [`palmsync-expflags-validator`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/palmsync-expflags-validator) в сервис, чтобы гарантировать корректность использования флагов в YAML-файлах. Инструкция по установке и настройке в самом плагине.

Необходимо добавить конфиг в сервис со следующим содержимым. В качестве примера используются конфиги из сервиса `ydo`. Для примера можно посмотреть существующие выборки в AB для вашего сервиса.

```json
// .config/expflags/testids.json
{
  // Хэндлер, которым обрабатываются флаги сервиса.
  "handler": "USLUGI",
  // Основной проект сервиса в TestPalm.
  "project": "uslugi",
  // Контекст, в котором работают флаги.
  "context": "MAIN.USLUGI.templates"
}
```

## Шаг 6. Настройки селективности

Добавьте в конфиг селективности (`.config/selectivity.conf.js`) информацию о следующих проверках:

* `testpalm:synchronize`
* `testpalm:validate`
* `expflags:upload`
* `expflags:convert-to-testids`

Обратите внимание, что проверка `expflags:convert-to-testids` зависит от всех трёх проверок, поэтому список общих паттернов, от которых они зависят должен быть синхронизирован.

Как правило, эти проверки должны запускаться при изменении YAML-файлов, hermione-тестов, флагов и конфигов. Если говорить конкретнее по проверкам, то:

* `testpalm:synchronize` и `testpalm:validate` — изменение YAML-файлов, hermione-тестов, флагов и конфигов.
* `expflags:upload` — изменение флагов и конфигов.
* `expflags:convert-to-testids` — изменение YAML-файлов, hermione-тестов, флагов и конфигов.

Подробнее про конфиг `selectivity` можно узнать в [документации](./selectivity.md).
