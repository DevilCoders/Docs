# Школа разработки фронтенда Self-Driving Cars

## Общая информация

Описывает технологии и процессы, которые применяются при разработке Web-интерфейсов в [службе визуализации и веб-проектов SDC](https://staff.yandex-team.ru/departments/yandex_rkub_taxi_selfdriven_tech_1850_dep08764/).

## Технологии

| Параметр               |         Значение         |
| ---------------------- | :----------------------: |
| Язык программирования  | JavaScript => TypeScript |
| CSS                    |           SCSS           |
| CSS-модули             |           Есть           |
| Клиентский фреймворк   |          React           |
| Управление состоянием  |          Redux           |
| Песочница компонентов  |        Storybook         |
| Серверный фреймворк    |         Express          |
| Сборка                 | Webpack => React Scripts |
| Unit-тесты             |           Jest           |
| React-тесты            |  React Testing Library   |
| E2E-тесты              |            -             |
| i18n                   |      React i18next       |
| Работа с зависимостями |           NPM            |
| Code style             |  @yandex-sdc/codestyle   |

[@yandex-sdc/codestyle](https://bb.yandex-team.ru/projects/SDC/repos/www/browse/packages/codestyle) – мета-пакет с ESLint, Stylelint, Prettier и конфигурационными файлами для этих утилит.

## Инфраструктура

| Параметр                    |                Значение                |
| --------------------------- | :------------------------------------: |
| Процесс разработки          | Локально на macOS и десктопах с Ubuntu |
| Хостинг репозитория         |               Bitbucket                |
| Система контроля версий     |                  Git                   |
| Управление монорепозиторием |                 Lerna                  |
| Флоу работы с репозиторием  |            Feature branches            |
| Деплой                      |            Qloud => YDeploy            |
| CI/CD                       |                TeamCity                |
| Task runner                 |           NPM Scripts + Make           |
| Сбор клиентских ошибок      |             Error Booster              |
| Серверное логирование       |             Yandex Logger              |
| Конфигурация                |             Yandex Config              |
| Мониторинг                  |            Голован, Juggler            |
