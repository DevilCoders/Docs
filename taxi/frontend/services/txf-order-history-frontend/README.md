# Фронтенд истории заказов

|                                                                                                                                                    Last pre-release                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                        Last unstable |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_FrontendMonorepo_Stable,branch:txf-order-history-frontend/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_FrontendMonorepo_Stable&branch=txf-order-history-frontend) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_Infranaim_Frontend_NewFlowTest,branch:txf-order-history-frontend/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Infranaim_Frontend_NewFlowTest&branch=txf-order-history-frontend) |

[Сервис в админке](https://tariff-editor.taxi.yandex-team.ru/services/43/edit/355058/info)
[Информация на wiki](https://wiki.yandex-team.ru/taxi/frontend/orderhistory/)

## Хосты

### С авторизацией через OAuth + X-YaTaxi-UserId

| env        | host                                          |
| ---------- | --------------------------------------------- |
| testing    | https://m.taxi.taxi.tst.yandex.ru/webview/history |
| production | https://m.taxi.yandex.ru/webview/history      |

### С авторизацией через YA AUTH PROXY

Для авторизации используется портальная кука Session_id + X-YaTaxi-UserId + ?id=<user_id>

| env        | host                                                            | Правило проксирования                                                                                              |
| ---------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| testing    | https://ya-authproxy.taxi.tst.yandex.ru/webview/yaproxy/history | [Ссылка](https://tariff-editor.taxi.tst.yandex-team.ru/authproxies/ya-authproxy/show/L3dlYnZpZXcveWFwcm94eQ%3D%3D) |
| production | https://ya-authproxy.taxi.yandex.ru/webview/yaproxy/history     | [Ссылка](https://tariff-editor.taxi.yandex-team.ru/authproxies/ya-authproxy/show/L3dlYnZpZXcveWFwcm94eQ%3D%3D)     |

### У сервиса есть прямые хосты (не рекомендуется использовать для тестирования)

Авторизация OAuth + X-YaTaxi-UserId

| service | env        | host                                                                     |
| ------- | ---------- | ------------------------------------------------------------------------ |
| yandex  | testing    | http://order-history-frontend-yandex.taxi.tst.yandex.net/webview/history |
| uber    | testing    | http://order-history-frontend-uber.taxi.tst.yandex.net/webview/history   |
| yango   | testing    | http://order-history-frontend-yango.taxi.tst.yandex.net/webview/history  |
| vezet   | testing    | http://order-history-frontend-vezet.taxi.tst.yandex.net/webview/history  |
| yandex  | production | http://order-history-frontend-yandex.taxi.yandex.net/webview/history     |
| uber    | production | http://order-history-frontend-uber.taxi.yandex.net/webview/history       |
| yango   | production | http://order-history-frontend-yango.taxi.yandex.net/webview/history      |
| vezet   | production | http://order-history-frontend-vezet.taxi.yandex.net/webview/history      |

## Логи

| service | testing                                                                                                                                                                                                                                                                      | production                                                                                                                                                                                                                                                                                       | клиентские                                                                                    |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| yandex  | [testing](<https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=()&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxi-txf-order-history-frontend-yandex'),sort:!(!('@timestamp',desc)))>) | [production](<https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(filters:!())&_a=(columns:!(_source),filters:!(),index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,interval:auto,query:(language:kuery,query:'name:%20taxi-txf-order-history-frontend-yandex'),sort:!(!('@timestamp',desc)))>) | [error](https://error.yandex-team.ru/projects/order-history-frontend.yandex/projectDashboard) |
| uber    | [testing](<https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=()&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxi-txf-order-history-frontend-uber'),sort:!(!('@timestamp',desc)))>)   | [production](<https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(filters:!())&_a=(columns:!(_source),filters:!(),index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,interval:auto,query:(language:kuery,query:'name:%20taxi-txf-order-history-frontend-uber'),sort:!(!('@timestamp',desc)))>)   | [error](https://error.yandex-team.ru/projects/order-history-frontend.uber/projectDashboard)   |
| yango   | [testing](<https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=()&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxi-txf-order-history-frontend-yango'),sort:!(!('@timestamp',desc)))>)  | [production](<https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(filters:!())&_a=(columns:!(_source),filters:!(),index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,interval:auto,query:(language:kuery,query:'name:%20taxi-txf-order-history-frontend-yango'),sort:!(!('@timestamp',desc)))>)  | [error](https://error.yandex-team.ru/projects/order-history-frontend.yango/projectDashboard)  |
| vezet   | [testing](<https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=()&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxi-txf-order-history-frontend-vezet'),sort:!(!('@timestamp',desc)))>)  | [production](<https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(filters:!())&_a=(columns:!(_source),filters:!(),index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,interval:auto,query:(language:kuery,query:'name:%20taxi-txf-order-history-frontend-vezet'),sort:!(!('@timestamp',desc)))>)  | [error](https://error.yandex-team.ru/projects/order-history-frontend.vezet/projectDashboard)  |

## Дашборды uptime

- [server uptime](https://monitoring.yandex-team.ru/projects/taxi/dashboards/monmf8u65r9be8gckukj?range=1d&refresh=60)
- [client uptime](https://static.twin.front.taxi.dev.yandex-team.ru)

## GET параметры сервиса

- `id` | `userId` - id пользователя такси
- `services` - список необходимых сервисов через запятую. ?service=taxi,grocery,drive. Весь [список здесь](https://github.yandex-team.ru/taxi/frontend-monorepo/blob/master/services/txf-order-history-frontend/src/core/constants.ts#L3)
- `disableRemove` - отключить кнопку удаление поездок
- `hideсontrols` - скрыть контролы "службы поддержки", "звонок водителю", "возврата товара"

## Установка и разработка

Нужно пойти в секретницу и скачать [.tvm-<service>.json](https://yav.yandex-team.ru/edit/secret/sec-01em1n08qkksbybh8rmwxbv30a/explore/versions) и положить в домашнюю папку под именем `.tvm-<service>.json` (например, `.tvm-yandex.json`), зависит какой сервис будете запускать.

Если используем nvm, то выбираем версию nodejs. Можно выставлять автоматически [подробнее](https://github.com/nvm-sh/nvm#deeper-shell-integration).

```
nvm use
```

> Иначе зайти в .nvmrc и установить в ручную

```
npm ci
npm start
```

Сервис доступен по http://localhost:4001/webview/history

## Локализация

Вся локализация Истории заказов реализована через Танкер [(инструкция)](./.tanker/README.md) 

## Сборка

```
npm run build
```

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Разное

[Расширение для подмены заголовков](https://chrome.google.com/webstore/detail/modheader/idgpnmonknjnojddfkpgkljpfnnfcklj?hl=ru)
