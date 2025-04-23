# Testcop

## Шедулеры

### aggregate-builds-by-day

* [sandbox-шедулер](https://sandbox.yandex-team.ru/scheduler/705870/view)
* [код шедулера](https://a.yandex-team.ru/arcadia/devtools/fei-schedulers/infra/testcop/aggregate-builds-by-day)

#### Описание

Собирает и агрегирует по дням информацию из таблицы `testcop.suites` в таблицу `testcop.builds`.

Запускается раз в день. На выходе имеем информацию о каждом тесте за конкретный день:

* мета-информацию о тесте
* кол-во его прогонов, а также их результат
* список sandbox-задач, в которых он выполнялся

Таблица `testcop.builds` используется ручкой тесткопа [/mutes-to-skip][mutes-to-skip] для определения кандидатов на заскип.

#### Настройка шедулера

Для настройки шедулера доступны переменные окружения:

* `GET_DATA_INTERVAL` – интервал времени, на которые нужно разбивать получаемые данные, по умолчанию 12 (должно делить 24 без остатка)

### skip-muted-tests

* [sandbox-шедулер](https://sandbox.yandex-team.ru/scheduler/705869/view)
* [код шедулера](https://a.yandex-team.ru/arcadia/devtools/fei-schedulers/infra/testcop/skip-muted-tests)

#### Описание

Проходится по всем проектам из конфига Тесткопа. После, для каждого проекта получает с помощью ручки [/mutes-to-skip][mutes-to-skip] список тестов, которые в последних `N` сборках мьютились более чем в `n`% случаев (где `N` – `buildCountToAnalyze`, а `n` – `muteRateLimit` из раздела autoSkip конфигурации проекта). Затем отключает их с помощью [testcop-cli][testcop-cli].

Также в шедулере задается [шаблон][skip-template] для создаваемых тикетов.

#### Настройка шедулера

Для настройки шедулера доступны переменные окружения:

* `PROJECTS_TO_EXCLUDE` – список проектов через запятую, для которых тесты автоскипаться не будут
* `ALLOWED_PROJECTS` – список проектов через запятую, для которых будут работать автозаскипы
* `TESTCOP_ISSUE_AUTHOR` – логин пользователя, который будет указан автором создаваемых тикетов

[mutes-to-skip]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/testcop/server/routes/api.ts?rev=r9461149#L1136

[testcop-cli]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/testcop-cli

[skip-template]: https://a.yandex-team.ru/arcadia/devtools/fei-schedulers/infra/testcop/skip-muted-tests/constants.js?rev=r9306896#L9
