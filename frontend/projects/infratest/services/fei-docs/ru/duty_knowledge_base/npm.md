# NPM

В этом разделе приведены ответы на вопросы, связанные с внутренним устройством npm и дежурством.

Набор полезных скриптов для дежурного лежит в пакете [npm-duty-cli-tools](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/npm-duty-cli-tools).

## Где всё развёрнуто?

- Продакшен окружение
  - [Deploy](https://deploy.yandex-team.ru/projects/verdaccio)
  - [Балансер](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/verdaccio.yandex.net/show/)
  - [PostreSQL](https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-postgresql/cluster/mdbv5pmjds3hv086op7j)
- Тестовое окружение
  - [Deploy](https://deploy.yandex-team.ru/stage/npm-test-stage)
  - [Балансер тестового окружения](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/npm-testing.in.yandex-team.ru/show/)
  - [PostreSQL](https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-postgresql/cluster/mdb0isjuimpbej99rtte)

## Где смотреть метрики?

- [Дашборд мониторингов в juggler](https://juggler.yandex-team.ru/dashboards/760a758b)
- [Панель с внутренними метриками NPM](https://yasm.yandex-team.ru/panel/frimuchkov._oJfpYc/)
- [Шаблонизированная панель с внутренними метриками NPM](https://yasm.yandex-team.ru/template/panel/npm-dashboard-for-host/)
- [Панель с метриками L7 балансеров](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=verdaccio.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=verdaccio.yandex.net;signal=service_total/)
- [Панель с метриками s3 бакета verdaccio](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=verdaccio;owner=1405)
- [Метрики PostgreSQL](https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-postgresql/cluster/mdbv5pmjds3hv086op7j?section=monitoring)

## Как выкатить новую версию в прод?

1. Влить ревью-реквест в транк
2. После влития автоматика собирает докер-образ и загружает его на [тестинг](https://deploy.yandex-team.ru/stage/npm-test-stage)
3. Smoke-тесты необходимо прогнать руками [по инструкции](#tests)
4. После этого нужно скопировать последнюю версию докер-образа из [тестинга](https://deploy.yandex-team.ru/stages/npm-test-stage/config/du-verdaccio_man/box-verdaccio#resources) (строка вида `yandex-trunk-2021.10.18-16.53.02`) и заменить ею версию на каждой локации [прода](https://deploy.yandex-team.ru/stages/verdaccio-production/config/du-verdaccio-production-man/box-Verdaccio#resources)
5. Нажать `Update`, ввести на последнем шаге лаконичный комментарий к ревизии и нажать `Deploy`

## Как снять нагрузку с локации?

1. [l7heavy](https://nanny.yandex-team.ru/ui/#/l7heavy/verdaccio.yandex.net/)
2. Раздел `bygeo`
3. Тыкнуть `Close w/ current weights` напротив нужной локации
4. Тыкнуть `Save section weights`

## Как покопать логи на машинках?

Дневные логи балансера доступны на [hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/npm-balancer-log).

Для доступа к машинкам через sky запущена отдельная [машинка](https://qyp.yandex-team.ru/vm/sas/npm-sky).

У балансера логи лежат в папке /logs. Там можно найти следующие файлы с логами:

- current-access_log-balancer-443
- current-access_log-balancer-80
- current-error_log-balancer-443
- current-error_log-balancer-80

У verdaccio логи лежат в папке porto_log_files внутри бокса. Там можно найти следующие файлы с логами:

- verdaccio-cmd_stderr.portolog
- verdaccio-cmd_stdout.portolog

Покопать логи можно следующим образом:

1. Зайти на выделенную машинку: `ssh -A npm-sky.sas.yp-c.yandex.net`
2. Для балансеров выполнить команду вида:  `sky portorun "tail -n 10 /logs/current-access_log-balancer-443" f@rtc_balancer_verdaccio_yandex_net_man`
3. Для verdaccio выполнить команду вида: `sky run "tail -n 10 /pod_agent/volumes/rootfs_Verdaccio/porto_log_files/verdaccio-cmd_stdout.portolog" YP@verdaccio-production.verdaccio-production-man:persistent`

## Как запустить тесты? {#tests}

У нас есть скрипт с интеграционными тестами, чтобы его запустить нужно пойти в директорию `frontend/projects/infratest/deprecated/verdaccio-smoke-test` и запустить там файл `smoke.sh`.
Рекомендуется выполнять их прогон после влития PR в мастер и раскатки нового Docker-образа на тестовый стенд.
Чтобы протестировать локально, достаточно в `smoke.sh` заменить `registry` на локальный.
Внутри `smoke.sh` используется утилита gsed, поэтому перед первым прогоном нужно поставить её из brew – `brew install gsed`.

## Как запустить нагрузочное тестирование?

Для нагрузочного тестирования у нас настроено [Dolbilo](https://deploy.yandex-team.ru/stage/npm-dolbilo)

Патроны сформированы из access_log балансера:
[патроны](https://sandbox.yandex-team.ru/resources?type=OTHER_RESOURCE&limit=20&attrs=%7B%22project%22%3A%22verdaccio-dolbilo%22%2C%22type%22%3A%22access-log-plan%22%7D)

При релизе нового образа на тестовый стенд необходимо переключить Dolbilo в режим тестирования нагрузки, а именно, выставить отвечающий за RPS параметр `--rps-schedule=step(50, 500, 50, 60)` в настройках контейнера. По умолчанию этот параметр отключён и запросы осуществляются с тем же RPS, что и на проде (т.к. логи взяты с одной машинки балансера, то это около 1/6 всего RPS).

Нужно учитывать, что после деплоя нового образа ему сначала необходимо прогреться, именно поэтому план в качестве плана нагрузки выбран `step`.

Если Dolbilo по каким-либо причинам не подходит, то необходимо заказать доступ к любой из машин из
[_TANKNETS_](https://puncher.yandex-team.ru/tasks?id=5f7b741427f8d48fd6c3f6e9),
после чего через Лунапарк провести стрельбы. В качестве патронов можно использовать патроны для Dolbilo.

## Как включить blocked-at?

В `verdaccio-yandex-storage` подключена библиотека [blocked-at](https://github.com/naugtur/blocked-at). Для её включения нужно в настройках деплоя выставить переменную окружения `BLOCKED_AT_LOGGING=1`.

Логи библиотеки затем можно найти в YDeploy ([например](https://deploy.yandex-team.ru/stages/npm-test-stage/logs?deploy-unit=verdaccio_man&highlight=57&query=message%3D%22blocked-at%22)).

## Доска с задачами

[Доска](https://st.yandex-team.ru/agile/board/11483)

## Страница npm на Wiki

[Страница](https://wiki.yandex-team.ru/npm/)

## Пример запроса для поиска логов

[Пример запроса](https://yql.yandex-team.ru/Operations/Xx8z35dg8vLJee865v0ck1tjP8di9ArP6ce_XVWWxWA=)

## Схема работы verdaccio

Первым делом все запросы идут в наши кеши, в прогретых кешах есть практически все пакеты и тарболы, поэтому в сам verdaccio летит только малая часть запросов.

В [метриках verdaccio](https://yasm.yandex-team.ru/panel/frimuchkov._oJfpYc/) на графиках `GET responses` графики `unistat-verdaccio_GET_route_fastTarballProxyMiddleware_status_302_ammm` и `unistat-verdaccio_GET_route_fastTarballProxyMiddleware_status_302_ammm` - графики тех запросов, которые мы не отправили в verdaccio. 302 коды ответа из-за того, что мы всегда отдаём ссылку на файлы в S3.

Если кеши не прогреты, то мы будем искать метаданные в базе, а наличие тарболов будем проверять путём отправки HEAD-запросов в S3 и только если ничего не найдено, будем синхронизировать пакет из внешнего npm.

## Как получить ключи к S3?

Значение переменных `AWS_ACCESS_KEY_ID` и `AWS_SECRET_ACCESS_KEY` можно получить следующим образом:

1. Получение oauth-токена для S3-MDS по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6797456f343042aabba07f49b478c49b)
2. Запросить роль `uploader` на работу с бакетом [вот здесь](https://nda.ya.ru/t/DD9EwDC73VyBL6)
```bash
curl -XPOST -H"Authorization: OAuth токен" "https://s3-idm.mds.yandex.net/credentials/create-access-key" --data "service_id=1405" --data "role=роль"
```

Пример ответа:
```json
{
  "AccessKeyId": "XXXXXXXXXXXXXXXXXXXX",
  "AccessSecretKey": "YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY",
  "IssueDate": "Thu, 09 Mar 2017 11:00:00 GMT",
  "Role": "reader",
  "ServiceId": 1405,
  "UserId": "<uid>"
}
```

## Как получить TVM_APP_SECRET?

Ключ к локальному TVM приложению лежит [вот тут](https://yav.yandex-team.ru/secret/sec-01emnxsnzb2zvqk8fhtzr8ytbn/explore/version/ver-01emnxsp0bpw12c3gt85xbjy9a)

## Как запустить образ локально?

**Важно: лучше использовать linux, так как docker for mac не имеет поддержки --network=host**

Все команды выполняются в директории infratest – `frontend/projects/infratest`:

1. [Авторизоваться во внутреннем registry](https://wiki.yandex-team.ru/docker-registry/#authorization)
2. Собрать образ `verdaccio-main` – `cd packages/verdaccio-main && docker build -t verdaccio:testing . --no-cache`. Может потребоваться опция `--network=host`.
3. `cd ../packages/verdaccio-yandex-storage/`.
4. В файле `docker-compose.yml` поменять образ в поле `image` на `verdaccio:testing` (или на тот, который вы использовали при сборке).
5. Выполнить `TVM_APP_SECRET=$TVM_APP_SECRET AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY docker-compose up`.

## Как подложить свою версию плагина?

Примерно так:

1. Пойти в `frontend/projects/infratest/packages/verdaccio-yandex-storage`
1. В файле `docker-compose.yml` в `volumes` у сервиса `volumes` подменить плагин по примеру `verdaccio-yandex-storage`

## Конфиги

Конфиги вшиты в образ, большинство настроек конфигурируется через переменные окружения
Сами конфиги лежат по пути `frontend/projects/infratest/packages/verdaccio-main/config`

## Поиск логов verdaccio по npmSession

```sql
USE arnold;

SELECT * FROM
    `logs/deploy-logs/30min/2020-08-06T02:30:00`
WHERE
    stage = 'verdaccio-production'
    AND
    Yson::Contains(context, "npmSession")
    AND
    Yson::LookupString(context, "npmSession") = 'e98cf905eaad277f'
ORDER BY `timestamp` DESC;
```

## Как подключиться к PostgreSQL?

Если не нужен GUI, то можно воспользоваться местной инструкцией, для этого кликаем [сюда](https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-postgresql/cluster/mdbv5pmjds3hv086op7j) и справа выбираем пункт `Подключиться`

Если хочется GUI, то делаем следующим образом:

- Получаем нужный хост: [список хостов](https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-postgresql/cluster/mdbv5pmjds3hv086op7j?section=hosts)
- Формируем URL: `$HOST_NAME.db.yandex.net`
- Создаём туннель через машинку в QYP: `ssh dev.sas.yp-c.yandex.net -L 127.0.0.1:6432:vla-n0z99nrkn68xj81m.db.yandex.net:6432`
- Берём пароль вот [отсюда](https://yav.yandex-team.ru/secret/sec-01edpmc8q9a60d7yq45nrnyja6)
- Пробуем подключиться через любую удобную программу (если не получается, то пробуем выставить параметр `sslmode=verify-ca`)

## Как удалить версию пакета?

В [npm-duty-cli-tools](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/npm-duty-cli-tool) есть соответствующая команда.

## Зачем нужны апстримы verdaccio_s3_tarball_proxy и verdaccio_s3_meta_proxy?

[verdaccio_s3_tarball_proxy](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/verdaccio.yandex.net/upstreams/list/verdaccio_s3_tarball_proxy/show/) и
[verdaccio_s3_meta_proxy](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/verdaccio.yandex.net/upstreams/list/verdaccio_s3_meta_proxy/show/)
нужны для того, чтобы ассессоры могли ходить в s3 за пакетами ([FEI-20653](https://st.yandex-team.ru/FEI-20653)).

## Что делать, если пользователь по ошибке опубликовал пакет во внутренний registry?

Проблема: пользователь публикует пакет во внутренний реджистри, затем публикует во внешний (пакет предназначается для внешнего реджистри).
Чтобы устранить последствия, нужно сделать следующее:

- Удалить пакет из s3
- Удалить пакет из базы (`DELETE from internal_packages WHERE name = 'PACKAGE_NAME_HERE'`)
- Стриггерить выкачивание пакета снаружи переходом по ссылке с указанием версии пакета (пример: https://npm.yandex-team.ru/get-gpu/1.0.1)

## Как посмотреть метрику по странице поиска?

Пока мы ждём intranet search, мы предоставляем пользователям собственную страницу поиска: [страничка](https://npm.yandex-team.ru).
К ней подключена Яндекс.Метрика. Для получения доступа к ней нужно:

- Запросить права вот здесь: [тык](https://idm.yandex-team.ru/system/metrika/roles#rf=1,rf-role=28551297#metrika/internal_counter_grant,f-status=all,f-role=metrika,sort-by=-updated,rf-expanded=28551297)
- В качестве идентификатора счётчика указать `70566175`
- Дождаться подтверждения роли
- Зайти в Яндекс при помощи нового логина (письмо о создании нового аккаунта придёт на корпоративную почту)
- Перейти на страницу [Яндекс.Метрики](https://metrika.yandex.ru/)

## Как разрешить синк пакета во внутренний npm, если пакеты с внешнего npm недоступны?

1. Пакет нужно добавить в исключения в [конфиге](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/verdaccio-main/config/config.yaml?rev=r9535167#L90) по примеру уже существующих правил. Желательно добавить ссылку на причину исключения.
2. Вкоммитить правки, влить PR.
3. Проверить доступность пакета на тестинге.
4. Раскатить npm в продакшене.

## Что делать, если Yadi ручка не отвечает или если мне нужно забанить что-то в обход?

Есть возможность указать локальный файл как источник банлиста.
Содержимое из ответа ручки [лежит в аркадии](https://a.yandex-team.ru/arcadia/security/yadi/blacklist/blacklist.json).

1. Положить файл `banlist.json` в [verdaccio-main/config](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/verdaccio-main/config). Формат должен быть как в ответе yadi.
2. Вкоммитить и влить PR.
3. Раскатить npm на тестинге. В переменных окружения нужно указать `BANLIST_LOCAL_PATH=/opt/verdaccio/config/banlist.json`.
4. Раскатить npm в продакшене. В переменных окружения нужно указать `BANLIST_LOCAL_PATH=/opt/verdaccio/config/banlist.json`.
