# Школа разработки фронтенда Поисковых интерфейсов

## Общая информация
Используется для разработки web-интерфейсов конечных пользователей отдела разработки поисковых интерфейсов

## Технологии

| | |
--- | ---
Язык программирования | ES6, TypeScript
CSS | PostCSS
CSS-модули | нет
Клиентский фреймворк | React
Шаблонизация | React
Дизайн система | Лего
Песочница компонентов | Storybook
Работа с зависимостями | npm
Code style | [@yandex-int/lint](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/lint)
Использование кастомных шрифтов | да (Yandex Sans)
HTTP-фреймворк | [AppHost](https://wiki.yandex-team.ru/apphost/), [Kotik](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/kotik)
Управление стейтом | redux
Service Workers | да

## Инструменты

| | |
--- | ---
Сборка | webpack
Unit-тесты | jest + [Hermione](https://github.com/gemini-testing/hermione)
E2E тесты | [Hermione](https://github.com/gemini-testing/hermione)
RUM-трекинг | [RUM](https://wiki.yandex-team.ru/velocity/rum/)
i18n | @yandex-int/i18n
CMS | –
Управление монорепозиторием | [lerna-fork](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/projects/lerna), iver, hedwig, [depslint](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/depslint)


## Инфраструктура

| | |
 --- | ----
Флоу работы с репозиторием | monorepo, feature branches
Система контроля версий | git => [arc](https://arc-vcs.yandex-team.ru/docs/index.html)
CI/CD | [trendbox-ci](https://wiki.yandex-team.ru/trendbox-ci/)
Деплой | [Няня](https://wiki.yandex-team.ru/runtime-cloud/nanny/)
Хостинг репозитория | [Github](https://github.yandex-team.ru/search-interfaces/frontend) => [Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/frontend)
Task runner | npm scripts
Dev | локально, qyp
Сбор клиентских ошибок | [error-counter](https://github.yandex-team.ru/RUM/error-counter), [ErrorBooster](https://error.yandex-team.ru/projects/ydo/projectDashboard)
Логи | Baobab, ClickDaemon, Яндекс.Метрика
Мониторинг | [Yasm](https://wiki.yandex-team.ru/golovan/), [Juggler](https://wiki.yandex-team.ru/sm/juggler/)
Конфигурация | –