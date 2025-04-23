# Школа разработки отдела Сергея Горобцова для **сервера**

Для обсуждения присоединяйтесь к каналу
**[#greyevil-school](https://yndx-all.slack.com/archives/C01FJ3RCDL5)** в Slack.

## Правила

- Следовать правилам необходимо всем новым проектам. 

- **Жирным** выделены технологии, инструменты и инфраструктурные сервисы, которые **должны** использоваться в проекте.

- Технологии, инструменты или инфраструктурные сервисы не перечисленные в рамках категории **не должны** использоваться в проекте.

- Для категорий, не указанных в правилах, ограничений нет.

## Технологии

| | |
--- | ---
_Категория_ | _Технология_
Язык программирования | **[TypeScript](https://www.typescriptlang.org/)**
Фреймворк | 1. Node.js + [Express](https://github.com/expressjs/express), версия Node.js определяется  файлом [.nvmrc](https://a.yandex-team.ru/arc_vcs/frontend/.nvmrc) в монорепозитории; 2. AppHost
Логирование |[@yandex-int/yandex-logger](https://a.yandex-team.ru/arc_vcs/frontend/packages/yandex-logger)
Конфигурация | [@yandex-int/yandex-config](https://a.yandex-team.ru/arc_vcs/frontend/packages/yandex-config)
Работа с переводами | [@yandex-int/i18n](https://a.yandex-team.ru/arc_vcs/frontend/packages/packages/i18n), [tanker-kit](https://a.yandex-team.ru/arc_vcs/frontend/packages/packages/tanker-kit)
Улучшение трейсов | [Clarify](https://www.npmjs.com/package/clarify)
База данных | Postgres ([pg-promise](https://github.com/vitaly-t/pg-promise), [pg-pinger](https://a.yandex-team.ru/arc/trunk/arcadia/toolbox/pg-pinger/README.md)), [YDB](https://wiki.yandex-team.ru/kikimr/)

## Инструменты

| | |
--- | ---
_Категория_ | _Технология_
Code style | **[@yandex-int/lint](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/lint/README.md)**. Включает в себя конфигурации для eslint, stylelint и prettier. **Правила нельзя смягчать, но можно расширять и делать строже**. 
Unit-тесты | **[Jest](https://jestjs.io/)** (**[ts-jest](https://kulshekhar.github.io/ts-jest)**), [nock](https://github.com/nock/nock) – моки сетевых запросов, [supertest](https://github.com/visionmedia/supertest) – моки http-cервера
Работа с зависимостями | **npm**, **[yadi-bin](https://wiki.yandex-team.ru/product-security/yadi/)** – проверка на уязвимости, [patch-package](https://github.com/ds300/patch-package) – накладывание патчей
Запуск задач | **npm scripts**, **[husky](https://github.com/typicode/husky)** – запуск тестов перед коммитом, **[lint-staged](https://github.com/okonet/lint-staged)** – запуск тестов только для изменённых файлов, [npm-run-all](https://github.com/mysticatea/npm-run-all) – управление запуском задач, **[ts-node](https://github.com/TypeStrong/ts-node)** – интерпретация TypeScript на лету, [dotenv-cli](https://github.com/entropitor/dotenv-cli) - запуск с переменными окружения


## Инфраструктура
| | |
--- | ---
_Категория_ | _Технология_
Репозиторий | **Arc-монорепозиторий [arc_vcs/frontend/](https://a.yandex-team.ru/arc_vcs/frontend/)**
CI/CD | **Trendbox CI**, [Ревью кода](https://github.yandex-team.ru/devexp/devexp), [Merge Queue](https://github.yandex-team.ru/search-interfaces/microservices/tree/master/services/merge-queue), [CI-проверки](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/docs/faq/checks.md), [static-uploader](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/static-uploader), [ya tool](https://wiki.yandex-team.ru/yatool/)
Деплой приложения | AppHost, Awacs, Deploy + [базовые Docker-образы](https://github.yandex-team.ru/toolbox?utf8=%E2%9C%93&q=dockerfiles-) (текущий `registry.yandex.net/toolbox/nodejs:12.18.1-bionic`)
Локальное окружение для разработки | [tunneler](https://wiki.yandex-team.ru/users/unikoid/tunneler/) и/или [magicdev](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/magicdev)
Удалённое окружение для разработки | QYP. [Инструкция 1](https://wiki.yandex-team.ru/users/dmitryman/how-to-run-turbo-qyp/), [инструкция 2](https://wiki.yandex-team.ru/lp-constructor/razrabotka-kl-na-servere/).
Технические логи | [ErrorBooster](https://wiki.yandex-team.ru/error-booster/) через [стрим yandex-logger](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/yandex-logger/streams/error-booster), LogBroker+YP+YDB (в Deploy есть [из коробки](https://wiki.yandex-team.ru/deploy/docs/concepts/pod/sidecars/logs/))
Мониторинг | [Yasm](https://wiki.yandex-team.ru/golovan/), [Juggler](https://wiki.yandex-team.ru/sm/juggler/introduction/), [Monitorado](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/monitorado), [yasmkit](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/yasmkit). Всё, что можно настроить через monitorado, необходимо делать **только** через него.
Работа с переводами | [Tanker](https://wiki.yandex-team.ru/doc-and-loc/l10n/tools/tanker/)
