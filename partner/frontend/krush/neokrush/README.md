## NeoKrush
Новая версия робота Krush, написанная на TypeScript

## Архитектура
Робот представляет из себя посредника между сервисами — модулями в папке `remote`, и интерфейсами — модулями в папке `interfaces`.
Например, в функционал Телеграмм бота (`src/interface/telegram`) входит работа с сервисом Sentry (`src/remote/sentry`). Бизнес логика этого функционала реализована в сервисном модуле телеграмм бота (`src/interface/telegram/service/sentry`).

## Как выложить новую версию Neokrush
1. Получить "пальцы" на пуллреквесте.
2. Замержить пуллреквест в мастер
3. Обновить локально мастер, сделать коммит с новой версией в package.json (сообщение "Neokrush Version X.Y.Z")
4. Собрать докер-образ с помощью команды npm run build
5. Запушить докер-образ с помощью команды npm run push
6. Обновить стейдж в Y.Deploy. На шаге 4 спек деплой-стейджа был обновлен тэгом нового
    образа neokrush, теперь весь стейдж нужно передеплоить. Перед этим крайне важно подтянуть
    свежий мастер, чтобы не перетереть тэг старого `krush`.
    Обновить стейдж можно утилитой [dctl](https://wiki.yandex-team.ru/deploy/docs/tools/dctl/?from=%2Fdeploy%2Fdocs%2Fscenarii-ispolzovanija-dctl%2F):
        `ya tool dctl put stage ../deploy/spec/krush.yaml` - если находимся внутри neokrush
        `ya tool dctl put stage deploy/spec/krush.yaml` - если находимся в корне проекта krush
    Альтернативно, можно просто зайти в [интерфейс деплоя](https://deploy.yandex-team.ru/stage/krush),
    открыть спек на редактирование и прописать вручную тэг образа, затем передеплоить стейдж.
7. Запушить все изменения (package.json, deploy/spec/krush.yaml) в мастер

## Если нужно залезть в logger ...
... не забудь:
1. Установить сертификат командой `npm run ca:init`. Справка по [сертификатам](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vnode.js).
2. Забрать пароль БД из [секретницы](https://yav.yandex-team.ru/secret/sec-01fk14j97bqr5s6xjaqwf270wp/explore/versions) и прописать его в env переменную `CH_PASSWORD`.
3. Настроить параметры БД в `config.json` в `src/remote/clickhouse/config.json`.
