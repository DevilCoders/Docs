# Школа разработки отдела Сергея Горобцова для **клиентских скриптов на JavaScript**

В эту школу попадают клиентские скрипты, для которых необходим полный контроль над итоговым размером кода в собранном бандле. 

Пример такого проекта – [загрузчик сервиса «Комментатор»](https://github.yandex-team.ru/cmnt/cmnt-loader/).

Для обсуждения присоединяйтесь к каналу   
**[#greyevil-school](https://yndx-all.slack.com/archives/C01FJ3RCDL5)** в Slack.

## Правила

- Следовать правилам необходимо всем новым проектам. 

- **Жирным** выделены технологии и инструменты, которые **должны** использоваться.

- Технологии и инструменты не перечисленные в рамках категории **не должны** использоваться.

- Для категорий, не указанных в правилах, ограничений нет.

## Технологии

| | |
--- | ---
_Категория_ | _Технология_
Язык программирования | JavaScript

## Инструменты

| | |
--- | ---
_Категория_ | _Технология_
Code style | **[@yandex-int/lint](https://a.yandex-team.ru/arc_vcs/frontend/packages/lint)**. Включает в себя конфигурацию для eslint, stylelint и prettier. **Правила нельзя смягчать, но можно расширять и делать строже**. 
Тесты | **[Jest](https://jestjs.io/)**, **[husky](https://www.npmjs.com/package/husky)** – запуск тестов перед коммитом, **[lint-staged](https://www.npmjs.com/package/lint-staged)** – запуск тестов только для изменённых файлов
Работа с зависимостями | **npm**, **[yadi-bin](https://wiki.yandex-team.ru/product-security/yadi/)**  – проверка на уязвимости, [patch-package](https://www.npmjs.com/package/patch-package) – накладывание патчей
Запуск задач | **npm scripts** , [dotenv-cli](https://www.npmjs.com/package/dotenv-cli) – подмешивание переменных окружения в команды, [npm-run-all](https://www.npmjs.com/package/npm-run-all) – управление запуском задач, [ts-node](https://www.npmjs.com/package/ts-node) – интерпретация TypeScript на лету

## Инфраструктура
| | |
--- | ---
_Категория_ | _Технология_
Репозиторий | **Arc-монорепозиторий [arc_vcs/frontend/](https://a.yandex-team.ru/arc_vcs/frontend/)**
CI/CD | **Trendbox CI**, [Ревью кода](https://github.yandex-team.ru/devexp/devexp), [Merge Queue](https://github.yandex-team.ru/search-interfaces/microservices/tree/master/services/merge-queue), [CI-проверки](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/docs/faq/checks.md), [static-uploader](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/static-uploader), [ya tool](https://wiki.yandex-team.ru/yatool/)
