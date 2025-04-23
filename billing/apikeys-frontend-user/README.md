[![oko health](https://badger.yandex-team.ru/oko/repo/data-ui/core/health.svg)](https://oko.yandex-team.ru/repo/data-ui/core)

## TODO
**Static**
1. Обновить react-scripts
2. Перенести разбор сфетченных данных с клиента в Ноду
3. Актуализировать все это, в связи с миграцией в аркадию (МОГУТ БЫТЬ НЕТОЧНОСТИ!!!)

## Документация
https://wiki.yandex-team.ru/billing/apikeys/dev/ui/newstaff/description/

## Структура проекта
```
debian/                 Конфигурация дебианизации проекта
server/                 Серверная часть проекта
  configs/              Конфигурационные файлы для разных окружений
  controllers/          Контроллеры для страниц
  lib/                  Утилиты
  middleware/           Промежуточной обработки Express
  run/                  Нужно для контенера (см. docker-apikeys)
  index.js              Recluster
  server.js             Инстанс сервера
  app.js                Express-application
  router.js             Привязка контроллеров к url'ам
static/                 Статика и верстка
www/                    Дополнительные файлы статики
```

## Тестирование
https://wiki.yandex-team.ru/billing/apikeys/dev/ui/testing/description/

## Как запустить
Вместо npm используется yarn. Для начала нужно настроить себе registry: yarn config set registry http://npm.yandex-team.ru/

1. Клонировать аркадию и открыть папку с проектом
2. Поднять контейнер на dev-сервере (см. документацию, ОСТОРОЖНО, частичная утрата актуальности после миграции в аркадию)
3. Выполнить в терминале на своём компе команду:
    ```
    yarn start
    ```
    Эта команда запускает синхронизацию файлов проекта на компе и в папке на dev-сервере, в которую смотрит Docker.
4. Открыть http://%my-user-name%-user-front.apikeys-dev.paysys.yandex.ru и можно работать.


## Особенности разработки
На dev-сервере установлен supervisor. С его помощью можно перезапускать node.js, webpack-dev-server etc.
Для запуска supervisorctl нужно зайти в контейнер и выполнить команду:
```
sv
```

Локализация выкачивается из Танкера https://tanker.yandex-team.ru/?project=apikeys&branch=master каждый раз при запуске контейнера и при сборке на тестинг.
Если нужно обновить локализации в процессе работы, нужно выполнить в контенере команду:
```
yarn i18n
```
После этого перезапустить webpack-dev-server через supervisor:
```
sv
restart webpack-dev-server
```

Некоторые файлы (иконки, манифесты) не обновляются от версии к версии.
Они переименовываются (md5 hash) и все хранятся в
http://yandex.st/yandex-balance-apikeys-frontend-user/_/
Оттуда они отдаются с загловками "никогда больше не запрашивать".
На yandex.st их заливет ycssjs-freeze-keeper. Подробнее:
https://wiki.yandex-team.ru/verstka/tools/ycssjs/#zamorozkakartinok
https://wiki.yandex-team.ru/verstka/tools/ycssjs-freeze-keeper/
Чтобы узнать, с каким именем зальются файлы, в контейнере нужно выполнить команду:
```
make print-freeze-names
```
Эта команда так же выполняется при запуске контейнера.

## Workflow
Основая ветка trunk.

Для разработки нужно создать новую верку от trunk. Ветку назвать "APIKEYS-0000-какая-то-метка-для-себя" где "APIKEYS-0000" – это номер задачи из Стартрека.
"APIKEYS-0000" нужно в названии ветки обязательно потому при сборке релизного тикета что все найденные "APIKEYS-0000" из названий смерженных веток автоматически добавляются в описание тикета.

Изменения тестируются в dev-контейнере.

Обновить ./debian/changelog, для этого в корне проекта запускаешь `make changelog`.
Копируешь и в ставляешь вывод в начало файла и перечисляешь коммиты (либо оставляешь все без изменений если нужно обновить переводы из танкера)

После завершения работы ветка мержится в trunk через пулл-реквест.

## Релиз
После мержа в trunk, все выкатывается на тестинг:
https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Billing_Apikeys_FrontendUser_TestingDocker

После того, как релиз раскатится на тестинг и будет протестирован, создаётся релизный тикет:
https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Billing_Apikeys_FrontendUser_CreateReleaseTicket

После одобрения релиза нужно зайти в timeline и запустить релиз (в случае неожиданностей обратиться дежурному fintools).

## Ручки бекенда
https://wiki.yandex-team.ru/tech/developer/API-Klientskogo-interfejjsa-v.2/

## Debian
Релиз выезжает в виде debian-пакета. Подробнее:
https://wiki.yandex-team.ru/verstka/methods/debianize

## Sentry
Прод: https://sentry.t.yandex-team.ru/billing

Тест: https://sentry-test.t.yandex-team.ru/billing

## Разное
API Центра документации: https://wiki.yandex-team.ru/techdoc/doc-platform/doccenter/api/?from=%252Ftechdoc%252Fapi%252F

