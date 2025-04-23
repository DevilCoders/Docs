# DX-метрики/телеметрия

Все метрики, связанные с процессом разработки, логируются с помощью [metric-logger](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/dx-metrics-logger/Readme.md).
Некоторые метрики пишутся в ClickHouse-кластер, некоторые пишутся только в консоль для отладки

- [Метрики, отправляемые в CH](#Метрики-отправляемые-в-CH)
- [Метрики для отладки](#Метрики-для-отладки)

Графики, построенные на основе собранных метрик, собраны на [дашборде](https://datalens.yandex-team.ru/pgqonf4vsc2km-metriki-sborki-web4)

## Метрики, отправляемые в CH

Метрики отправляются по http в [arch-dx-handler](https://a.yandex-team.ru/arc_vcs/frontend/projects/microservices/services/webhook-handler/modules/metrics-logger/handlers.js) сервиса web-хуков Инфраструктуры, которая пишет данные в таблицу [fei_infra/arch_build_time](https://yql.yandex-team.ru/?cluster=fei_infra&path=cluster%2Fstats%2Farch_build_time&table_mode=scheme)

#### Основные метрики

- `install-deps` — установка зависимостей
- линтеры
    - `lint/all`
    - `lint/typechecking`
- сборка
    - `build-project/{mode}/{platform}` — полная сборка
    - `build-bem/{mode}/{platform}` — сборка старого стека
    - `webpack/{mode}` — сборка нового стека
- unit-тесты
    - `priv-test/{mode}/{platform}` — сборка и выполнение priv-тестов
    - `commonjs-test/{mode}/{platform}` — выполнение cjs-тестов (не требующих сборки)

параметры основных метрик:
- `{mode}` — режим запуска: "development", "testing" (в PR) или "production" (в релизе)
- `{platform}` — платформа: "desktop" или "touch-phone"

#### Метрики dev-сервера

- `tti-first` и `tti` — время между отправкой запроса в dev-сервер и завершением последнего [js-long-task](https://developer.mozilla.org/en-US/docs/Web/API/Long_Tasks_API)-а при инициализации страницы. Метрика "tti-first" отправляется для самого первого запроса после старта dev-сервера, метрика "tti" отправляется для всех последующих запросов
- `webpack-watch-builder:startup` — время от инициализации [middleware](../.config/kotik/middlewares/webpack-watch-builder.js)-ы и до запуска watcher-а
- `webpack-watch-builder` — время селективной пересборки статики нового стека (между хуками *beforeCompile* и *afterCompile*)

#### Дополнительное

Кроме самого значения метрики логируется дополнительная информация:
- имя пользователя
- окружение: `process.platform`, число CPU-ядер, объем RAM, система контроля версий (git/arc) и тип машины (qyp/local)
- имя текущей ветки и коммит

Для запусков из-под Sandbox-задачи действуют специальные правила формирования некоторых полей:
- имя пользователя "sandbox"
- имя ветки "pull-{num}" или "mq"
- коммит содержит URL на Sandbox-задачу

## Метрики для отладки

Для отладки или разборка замедлений можно включить дополнительное логирование — через переменную окружения `DX_DEBUG=1`

Отладочные метрики:

- `kotik:first-request:*` и `kotik:request:*` — метрики работы plugin/middleware внутри kotik-а. Отдельно лигируются метрики для самого первого и последующих запросов после старта dev-сервера
    - `rebuild-static` — automake-пересборка и watch-builder-пересборка старого стека
    - `soft-restart` — переподключение серверных шаблонов в kotik (с полным сбросом nodejs-кешей)
    - `templar-proxy` (или `templarProxy`) — plugin/middleware, вызываемые из-под templar-а
- сборка старого стека
    - `build-bemdecls` — раскрытие `.bemdecl.js`-файлов
    - `build-bundle-static` — сборка статики обычных бандлов
    - `build-exp-bundles` — сборка экспериментальных бандлов
    - `build-additional-exp-bundles` — сборка дополнительных экспериментальных бандлов
    - `build-page-static` — сборка статики страницы
