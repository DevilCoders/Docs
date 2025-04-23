# Школа разработки фронтенда Маркета

## Общая информация
Используется для разработки web-интерфейсов конечных пользователей в Яндекс.Маркете.

## Технологии

| | |
--- | ---
Язык программирования | Flow => TypeScript
CSS | Stylus => PostCSS
CSS-модули | есть
Клиентский фреймворк | React
Шаблонизация | yate => React
Дизайн система | \[разные\] => [Levitan](https://wiki.yandex-team.ru/market/levitan/)
Песочница компонентов | [Levitan](https://levitan.yandex-team.ru/)
Работа с зависимостями | npm + [veendor](https://github.com/mutantcornholio/veendor)
HTTP-фреймворк | [Stout](https://github.yandex-team.ru/market/stout) + [Apiary](https://github.yandex-team.ru/market/apiary)
Code style | [Market CodeStyle](https://github.yandex-team.ru/market/codestyle)
Использование кастомных шрифтов | Разные способы использования кастомных шрифтов => мордячий подход / отказ от кастомных шрифтов
Управление стейтом | Redux
Service Workers | –

## Инструменты

| | |
--- | ---
Сборка | enb => Webpack
Unit-тесты | Jest
E2E тесты | [Hermione](https://github.com/gemini-testing/hermione) + [Ginny](https://github.yandex-team.ru/market/ginny)
RUM-трекинг | что-то своё => [RUM](https://wiki.yandex-team.ru/velocity/rum/)
i18n | [Tanker](https://wiki.yandex-team.ru/doc-and-loc/l10n/tools/tanker/)
CMS | [Бункер](https://wiki.yandex-team.ru/verstka/tools/bunker/), [Market CMS](https://wiki.yandex-team.ru/market/cms/)
Управление монорепозиторием | –


## Инфраструктура

| | |
 --- | ----
Флоу работы с репозиторием | feature branches => green trunk => monorepo
Система контроля версий | git => [arc](https://arc-vcs.yandex-team.ru/docs/index.html)
CI/CD | [sandbox-ci](https://wiki.yandex-team.ru/sandbox/), [ЦУМ](https://tsum.yandex-team.ru/)
Деплой | [Няня](https://wiki.yandex-team.ru/runtime-cloud/nanny/)
Хостинг репозитория | github.yandex-team.ru => [Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia)
Task runner | npm scripts + make
Dev | выделенные железные машины
Сбор клиентских ошибок | [ErrorBooster](https://wiki.yandex-team.ru/error-booster/)
Логи | [logshatter](https://wiki.yandex-team.ru/market/development/health/logshatter/) + [clickphite](https://wiki.yandex-team.ru/market/development/health/clickphite/)
Мониторинг | [Grafana](https://wiki.yandex-team.ru/sm/grafana/), [Yasm](https://wiki.yandex-team.ru/golovan/)
Конфигурация | –
