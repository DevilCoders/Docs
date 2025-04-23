# Yandex Travel UI

Единый портал Яндекс Путешествий.

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=travel/frontend/rooms&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/rooms)
[![oko vulnerabilities](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=travel/frontend/rooms&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/rooms)

<!-- toc -->

- [Чаты, боты и рассылки](#%D1%87%D0%B0%D1%82%D1%8B-%D0%B1%D0%BE%D1%82%D1%8B-%D0%B8-%D1%80%D0%B0%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B8)
  * [Чаты в Telegram](#%D1%87%D0%B0%D1%82%D1%8B-%D0%B2-telegram)
  * [Каналы в Slack](#%D0%BA%D0%B0%D0%BD%D0%B0%D0%BB%D1%8B-%D0%B2-slack)
  * [Полезные боты](#%D0%BF%D0%BE%D0%BB%D0%B5%D0%B7%D0%BD%D1%8B%D0%B5-%D0%B1%D0%BE%D1%82%D1%8B)
- [Документация](#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8F)
  * [Старт](#%D1%81%D1%82%D0%B0%D1%80%D1%82)
  * [Подходы к разработке](#%D0%BF%D0%BE%D0%B4%D1%85%D0%BE%D0%B4%D1%8B-%D0%BA-%D1%80%D0%B0%D0%B7%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B5)
  * [Процессы](#%D0%BF%D1%80%D0%BE%D1%86%D0%B5%D1%81%D1%81%D1%8B)
  * [Инструменты](#%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B)
  * [Инструкции](#%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%86%D0%B8%D0%B8)
  * [Проектная документация](#%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%BD%D0%B0%D1%8F-%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8F)
- [Быстрые ссылки](#%D0%B1%D1%8B%D1%81%D1%82%D1%80%D1%8B%D0%B5-%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B8)

<!-- tocstop -->

## Чаты, боты и рассылки

### Чаты в Telegram

-   [Travel Front Dev](https://t.me/joinchat/CwgtDBgyudPINcCaq1VbLw) **private** - чат для вопросов разработки
-   [Travel Front Testing](https://t.me/joinchat/CwgtDFBKPuu25EF0UWzfLg) **public**, **Tasha** - чат для вопросов тестирования
-   [Travel Front Alerts](https://t.me/joinchat/AEKtx1I4lg5eg2MfQeEIXQ) **public**, **Tasha** - чат для мониторингов
-   [Travel Front Duty](https://t.me/joinchat/CwgtDFN7gfPrzLyGBlK9Eg) **private** - чат для вопросов дежурства, для статусов релизов

### Каналы в Slack

Слак активно используется для решения рабочих вопросов - Workspace `yndx-travel.slack.com`.

А вот каналы, которые будут в первую очередь полезны:

-   `meeting-minutes` - резюме встреч, в том числе с другими командами
-   `frontend` - вопросы к нашей команде от коллег
-   `design-front` - вопросы к дизайнерам
-   `backend` - вопросы к команде бэкенда
-   `proj-*` - общение по ведущимся проектам

### Полезные боты

-   [codereview_bot](https://t.me/codereview_bot) - бот, которые напоминает о ревью
-   [travel_release_bot](https://t.me/travel_release_bot) - бот пишет о результате тестирования задач (протестировано/есть замечания)

## Документация

### Старт

-   [Запуск проекта](docs/start.md)
-   [Workflow](docs/workflow.md)

### Подходы к разработке

-   [Защита от CSRF](docs/csrf-token-how-to.md)
-   [Архитектура сервера](docs/server-api-architecture.md)
-   [Взаимодействие с бэкендом](docs/backend.md)
-   [Переводы](docs/translations.md)
-   [Синхронизация иконок с Travel.Styles](docs/icons.md)
-   [Наименование и расположение файлов](docs/naming-and-structuring.md)
-   [Асинхронные редюсеры](docs/loadableReducers/loadableReducers.md)
-   [Временные и постоянные редиректы](docs/redirects.md)
-   [Автотестирование](docs/tests.md)
-   [Эксперименты и Feature Toggle](docs/experiments.md)

### Процессы

-   [Оценка задач](docs/story-points.md)
-   [Дежурства по релизам](docs/release-duty.md)
-   [Мониторинги и логи](docs/logs-and-monitoring.md)
-   [Работа с дизайном](docs/design.md)

### Инструменты

-   [Ферма](docs/farm.md)
-   [CrowdTestProxy](docs/crowd-test-proxy.md)
-   [Управление статикой](<docs/static%20(mds%20s3).md>)
-   [Управление контентом](docs/bunker/bunker.md)
-   [Учет размера бандлов](docs/bundle-size-statistics.md)
-   [Телеметрия](docs/telemetry.md)
-   [AdFox](docs/ads/adfox.md)
-   [Lighthouse](docs/lighthouse.md)

### Инструкции

-   [Debug дев-сервера](docs/debug.md)
-   [Симулятор iOS](docs/ios-simulator.md)

### Проектная документация

-   [Проектная документация](docs/project.md)

## Быстрые ссылки

-   [Доска с проектами](https://miro.com/app/board/o9J_kjSn_vs=/)

-   [Доска спринтов](https://st.yandex-team.ru/agile/board/5007)

-   [Про процессы, про проекты](https://wiki.yandex-team.ru/users/sirinity13/travelfrontend)

-   [UI Sync Wiki](https://wiki.yandex-team.ru/users/sirinity13/travelfrontend/ui-sync) - набросы перед UI синками
-   [Design Sync Wiki](https://wiki.yandex-team.ru/users/sirinity13/travelfrontend/design-sync/) - набросы перед Design синками
