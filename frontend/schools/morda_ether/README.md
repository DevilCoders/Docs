# Школа разработки фронтенда Морды

## Общая информация
Сервисы, разрабатываемые в проектах главной страницы. Изначально заточена на SSR.

## Технологии

| | |
--- | ---
Язык программирования | JS(ES5, ES6), TypeScript
CSS | Stylus
CSS-модули | нет
Клиентский фреймворк | i-bem, mini-bem, svelte (safari ntp, madm, web divkit)
Шаблонизация | Views
Дизайн система | Лего
Песочница компонентов | –
Работа с зависимостями | npm, bower
HTTP-фреймворк | AppHost+Node.js (Express)
Code style | @yandex-int/lint inspired
Использование кастомных шрифтов | Вариативный YS
Управление стейтом | нет 
Service Workers | часть страниц кэшируется (ntp Браузера, Хрома и т.п.) 

## Инструменты

| | |
--- | ---
Сборка | enb => Webpack
Unit-тесты | Mocha Jest
E2E тесты | [Hermione](https://github.com/gemini-testing/hermione) [Cypress](https://www.cypress.io/)
RUM-трекинг | [RUM](https://wiki.yandex-team.ru/velocity/rum/)
i18n | [Tanker](https://wiki.yandex-team.ru/doc-and-loc/l10n/tools/tanker/)
CMS | madm
Управление монорепозиторием | –


## Инфраструктура

| | |
 --- | ----
Флоу работы с репозиторием | feature branches
Система контроля версий | Arcadia
CI/CD | [trendbox-ci](https://wiki.yandex-team.ru/trendbox-ci/) + [tkit](https://a.yandex-team.ru/arcadia/maps/front/packages/tkit), Potato
Деплой | YP
Хостинг репозитория | Arcadia
Task runner | make + npm scripts
Dev | QYP
Сбор клиентских ошибок | [ErrorBooster](https://wiki.yandex-team.ru/error-booster/)
Логи | blockstat + redir, [logshatter](https://wiki.yandex-team.ru/market/development/health/logshatter/) 
Мониторинг | [Yasm](https://wiki.yandex-team.ru/golovan/)
Конфигурация | –
