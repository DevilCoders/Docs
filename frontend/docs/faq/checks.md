# Continuous Integration

CI в монорепозитории реализован на основе [trendbox-ci](https://github.yandex-team.ru/search-interfaces/trendbox-ci).

## Как работает

Фактически [trendbox-ci](https://github.yandex-team.ru/search-interfaces/trendbox-ci) запускает скрипты
из пакетов и сервисов на основе [конфигурации](../.trendbox.yml).

## Подключение

Для того, чтобы сервис или пакет получил поддержку в CI, необходимо в `package.json` в секцию `scripts` добавить необходимые скрипты.
Ни один из них не является обязательным, отсутствие любого CI проигнорирует.
Тем не менее на основе соглашения крайне желательными считаются скрипты для сборки и запуска любых тестов.

## Units

[Описание проверки](./units.md)

## Отчет проверки в PR

Для отображения результатов проверок в PR, необходимо настроить сохранение отчета в папку `__reports` внутри своего пакета/сервиса,
соблюдая следующий паттерн названия отчета `report-<Название проверки>-<любой суффикс>`.

Отчет может быть html- или txt-файлом, либо папкой с вложенным `index.html`.

Примеры:

- `./__reports/report-unit.html`
- `./__reports/report-unit-coverage/index.html`

## Список запускаемых в CI скриптов

- `ci:artifacts` - сборка артефактов в динамический пакет
- `ci:build` - сборка
- `ci:deploy` - деплой беты при создании и обновлении пул-реквеста
- `ci:deploy:remove` - удаление беты на влитие или закрытие пул-реквеста
- `ci:deploy:master` - деплой тестинга при влитии в master
- `ci:deploy:static` - деплой статических файлов
- `ci:deploy:release` - кастомизация деплоя релизной ветки
- `ci:hermione` - запуск hermione тестов
- `ci:e2e` - запуск e2e тестов
- `ci:testpalm:validate` - проверка тестовых сценариев
- `ci:testpalm:synchronize` - выгрузка тестовых сценариев в TestPalm
- `ci:testpalm:synchronize:testing` - выгрузка тестовых сценариев в TestPalm для пул-реквеста
- `ci:testpalm:suite` - автозапуск асессоров
- `ci:unit` - запуск модульных тестов
- `ci:unit:coverage` — покрытие модульными тестами
- `ci:pulse:static` - запуск Pulse Static
- `ci:pulse:shooter` - запуск Pulse Shooter

### Hermione

> Подробнее о настройке Hermione напишем в рамках [FEI-20970](https://st.yandex-team.ru/FEI-20970)

Черновик по настройке:

* json-репорт Гермионы должен называться `__reports/report-hermione:ci.json` (для автоматической генерации html-файлика тесткопа)
* Дампы клемента должны лежать в папке `test-data`. Минискрипт на баше для переименования папок (dumps → test-data): `find ./tests/features/desktop -type d -name dumps | sed -E 's/^((.+)dumps)$/\1 \2test-data/' | xargs -L 1 -I {} sh -c "mv {}"`.
* Обновить `@yandex-int/tunneler` до последней версии, потому что в монорепе некоторые важные настройки передаются в тунеллер через переменные окружения (раньше не было поддержки этих переменных). Сломаться ничего не должно.
* Перейти на монорепный `tunneler` для запуска Hermione-тестов (только для ci):
    * опция конфига hosts: ['tun.si.yandex-team.ru']
    * опция cloud: 'yp'
    * опция version: 2
    * Во время миграции эти настройки можно будет удалить, т.к. они определены в монорепе.
    * [Гайд по подключению](https://a.yandex-team.ru/arc/trunk/arcadia/serp/infra/docs/ru/tunneler/tunneler.md#подключение)
* Настроить запуск Гермионы
  * Настроить плагин тунеллера.
  * Если вы использовали клиент секретницы yav, замените его на ya vault.
  * Выдайте роботу @robot-frontend права на чтение ваших секретов.
* Если вы генерировали файлик testcop-link.html, то перестаньте это делать. Монорепа сама его умеет создавать.

## Линтеры

[Описание проверки](./linters.md)

### Валидация конфига селективности

> ⚠️ Временно проверка всегда проходит успешно, что будет исправлено после [задачи](https://st.yandex-team.ru/FEI-20584).

Если *pre*-коммит хук или проверка в *CI* упала примерно с такой ошибкой:

```bash
✖ selectivity validate --config .config/selectivity.conf.js:
File "baz.quux" is not covered by patterns from a config
File "foo.bar" is not covered by patterns from a config

✗ 2 errors
```

то это значит, что в рамках ревью-реквеста были добавлены файлы, которые не покрываются масками из конфига селективности (подробнее в [документации](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/selectivity/README.md#валидация)).

Чтобы линтер перестал завершаться с ошибкой, необходимо добавить маски в конфиг селективности (или в корневой [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/.config/selectivity.conf.js), или в конфиг для проекта), которые покрывают добавленные файлы в рамках ревью-реквеста.

## События запуска `ci:deploy` скриптов

| `type` | `event` | `name` | `cmd` |
|--------|---------|--------|-------|
| `pull_request` | `created` | `*` | `ci:deploy` |
| `pull_request` | `updated` | `*` | `ci:deploy` |
| `pull_request` | `merged` | `*` | `ci:deploy:remove` |
| `pull_request` | `declined` | `*` | `ci:deploy:remove` |
| `branch` | `push` | `master` | `ci:deploy:master` |
| `branch` | `push` | `release/**/*` | `ci:deploy:release` (if exists) |
| `branch` | `push` | `release/**/*` | `ci:build; ci:deploy:static; ci:artifacts; nanny-workflow create-release` |

