# Goals proxy

Proxy сервер между фронтом и бекендом/трекером

## Костыли

Список, обоснование и шаги по выпиливанию [лежат здесь](./docs/CRUTCHES.md)

## Как развернуть локально

0. `nvm i` ([NVM][nvm]), либо окружение с nodejs v12. Да, используется более новая версия, чем во фронтенде голсов. Нужно запускать в разных вкладках с разными версиями nodejs. Хорошо работает через nvm
1. `npm i`.
2. Сформировать `.env`: запустить `env YAV_TOKEN=… npm run dotenv` (см. подробную инструкцию ниже)
3. `npm run dev`.
4. `npm start -- --endpoint=http://localhost:3000` из папки фронтенда голсов
5. Profit! Теперь ваш локальный фронт ходит через proxy

## Конфигурация

Конфигурация работает через .env файлы. Сначала применяется файл `.env`, потом один из файлов .dev.env/.testing.env/.test.env/.prod.env на основе переменной `NODE_ENV`. По умолчанию используется `NODE_ENV=development`

Итого, порядок такой: `переменные окружения` > `.env` > `.{NODE_ENV}.env`
Уровень ниже не перезатирает более верхний уровень

## Переменные окружения, определенные в .dev.env/.testing.env/.test.env/.prod.env

Это переменные, которые редко меняются (урлы других сервисов, название очереди и т.д.), поэтому они закоммичены в репозиторий

- `NODE_ENV`: определяет, какой конфиг по умолчанию нужно подключить. Возможные значения: `development`(по умолчанию), `testing`, `production`, `test` (ходит в тестинг через прокси clement)
- `YENV`: окружение, для которого запускается proxy. Необходимо для отправки метрик. При установке в `development` прокси начинает добавлять заголовок `X-Forwarded-For`, чтобы запросы корректно обрабатывались в blackbox
- `DISABLE_AUTH`: флаг отключения походов в blackbox и tvm. Включается значением `'1'`, корректно работает только с запущенным clement и `NODE_ENV=test`
- `GOALS_URL` - URL запущенного сервиса, нужен для построения правильных ссылок пагинации
- `TRACKER_URL`: URL API трекера, куда будут отправляться запросы из новых ручек
- `TRACKER_QUEUE`: Очередь в трекере, в которой хранятся тикеты-цели
- `TRACKER_ISSUE_IMPORTANCE_PRIVATE`, `TRACKER_ISSUE_IMPORTANCE_REGULAR`, `TRACKER_ISSUE_IMPORTANCE_DEPARTMENT`, `TRACKER_ISSUE_IMPORTANCE_COMPANY`, `TRACKER_ISSUE_IMPORTANCE_OKR` - ID значений для поля важности цели в трекере. Берется из ручки /v2/fields/goalImportance из TrackerAPI
- - `TRACKER_ISSUE_STATUS_NORMAL`, `TRACKER_ISSUE_STATUS_RISK`, `TRACKER_ISSUE_STATUS_BLOCKED`, `TRACKER_ISSUE_STATUS_CANCELED`, `TRACKER_ISSUE_STATUS_DONE`, `TRACKER_ISSUE_STATUS_NEW` - ID значений для поля важности цели в трекере. Можно получить из ручки https://st-api.yandex-team.ru/v2/queues/GOALSVAULTO/statuses/, подставив очередь из `TRACKER_QUEUE`
- `TRACKER_CONFIDENTIAL_COMPONENT` - ID компонента `is_confidential` в трекере, можно получить по ссылке https://st-api.yandex-team.ru/v2/queues/GOALSVAULTO/components, подставив очередь из `TRACKER_QUEUE`
- `TRACKER_GOAL_ISSUE_TYPE` - ID типа тикета "Цель", можно получить по ссылке https://st-api.yandex-team.ru/v2/queues/GOALSVAULTO/issuetypes/, подставив очередь из `TRACKER_QUEUE`
- `STAFF_URL` - урл StaffAPI
- `IDM_URL` - урл IDMAPI

## Переменные окружения, определяемые в окружении/.env файле

**Заполняются автоматически командой `env YAV_TOKEN='<OAUTH-токен>' npm run dotenv`**

Переменную окружения `YAV_TOKEN` можно получить [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982).
После запуска команды файл `.env` заполнится корректными значениями **для работы с тестингом**.

- `PORT` - порт, на котором запускается приложение. По умолчанию - `3000`
- `USE_ROBOT` - флаг для использования TrackerAPI с OAuth токеном робота вместо TVM2. Полезно при работе с продовым трекером во время разработки
- `TRACKER_ENABLE_NOTIFICATIONS` - флаг для включения отбивок от трекера об изменении тикетов. Включить, когда перейдем на трекерные уведомления вместо голсовых
- `TRACKER_TOKEN` - OAuth токен для подключения к TrackerAPI
- `STAFF_TOKEN` - OAuth токен для подключения к StaffAPI
- `IDM_TOKEN` - OAuth токен для подключения к IDM API
- `ABC_TOKEN` - OAuth токен для подключения к ABC API
- `TVM_TOKEN` - Токен для запуска tvm-tool
- `MONITORADO_OAUTH_TOKEN` - OAuth токен для актуализации мониторингов
- `READONLY` - включение режима readonly
- `DISABLE_YASM` - отключение логов про отсутствие Yasm сервера. Отключение используется для запуска скриптов, потому что для них мы не собираем метрики в yasm

