## Логи node.js
Логи лежат тут
```/var/log/node-init-cluster/<app>/<logfile>.log```

```debug.log``` <- console.log

```error.log``` <- console.error (в деве для удобства все пишется в один файл `debug.log`)

```access.log``` лог всех входящих (пользовательских) и исходящих (в бекенды) запросов. Машиночитаемый формат, похожий на nginx access.log. Все запросы можно склеить по x-request-id.

Формат: `{.time} {.requestId} {.appId}[{.method}] {.code} {.timers.total} {.url} {.headers} {.body}`

Все логи заливаются на ```logs.vertis.yandex.net:/var/remote-log/nodejs-*```. Например:
```
ssh logs.vertis.yandex.net
tail -f /var/remote-log/nodejs-02-sas.prod.vertis.yandex.net/node-init-cluster/autoru-frontend-desktop/error.log
```

## Клиентские ошибки

Есть общеяндексовый сервис [Error Booster](https://error.yandex-team.ru/projects/auto_ru/projectDashboard).
Туда отправляются все ошибки с `window.onerror` и ошибки, отправленные явно.


## Графики

Фронтовый дашборд https://grafana.vertis.yandex-team.ru/d/000000595/autoru-nodejs-frontends

## Логи других сервисов

В дев-окружении логи public Api и VOS лежат на машине ``team-java-01-sas.dev.vertis.yandex.net`` (актуальный адрес смотрите в датасорцах).

**Public Api**

/var/log/autoru/api-server.log

/var/log/autoru/api-server-http-access.log


**VOS**

/var/log/vos2/vos2-autoru-api.log

/var/log/vos2/vos2-autoru-api-http-access.log
