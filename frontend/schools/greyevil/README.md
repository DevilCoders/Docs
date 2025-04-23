# Школа разработки отдела Сергея Горобцова для **фронтенда**

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
Язык программирования | **TypeScript**
CSS | **PostCSS**
CSS Modules | **Не разрешены**
Фреймворк на клиенте | **React**. Версия определяется пакетом, @yandex-int/react-static-version.
Фреймворк на сервере | AppHost или Node.js + Express. Версия Node.js определяется  файлом [.nvmrc в монорепозитории](https://a.yandex-team.ru/arc_vcs/frontend/.nvmrc).
Библиотека компонентов | [lego-components](https://lego.yandex-team.ru/components/lego/latest/)
Загрузка шрифтов | [yandex-font](https://a.yandex-team.ru/arc_vcs/frontend/projects/lego/packages/yandex-font)
Управление состоянием | Redux
WebSockets на клиенте | window.WebSocket
Логирование на сервере |[@yandex-int/yandex-logger](https://a.yandex-team.ru/arc_vcs/frontend/packages/yandex-logger)
Логирование на клиенте | [error-counter](https://github.yandex-team.ru/RUM/error-counter)
Конфигурация | [@yandex-int/yandex-config](https://a.yandex-team.ru/arc_vcs/frontend/packages/yandex-config)
Работа с переводами | [@yandex-int/i18n](https://a.yandex-team.ru/arc_vcs/frontend/packages/packages/i18n), [tanker-kit](https://a.yandex-team.ru/arc_vcs/frontend/packages/packages/tanker-kit)
Базовые алгоритмы и структуры данных | lodash
Выполнение http-запросов | got
Улучшение трейсов | [clarify](https://www.npmjs.com/package/clarify) – вырезание внутренних трейсов Node.js, [source-map](https://www.npmjs.com/package/source-map) – поддержка source maps

## Инструменты

| | |
--- | ---
_Категория_ | _Технология_
Сборка | **[Webpack](https://webpack.js.org/)** 
Code style | **[@yandex-int/lint](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/lint/README.md)**. Включает в себя конфигурации для eslint, stylelint и prettier. **Правила нельзя смягчать, но можно расширять и делать строже**. 
Unit-тесты | [Jest](https://jestjs.io/), [nock](https://www.npmjs.com/package/nock) – моки сетевых запросов, [supertest](https://www.npmjs.com/package/supertest) – моки http-cервера
React-тесты | [Enzyme](https://github.com/enzymejs/enzyme) 
E2E-тесты | **[Hermione](https://github.com/gemini-testing/hermione)** 
Песочница компонентов | [Storybook](https://storybook.js.org/) 
Работа с зависимостями | **npm**, **[yadi-bin](https://wiki.yandex-team.ru/product-security/yadi/)** – проверка на уязвимости, [patch-package](https://www.npmjs.com/package/patch-package) – накладывание патчей
Запуск задач | **npm scripts**, **[husky](https://www.npmjs.com/package/husky)** – запуск тестов перед коммитом, **[lint-staged](https://www.npmjs.com/package/lint-staged)** – запуск тестов только для изменённых файлов, [npm-run-all](https://www.npmjs.com/package/npm-run-all) – управление запуском задач, [ts-node](https://www.npmjs.com/package/ts-node) – интерпретация TypeScript на лету
Список браузеров | **Необходимо указать в формате [Browserslist](https://github.com/browserslist/browserslist) в файле `.browserslistrc`** 


## Инфраструктура
| | |
--- | ---
_Категория_ | _Технология_
Репозиторий | **Arc-монорепозиторий [arc_vcs/frontend/](https://a.yandex-team.ru/arc_vcs/frontend/)**
CI/CD | **Trendbox CI**, [Ревью кода](https://github.yandex-team.ru/devexp/devexp), [Merge Queue](https://github.yandex-team.ru/search-interfaces/microservices/tree/master/services/merge-queue), [CI-проверки](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/docs/faq/checks.md), [static-uploader](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/static-uploader), [ya tool](https://wiki.yandex-team.ru/yatool/)
Деплой приложения | AppHost, Awacs, Deploy + [базовые Docker-образы](https://github.yandex-team.ru/toolbox?utf8=%E2%9C%93&q=dockerfiles-) (текущий `registry.yandex.net/toolbox/nodejs:12.18.1-bionic`)
Деплой статики | S3
Локальное окружение для разработки | [tunneler](https://wiki.yandex-team.ru/users/unikoid/tunneler/) и/или [magicdev](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/magicdev)
Удалённое окружение для разработки | QYP. [Инструкция 1](https://wiki.yandex-team.ru/users/dmitryman/how-to-run-turbo-qyp/), [инструкция 2](https://wiki.yandex-team.ru/lp-constructor/razrabotka-kl-na-servere/).
Технические логи и метрики | **[ErrorBooster](https://wiki.yandex-team.ru/error-booster/)**, **[RUM](https://wiki.yandex-team.ru/velocity/rum/)**
Мониторинг | [Yasm](https://wiki.yandex-team.ru/golovan/), [Juggler](https://wiki.yandex-team.ru/sm/juggler/introduction/), [Monitorado](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/monitorado). Всё, что можно настроить через monitorado, необходимо делать **только** через него.
Продуктовые логи и метрики | Яндекс.Метрика, [ClickDaemon](https://wiki.yandex-team.ru/logs/clickdaemon/)
Работа с переводами | [Tanker](https://wiki.yandex-team.ru/doc-and-loc/l10n/tools/tanker/)