## Заведение/обновление собственного стенда
0. Установить `ya tool` ([инструкция](https://wiki.yandex-team.ru/yatool/distrib/)). Внутри должен быть `releaser`
1. Добавить алиас для утилиты `ya`, чтобы к ней можно было обращаться без указания пути
2. Запустить `. ./scripts/update-stand` **из корня проекта**
3. Создается стенд `tools/goals/proxy-$USER`, где $USER - ваш логин

## Работы по графику

Рецепт успеха разработки скриптов «по крону»:
1. Создаем ветку с изменениями в скрипте.
1. Клонируем последнюю успешную sandbox-таску из [Scheduled runs](https://sandbox.yandex-team.ru/scheduler/25188).
1. Меняем в конфиге (trendbox_config) ветку при клонировании на свою (ищем `git clone ... --branch ...`).
1. Запускаем и смотрим результат. Повторить многократно до готовности.
1. Когда результат устраивает — вливаем PR в master.

### [sync-groups](./scripts/sync-groups)

Периодичность: [каждый час](https://sandbox.yandex-team.ru/scheduler/25188/tasks)

Синхронизация групп для пользователей из полей `assignee`, `customers`, `participants` в поля `groupTestArray` (Группы Исполнителя), `customerGroups`, `participantsGroups`, используя актуальные данные Стаффа.

Алгоритм:
- берем всех пользователей и их группы со стаффа, строим для каждого цепочку до корня, сортируем по id.
- берем живые тикеты с целями из трекера, ищем те, где группы не соотв. пользователям.
- группируем запросы по необходимым изменениям (по полям или по пользователям).
- дергаем ручки трекера, чтобы применить необходимые изменения.

### [users-cache](./bin/updateUsersGoalsCache.ts)

Периодичность: каждый час

Наполнение кеша целей в redis, сгруппированных по людям для
- отображения в блоке на staff
- отображения в таблице ресурсов

Таска запускает скрипт для тестинга и прода параллельно через пакет [npm-run-all](https://www.npmjs.com/package/npm-run-all)

Алгоритм:
- берем все открытые цели
- группируем их по людям
- выгружаем из redis все ключи
- обновляем те ключи, где есть данные
- удаляем ключи, по которым нет данных

Шедулер:
- https://sandbox.yandex-team.ru/scheduler/45100/view

## Сборка и выкатка релиза
0. Завести релизный тикет, прилинковать к нему все тикеты, которые катятся в прод.
1. Отвести ветку с релизом
2. Апнуть версию приложения `npm version minor`
3. Запустить `npm run release` (или `. ./scripts/release`, если yatool не работает через npm) для выкатки новой версии на тестинг и препрод. Подождать, пока версия выкатится ([тестинг](https://platform.yandex-team.ru/projects/tools/goals/testing), [препрод](https://platform.yandex-team.ru/projects/tools/goals/preprod))
4. Протестировать релиз
5. Если что-то пошло не так и нужны фиксы, то поле их влития в релизную ветку повторяем всё с шага 3 (новый образ соберется и раскатится под тем же тегом)
6. Запустить `npm run release:end` (или `. ./scripts/end-release`, если yatool не работает через npm) для выкатки новой версии в прод и эталонный тестинг. Подождать, пока версия выкатится ([эталонный тестинг](https://platform.yandex-team.ru/projects/tools/goals/goals-for-testing), [прод](https://platform.yandex-team.ru/projects/tools/goals/production))

### Swagger

Документация для всех ручек описывается в `JSDoc` для каждого метода.
Данные в запроса/ответах описываются через тайпинги.
Из последних генерируется JSON-schemas: `./scripts/generate-schemas`
Смотри ([документацию][annotations]) к аннотациям типов.
Сгенеренные схемы добавляются в компоненты `swagger.json`: `./scripts/compile-swagger`

[nvm]: https://github.com/nvm-sh/nvm
[annotations]: https://github.com/YousefED/typescript-json-schema#annotations

## Ссылки на разные версии:
- https://goals.test.yandex-team.ru - тестинг, релиз попадает в первую очередь сюда. Алиасы: https://goals-yd.test.yandex-team.ru. [Deploy](https://deploy.yandex-team.ru/stages/tools_goals_testing)
- https://master.goals.test.yandex-team.ru - мастер стенд, самая актуальная версия из master ветки голсов. Алиасы: https://master.goals-yd.test.yandex-team.ru. [Deploy](https://deploy.yandex-team.ru/stages/tools_goals_master)
- - https://assessors.goals.test.yandex-team.ru - стенд для тестирования асессорами. Выкатывается вместе с тестингом и препродом в процессе релиза
- https://pre.goals.yandex-team.ru - препрод, обновляется вместе с тестингом, смотрит в продовые данные, с статика из тестинга. Алиасы: https://pre.goals-yd.yandex-team.ru [Deploy](https://deploy.yandex-team.ru/stages/tools_goals_preprod)
- https://goals.yandex-team.ru - прод. Алиасы: https://goals-yd.yandex-team.ru. [Deploy](https://deploy.yandex-team.ru/stages/tools_goals_prod)
