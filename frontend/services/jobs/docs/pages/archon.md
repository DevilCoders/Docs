# Archon и локальная разработка

Немного о `npm start`, `srcrwr` и портах.

```
archon kotik --graph testing.json --port 9999 --renderer-port 8888
```

Опция `--graph` - имя файла с графом (из директории `graphs`), с которым будет выполнен запрос. В момент запуска `npm start` локальный граф выгружается в `Horizon` с префиксом в виде никнейма пользователя. В случае `jobs`, например, `username-jobs_test`. В ссылку на `hamster` также подклеивается это имя графа:

```
https://hamster.yandex.ru/jobs?renderer_export=binary&renderer_render_on_export=1&graph=testing_koreil-jobs_test
```

Для `jobs` в конфиге `kotik`'а подключается специальная [мидлвара](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/jobs/.config/kotik/config.js#L34) - это нужно для того, чтобы делать `srcrwr` всего, кроме источника `RENDERER` Турбо-подграфа.

Чтобы протестировать работоспособность Турбо локально есть возможность использовать `hamster` и `srcrwr`. Для этого нужно запустить Турбо локально с помощью команды:
`env FREEZE_PATH=https://<yandexLogin>-1-<instance>.tunneler-si.yandex.ru TUNNELER_HOST=<instance>-tunnelerapi.tunneler-si.yandex-team.ru NODE_TLS_REJECT_UNAUTHORIZED=0 npm run start -- --kotik-public --kotik-verbose`.
Здесь `yandexLogin` – логин на стаффе, который используется для тунеллера; `instance` (например, `ws3`) – экземпляр тунеллера (в команде используется дважды `<instance>` для `FREEZE_PATH` & `TUNNELER_HOST`).
Чтобы понять какая подпись должна быть у твоего тунеллера нужно запустить турбу с помощью `env NODE_TLS_REJECT_UNAUTHORIZED=0 npm run start -- --kotik-public` и тогда в консоль будет выведено что-то на подобие `Tunnel is ready to use: https://danigorokhov-1-ws3.tunneler-si.yandex.ru`.
Далее, можно запустить саму команду, например она может выглядеть так:
`env FREEZE_PATH=https://danigorokhov-1-ws3.tunneler-si.yandex.ru TUNNELER_HOST=ws3-tunnelerapi.tunneler-si.yandex-team.ru NODE_TLS_REJECT_UNAUTHORIZED=0 npm run start -- --kotik-public --kotik-verbose`.
После этого нужно открыть свой тунеллер (опять запись вида `Tunnel is ready to use: https://danigorokhov-1-ws3.tunneler-si.yandex.ru`). И открыть любой stub.

![example](https://jing.yandex-team.ru/files/danigorokhov/Screen%20Shot%202021-08-14%20at%2019.10.25.png)

После открытия и загрузки стаба в консоли будет запись вида `[2021-08-14T19:10:53.267] [DEBUG] worker #1 (82488) - Resolved request "https://hamster.yandex.ru/turbo?renderer_export=binary&renderer_render_on_export=1&waitall=10000&srcrwr=TURBOPAGES_SUBGRAPH%3A%3A%3A10000&srcrwr=RENDERER%3Aposts%3A%2F%2Fdanigorokhov-47336-ws3.tunneler-si.yandex.ru%3A443%3A5000&text=test_news", reqid "1628957452536416-16388282304105536085-hxtdkz6b3lovb5u6-BAL-5408" [4133 ms]`. (она будет где-то в начале логов турбы, можно погрепать по `srcrwr`).
Отсюда нужно взять часть про `RENDERER`. В примере выше это `?srcrwr=RENDERER%3Aposts%3A%2F%2Fdanigorokhov-47336-ws3.tunneler-si.yandex.ru%3A443%3A5000`.
Затем открываем `https://hamster.yandex.ru/jobs` и дописываем `srcrwr`, но нужно поменять порт с `443` на `80` в конце `srcrwr`. В данном примере получится:
`https://hamster.yandex.ru/jobs?srcrwr=RENDERER%3Aposts%3A%2F%2Fdanigorokhov-47336-ws3.tunneler-si.yandex.ru%3A80%3A5000`.
ПС сначала может вылетать 503, но после нескольких обновлений начинает работать.

Опция `--port 9999` указывает, на каком порту будет локально поднят сервис.
Опция `--renderer-port 8888` указывает, на каком порту будет поднят локальный `report-renderer`.
Порт тунеллера меняется при каждом запуске, ждем https://st.yandex-team.ru/FEI-20149

![example](https://jing.yandex-team.ru/files/koreil/Снимок%20экрана%202021-01-20%20в%205.16.05%20PM.png)

### Как внести изменения в граф?

Для локальной разработки достаточно поправить граф [`testing.json`](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/jobs/graphs/testing.json). При следующем запуске команды `npm start` граф будет выгружен в Horizon с префиксом в виде вашего ника, затем, при условии, что граф валидный, раскатится по машинам и будет использоваться при локальном запуске.

Убедиться, что локально используется нужная версия графа, можно двумя способами:

1. Посмотреть логи `report-renderer`:

```
tail -f ~/.yandex-int/logs/rr/current-report-renderer_renderer-request-event-8888
```

2. Передать в запрос `cgi`-параметры `dump=eventlog&eventlog_format=html`

```
http://localhost:9999/jobs?dump=eventlog&eventlog_format=html
```

Под отрендеренной страницей появятся логи, в том числе строка с именем и версией графа. Например:

```
1611231558854192	0	TRunGraph	jobs@tags_apphost_conf_jobs_stable-4-1	["default"]
```

Чтобы выкатить граф в продакшн, необходимо закоммитить его в [Аркадию](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/JOBS/jobs.json), влить в `trunk`, а затем зарелизить его, [инструкция](https://wiki.yandex-team.ru/users/koreil/apphost/#kakpolzovatsjareliznojjmashinojj).

Тестировать влитый, но не зарелиженный граф можно, передавая параметр `graph=jobs@<revision>`.
Влитый в `trunk` граф с ревизией можно [найти в Horizon](https://horizon.z.yandex-team.ru/graphs?arcpath=trunk&vertical=JOBS).

### Как увидеть правки в локальных шаблонах на `hamster`?

Вы можете подменить бэкенд нужных вершин и перенаправить запрос в локальный `report-renderer` с помощью `cgi`-параметра `srcrwr`. Для этого вам нужно знать, на каком порту запущен ваш туннель. Например:

```
https://hamster.yandex.ru/jobs?srcrwr=ROUTER%3Aposts%3A%2F%2Fkoreil-10696-ws1.tunneler-si.yandex.ru%3A443%3A5000&srcrwr=TEMPLATES%3Aposts%3A%2F%2Fkoreil-10696-ws1.tunneler-si.yandex.ru%3A443%3A500&graph=testing_koreil-jobs_test
```
