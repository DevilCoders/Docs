# Школа разработки отдела Сергея Горобцова для **утилит и библиотек**

Для обсуждения присоединяйтесь к каналу   
**[#greyevil-school](https://yndx-all.slack.com/archives/C01FJ3RCDL5)** в Slack.

## Правила

- Следовать правилам необходимо всем новым утилитам и библиотекам. 

- **Жирным** выделены технологии и инструменты, которые **должны** использоваться.

- Технологии и инструменты не перечисленные в рамках категории **не должны** использоваться.

- Для категорий, не указанных в правилах, ограничений нет.

## Технологии

| | |
--- | ---
_Категория_ | _Технология_
Язык программирования | **[TypeScript](https://www.typescriptlang.org/)**
CLI | [yargs](https://www.npmjs.com/package/yargs) – разбор командной строки
Базовые алгоритмы и структуры данных | [lodash](https://www.npmjs.com/package/lodash)
Выполнение http-запросов | [got](https://www.npmjs.com/package/got)
Запуск переодических задач | [cron](https://www.npmjs.com/package/cron)
Логирование | [@yandex-int/yandex-logger](https://a.yandex-team.ru/arc_vcs/frontend/packages/yandex-logger)
Отправка писем | [nodemailer](https://www.npmjs.com/package/nodemailer)
Улучшение трейсов | [clarify](https://www.npmjs.com/package/clarify) – вырезание внутренних трейсов Node.js, [source-map](https://www.npmjs.com/package/source-map) – поддержка source maps
Управление конфигурацией | [@yandex-int/yandex-config](https://a.yandex-team.ru/arc_vcs/frontend/packages/yandex-config)

## Инструменты

| | |
--- | ---
_Категория_ | _Технология_
Code style | **[@yandex-int/lint](https://a.yandex-team.ru/arc_vcs/frontend/packages/lint)**. Включает в себя конфигурацию для eslint и prettier. **Правила нельзя смягчать, но можно расширять и делать строже**. 
Тесты | **[Jest](https://jestjs.io/)**, **[husky](https://www.npmjs.com/package/husky)** – запуск тестов перед коммитом, **[lint-staged](https://www.npmjs.com/package/lint-staged)** – запуск тестов только для изменённых файлов, [nock](https://www.npmjs.com/package/nock) – моки сетевых запросов, [supertest](https://www.npmjs.com/package/supertest) – моки http-cервера 
Работа с зависимостями | **npm**, **[yadi-bin](https://wiki.yandex-team.ru/product-security/yadi/)**  – проверка на уязвимости, [patch-package](https://www.npmjs.com/package/patch-package) – накладывание патчей
Запуск задач | **npm scripts** , [dotenv-cli](https://www.npmjs.com/package/dotenv-cli) – подмешивание переменных окружения в команды, [npm-run-all](https://www.npmjs.com/package/npm-run-all) – управление запуском задач, [ts-node](https://www.npmjs.com/package/ts-node) – интерпретация TypeScript на лету


## Инфраструктура
| | |
--- | ---
_Категория_ | _Технология_
Репозиторий | **Arc-монорепозиторий [arc_vcs/frontend/](https://a.yandex-team.ru/arc_vcs/frontend/)**
CI/CD | **Trendbox CI**, [Ревью кода](https://github.yandex-team.ru/devexp/devexp), [Merge Queue](https://github.yandex-team.ru/search-interfaces/microservices/tree/master/services/merge-queue), [CI-проверки](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/docs/faq/checks.md), [static-uploader](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/static-uploader), [ya tool](https://wiki.yandex-team.ru/yatool/)
