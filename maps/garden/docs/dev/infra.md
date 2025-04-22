# Инфраструктура

UI Огорода:
* [stable UI](https://garden.maps.yandex-team.ru/)
* [testing UI](https://garden.tst.c.maps.yandex-team.ru/)

## Nanny/YP

В Nanny/YP работают сервер и шедьюлер Огорода.

* Сводная информация о сервере Огорода на страничке [SEDEM](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs={%22sedem_service%22:%20%22core-garden-server%22})
* Сводная информация о scheduler Огорода на страничке [SEDEM](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_PAGE/index.html?attrs={%22sedem_service%22:%20%22core-garden-scheduler%22})

## Frontend

Y.Deploy:
* [stable](https://yd.yandex-team.ru/stage/maps-front-garden_production)
* [testing](https://yd.yandex-team.ru/stage/maps-front-garden_testing)

[Исходный код](https://a.yandex-team.ru/arc_vcs/maps/front/services/garden).

Ответственный: [Дмитрий Коваль](https://staff.yandex-team.ru/smith)

## YT

[Графики для самодиагностики](https://yt.yandex-team.ru/docs/problems/selfdiag#dashbordy-i-grafiki)

### Хранение

Аккаунты: garden (продакшен) и garden-exp (тестинг и песочницы)

[Общий дашборд](https://yt.yandex-team.ru/hahn/accounts/general?filter=garden&)

[Квоты garden](https://solomon.yandex-team.ru/?project=yt&cluster=hahn&service=accounts&host=none&dashboard=yt-account-limits-media&l.account=garden)

[Квоты garden-exp](https://solomon.yandex-team.ru/?project=yt&cluster=hahn&service=accounts&host=none&dashboard=yt-account-limits-media&l.account=garden-exp)

[Домашняя папка garden](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden)

[Домашняя папка garden-exp](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden-exp)

### Вычисления

Используется общий пул `garden`. В продакшене операции запускаются из-под пользователя `robot-garden-prod`. В тестинге и песочницах - из-под `robot-garden`.

[Общий дашборд](https://yt.yandex-team.ru/hahn/scheduling/details?pool=garden&tree=physical&)

[Дашборд с разбиением по модулям и задачам](https://dash.yandex-team.ru/rlc80mom129go)

[График потребления SSD](https://solomon.yandex-team.ru/?project=yt&cluster=hahn&service=accounts&l.medium=ssd_slots_physical&l.account=garden&graph=yt-account-disk&b=1d&e=)

## Mongo

Монго используется для хранения метаинформации об огородных ресурсах и служебных данных огородного сервера.

Кластера в [MDB](https://yc.yandex-team.ru/folders/fooj6ecqh8rsdsnj5806/managed-mongodb).

Кроме естественного доступа между компонентами одного окружения (например, stable сервер имеет RW доступ до stable монго-базы),
для поддержки синхронизации информации о версиях модулей, работает RO доступ от серверов из не-stable окружений до stable монго-базы.

## Sandbox

### Группа [MAPS_GARDEN](https://sandbox.yandex-team.ru/admin/groups/MAPS_GARDEN/general)

Под этой квотой запускаются таски:
* GARDEN_YT_STATS_COLLECTOR
* GARDEN_OSM_DOWNLOADER
* GARDEN_SERVER_AUTOTESTS
* RENDER_MODULES_TO_STAT
* OFFLINE_TILE_CACHE_TO_STAT
* MDS_UPLOAD (файлы из огородных тасок выгружаются в Сендбокс)
* Сборка деб-пакетов и тулов

[График потребления вычислительной квоты](https://grafana.yandex-team.ru/d/000015873/sandbox-quota-consumption-production?orgId=1&refresh=1m&var-owner=MAPS_GARDEN&var-group_by_days=0)

[График потребления дисковой квоты](https://grafana.yandex-team.ru/d/3MdO34WMk/sandbox-resources-storage-statistics-production?orgId=1&viewPanel=17&var-bucket=sandbox-2414&from=now-7d&to=now)

[Сколько диска занимает каждый тип ресурса](https://grafana.yandex-team.ru/d/3MdO34WMk/sandbox-resources-storage-statistics-production?viewPanel=10&orgId=1&var-owner=MAPS_GARDEN&var-type=All&var-bucket=All&var-count_deleted=no&from=now-7d&to=now)

### Коммунальная группа [MAPS-CI](https://sandbox.yandex-team.ru/admin/groups/MAPS-CI/general)

Под этой квотой собираются бинарные модули и докер-контейнеры.

[График потребления квоты](https://grafana.yandex-team.ru/d/000015873/sandbox-quota-consumption-production?orgId=1&refresh=1m&var-owner=MAPS-CI&var-group_by_days=0)

## S3 MDS

[Браузер файлов](https://yc.yandex-team.ru/folders/fooj6ecqh8rsdsnj5806/storage)

[Диспенсер](https://dispenser.yandex-team.ru/db/projects/maps-core-garden)

FileResource/DirResource:
* [stable](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-garden-files-stable;owner=2414)
* [testing](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-garden-files-testing;owner=2414)
* [playgrounds](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-garden-files-unstable;owner=2414)

Логи операций:
* [stable](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-garden-logs-stable;owner=2414)
* [testing](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-garden-logs-testing;owner=2414)
* [playgrounds](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-garden-logs-unstable;owner=2414)

## Календарь Garden Maintenance

Огородный календарь событий расположен [тут](https://calendar.yandex-team.ru/embed/month?layer_ids=248122&tz_id=Europe%2FMoscow).
Так же, проверяются события [календаря](https://calendar.yandex-team.ru/embed/month?embed&layer_ids=22354) с общеяндексовскими учениями.
