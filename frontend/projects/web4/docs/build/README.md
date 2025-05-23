# Сборка

Вся сборка в проекте использует [gulp](https://gulpjs.com/).

Сейчас на проекте два технологических стека разработки, сборка которых реализована по-разному:

- typescript/react — собирается через [tsc и webpack](./ts-react.md)
- priv/bemxjst/i-bem (устаревший стек) — собирается только [gulp-ом](./gulp.md)

Документация:

- [Стандартные команды](#Стандартные-команды)
- [Настройки](#Настройки)
- [Скорость](#Скорость)
- [Артефакты](#Артефакты)
- [Инициализация](#Инициализация)
- [Проверка типов](#Проверка-типов)
- [Доработки](#Доработки)

## VCS

> ⚠️ Внимание! Разработка ведётся на `arc`, не используйте `git` в работе.

* [Анонс про миграции разработки в arc](https://wiki.yandex-team.ru/search-interfaces/arc/)
* [Как работать с `arc`](https://wiki.yandex-team.ru/search-interfaces/arc/)
* [Как перенести существующий GitHub Pull Request в Arcanum](https://wiki.yandex-team.ru/search-interfaces/arc/#git-to-arc)

## Стандартные команды

* `npm run build` — выполнить gulp-сборку в dev-режиме
* `npm run build:testing` — собрать все в "testing"-режиме
* `npm run clean` — очистить кеши сборки (см. [кеши в ts/react](./ts-react.md#Кеши) и [кеши в gulp](./gulp.md#Кеши))

## Настройки

| Переменная окружения | Смысл | Доступные значения | Значение по умолчанию |
|----------------------|-------|--------------------|-----------------------|
| `YPROJECT` | Собираемая платформа | `desktop` `deskpad` (desktop) `touch` (touch-phone) `touch-phone` <пусто> | <пусто> (собираются все платформы) |
| `YENV` | Режим сборки | `development` `testing` `production` | `development` |
| `NOCACHE` | Отключение кеширования борщика и селективность сборки бандлов | `1` `0` | `0` |
| `SKIP_I18N` | Отключение сборки переводов | `1` `0` | `0` |
| `WEBPACK_FEATURES` | Фильтрация entry-файлов для webpack. Можно сократить время сборки при отладке. Можно использовать glob-паттерны. | Например, имя интересующей фичи: `LearnSerpFeature` | `**` |

Разница режимов сборки:

* `development` — режим разработки
  * серверный TS-код не собирается (см. [dev-режим](./ts-react.md#dev-режим))
  * js/css не минифицируются
  * картинки не [фризятся](https://github.com/borschik/borschik/blob/master/docs/freeze/freeze.ru.md)
  * пути к статике отностительные
* `testing` — режим для тестирования фиче-бранчей
  * React/TS-код **собирается**
  * js/css **минифицируются**
  * картинки не фризятся
  * пути к статике отностительные
* `production`
  * React/TS-код **собирается**
  * js/css **минифицируются**
  * картинки **фризятся**
  * пути к статике абсолютные; указывают на статический продакшен кластер

## Скорость

Текущее время сборки можно увидеть:

- на [графиках Инфры](https://charts.yandex-team.ru/preview/6pr5utomytks4?type=lastN&parent=SANDBOX_CI_WEB4&action=build&percentiles=95,80&target=180000&N=1) — общее время
- на [графиках Архи](https://dash.yandex-team.ru/pgqonf4vsc2km?tab=Qb) — срезы по разным этапа сборки

## Артефакты

Сборка собирает два вида файлов:

1. Cерверные шаблоны — это `pages-*/search/all/all.wrapped-server-templates.js`, в который включен весь priv/bemhtml-код, переводы, статика бандлов и другая статика, которая будет инлайнится на страницу. В этот же файл require-ятся скомпилированные ts-ом рантайм Табурета и реестры с адаптерами (и сами адаптеры, подключаемые там React-компоненты и библиотеки) из `.build/src`
2. Загружаемая статика выкладывается на "yastatic"
  - ajax-овые бандлы (см. "ajaxBundle" в [config](../../.enb/config/index.js))
  - ресурс-бандлы (см. "resource" в [config](../../.enb/config/index.js))
  - main-чанк
  - асинхронные чанки (подключаемые динамическими импортами)

## Инициализация

Собранный файлы включаются в рантайм так:

- Cерверные шаблоны подключаются в `pages-*/search/renderer.js` и далее в ReportRenderer, который на каждый запрос выполняет функцию, которую возвращает [templateRunner.getMain](../../src/lib/taburet/packages/template-runner/index.ts)
- Внешняя статика (см. `static-links.priv.js`) загружается отдельным ресурсом:
  - jquery
  - react-with-dom-and-polyfills
- инициализация статики на клиенте:
  - i-bem-код начинает инициализироваться по DOMContentLoaded
  - react-код фичей гидрируется, когда загружен react и main-чанк (зависимость реализована через `Ya.define`)

## Проверка типов

Проверка типов вынесена в линтер [`typechecking`](../../tools/linters/typechecking.js) для ускорения процесса разработки. В процессе работы нужно полагаться либо на редактор, например, для проверок в рамках вашей фичи, либо на запуск компиляции всего проекта с помощью `tsc`, например, для проверки глобальных изменений.

## Доработки

Тестирование любой задачи, изменяющей код сборки должно включать ручное тестирование по [сценарию](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/features/common/infra/build.testpalm.yml). Автотестов для сборки пока нет.

Кроме того, проверяйте время выполнения затронутого в задаче шага сборки в dev и testing (CI). Для этого есть два инструмента:

1. В "Автосборке" пулл-реквеста (sandbox-таска с типом SANDBOX_CI_WEB4) в футере есть строка "Building" со временем сборки
2. На [графиках Архи с фильтрами](https://dash.yandex-team.ru/pgqonf4vsc2km?tab=Zr) указать пользователя "sandbox", ветку "pull-{id-вашего-pr}" и выбрать нужные метрики

Время не должно расти. Любые возможные замедления нужно обсуждать с командой Архитектуры.
