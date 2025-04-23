# Yandex Balance Check Renderer

## Требования
* node v7.8.0+
* npm 4.2.0+

## Сборка
Можно собрать рендерелку в докере и запустить локально. Так же можно раскатить локально собранный образ в Deploy на тестинг и на прод (последнее крайне не рекомендуется).

Для того, чтобы собрать локально вам нужно придумать версию `your_version` которая послужит в качестве тега для собранного образа.

Собираем образ:
```
make -f deploy/Makefile build version=your_version
```

Запускаем образ локально:
```
docker run --env ENV_TYPE=testing --env TVM_SECRET=your_secret -p 18019:18019 check-renderer:your_version bash -c '/opt/main-setup.sh && node /check-renderer/bin/www --port 18019 --envType "${ENV_TYPE}"'
```

Раскатываем на тест:
```
make -f deploy/Makefile deploy_testing version=your_version
```

**Важно заметить**, что базовый образ зафиксирован в образе check-renderer-base. Если вы поменяли какие-либо зависимости, то его нужно пересобрать и запушить с новой версией:
```
make -f deploy/Makefile push_base version=new_version
```
После чего переключить версию в deploy/Dockerfile

## Формат данных на вход
Принимается только POST-запрос (Content-Type: application/json)

https://wiki.yandex-team.ru/billing/balance/dev/ui/ofd/format/

## Среды
- Тест: https://greed-ts.paysys.yandex.net:8019/ или https://greed-tm.paysys.yandex.net:8019/
  По GET-запросу выдает пример чека. На проде по GET-запросу будет - 404, принимаются только POST.
- Прод: https://check-back.paysys.yandex.net:8019/

## Адреса форматов чека
- / - обычная HTML версия
- /mobile - адаптированная под мобильные устройства HTML версия
- /mobile/mult - адаптированная под мобильные устройства HTML версия, на вход принимает массив объектов указанного выше формата: `[{...}, {...}, ...]`
- /pdf - PDF

## Мониторинг
См. по [ссылке](https://grafana.yandex-team.ru/dashboard/db/check-renderer?refresh=30s&orgId=1&panelId=3&fullscreen&from=now-3h&to=now)

## Перезапуск сервиса
`sudo service yb-ofd-check-renderer restart`

## Локальная разработка
- **nodejs web server**: 

`yarn web-server`

url https://local-check.yandex.ru:3030/test

Сертификаты могут устареть, нужно будет обновить скриптом из https://github.yandex-team.ru/Billing/dev-tools/tree/master/cert

- **webpack dev server**:

`yarn dev-server`

url: https://local.check.yandex.ru:9000/. 

Сначала может выдать ошибку, т.к. статика могла еще не собраться на момент открытия. Нужно будет перезагрузить страницу.

> Нужно добавить `local.check.yandex.ru` в `/etc/hosts`!

Для одновременного запуска nodejs-сервера и webpack-dev-сервера просто выполнить 

`yarn start`

> См. другие команды в `package.json` для отладки и тестирования.

## Мониторинг

Мониторинг производится путем периодического пуша в агент соломона, который ожидается локально, по адресу http://localhost:10050/balance-back/check-renderer. Если агент не запущен локально на машине разработчика, то к сбою приложения это не приводит.
