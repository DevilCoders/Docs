## Запуск экспорта на stable-данных

Экспорт можно запустить на разработческой машине, например, `spica.maps.dev.yandex.net`, из worktree своего репозитория. Далее под `<arcadia_root>` понимается корневая папка Аркадии (обычно это `~/arcadia` или `~/arc/arcadia`).

### Подготовка к запуску
1. Выполнить сборку:
    ```
    cd <arcadia_root>/maps/doc/schemas/ymapsdf/package
    ya make -r
    ```
2. Отредактировать файл __(временно, на период экспериментов)__ `<arcadia_root>/maps/wikimap/mapspro/tools/ymapsdf-conversion/json2ymapsdf/cfg/packages/test/ya.make`:
    ```
    SET(WIKI_EDITOR_CFG_DIR <arcadia_root>/maps/wikimap/mapspro/cfg/editor)
    SET(YMAPSDF_SCHEMA_DIR <arcadia_root>/maps/doc/schemas/ymapsdf/package)
    SET(YMAPSDF_VALIDATION_SQL_DIR <arcadia_root>/maps/doc/schemas/ymapsdf/garden/validation)
    ```
3. Выполнить сборку:
    ```
    cd <arcadia_root>/maps/wikimap/mapspro/tools/ymapsdf-conversion/json2ymapsdf
    ya make -r
    cd <arcadia_root>/maps/wikimap/mapspro/services/tasks_export/src/export_worker/client
    ya make -r
    ```
4. Скопировать файлы `services-base.xml` и `services.softtesting.xml` из каталога `<arcadia_root>/maps/wikimap/mapspro/cfg/services` к себе в `~/config`, после чего во втором файле заменить все вхождения строки `{{ POSTGRESQL_MAPSPRO_MDB }}` на значение соответствующего ключа из секрета `mapsdb-mapspro-stable`.
5. Создать каталог для результатов экспорта (в примере будет `~/export`).
6. Запуск экспорта производится командой в каталоге `<arcadia_root>/maps/wikimap/mapspro/services/tasks_export/src/export_worker/client`. Удобно использовать `screen` или `tmux`, т. к. процесс экспорта занимает продолжительное время.

### Запуск

- Основные объекты:
    ```
    ./wiki-export-worker-cli --branch-id <branch_id> --commit-id <commit_id> --config ~/config/services.softtesting.xml --json2ymapsdf <arcadia_root>/maps/wikimap/mapspro/tools/ymapsdf-conversion/json2ymapsdf/bin/json2ymapsdf --transform-cfg <arcadia_root>/maps/wikimap/mapspro/tools/ymapsdf-conversion/json2ymapsdf/cfg/packages/test/export_ymapsdf/json2ymapsdf.xml --ymapsdf-dir <arcadia_root>/maps/doc/schemas/ymapsdf/package --regions cis1 --root-dir ~/export --disable-mds-upload &> ~/export_log.txt
    ```
- Общественный транспорт:
    ```
    ./wiki-export-worker-cli --branch-id <branch_id> --commit-id <commit_id> --config ~/config/services.softtesting.xml --json2ymapsdf <arcadia_root>/maps/wikimap/mapspro/tools/ymapsdf-conversion/json2ymapsdf/bin/json2ymapsdf --transform-cfg <arcadia_root>/maps/wikimap/mapspro/tools/ymapsdf-conversion/json2ymapsdf/cfg/packages/test/export_masstransit/json2ymapsdf.xml --ymapsdf-dir <arcadia_root>/maps/doc/schemas/ymapsdf/package --geodata-path /var/lib/yandex/maps/ecstatic/data/yandex-maps-geodata6/geodata6.bin --subset masstransit --root-dir ~/export --disable-mds-upload &> ~/export_log.txt
    ```
- Организации:
    ```
    ./wiki-export-worker-cli --branch-id <branch_id> --commit-id <commit_id> --config ~/config/services.softtesting.xml --json2ymapsdf <arcadia_root>/maps/wikimap/mapspro/tools/ymapsdf-conversion/json2ymapsdf/bin/json2ymapsdf --transform-cfg <arcadia_root>/maps/wikimap/mapspro/tools/ymapsdf-conversion/json2ymapsdf/cfg/packages/test/export_poi/json2ymapsdf.xml --ymapsdf-dir <arcadia_root>/maps/doc/schemas/ymapsdf/package --regions cis1 --root-dir ~/export --disable-mds-upload &> ~/export_log.txt
    ```

Для получения понятных результатов и возможности сравнивать их лучше запускаться на какой-либо из релизных веток. Для этого нужно подставить её номер и номер соответствующего коммита в параметры запуска. Узнать их можно в Огороде([основные объекты](https://garden.maps.yandex-team.ru/ymapsdf), [общественный транспорт](https://garden.maps.yandex-team.ru/stable/mtr_mpro_export_src)): идентификатор поставки YMapsDF имеет формат `<date>_<task-id>_<stable-branch-id>_<commit-id>`.

### Тестирование результата

После сборки данных нужно [протестировать](https://docs.yandex-team.ru/garden/experiments) их корректность.

## То же, но автоматизированно и без следов

1. Если ещё нет, то создаём [экспериментальный контур в Огороде](https://docs.yandex-team.ru/garden/experiments#scenarij:-zapusk-lokalno-sobrannogo-modulya-na-vhodnyh-dannyh-iz-stabilnogo-kontura) (только шаг 1 из документации). Сам Огород [здесь](https://garden.maps.yandex-team.ru/).

2. Если ещё нет, заходим на дев. хост с настроенным докером (spica, jakku, etc) и добавляем себя в группу docker на хосте
    ```
    sudo usermod -a -G docker <username>
    ```
    После чего перезаходим на тачку, чтобы новая группа подсосалась.

3. Запускаем screen/tmux и выполняем
    ```
    cd <arcadia_root>/wikimap/mapspro/services/tasks_export/src/export_worker/client/docker
    ./make.sh --garden-contour <contour_name> --branch-id <branch_id> --commit-id <commit_id> [--subset <subset>] [--regions <regions>]
    ```
    Аргументы в целом совпадают с обычным cli, но есть два отличия: во-первых, `garden-contour` обязателен в случае make.sh, во-вторых, `task-id` указывать не нужно, оно будет игнорироваться. Для новых тасок в этом случае будут созданы записи в unstable-базе в таблицах `service.task` и `service.export_task`.

4. Ждём, когда соберётся докер и запустится экспорт (на экране побегут строчки из воркера экспорта), после чего можно идти заниматься другими делами. В идеале на почту придут два письма от Огорода о статусе билдов в модулях ymapsdf_src и ymapsdf.

5. По окончании работы в контейнере запускается пустой bash, т.е. контейнер не стопается, а остаётся включенным. Можно полазить по файловой системе контейнера, посмотреть локальный выхлоп от экспорта. Логи экспорта отображаются на экране и сохраняются в /var/log/yandex/maps/wiki/export-worker-cli.log

6. После выхода из контейнера будет предложено его _не удалять_. Если контейнер и образ больше не нужны, то можно просто нажать Enter. Если нужно их сохранить, нужно прожать `y`.
