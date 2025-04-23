Обновление geobase.pm в Директе.

1. Забираем свежие данные с геоэкспорта:

В корне рабочей копии geobase-pm:

    ./bin/update.sh

2. Коммитим geobase_pkg_inc.json, пересобираем и выкладываем deb-пакет, раскатываем на ppcdev

3. В рабочей копии Директа:

Обновляем версию yandex-du-geobase-pm-perl в зависимостях.

Перегенерируем статику:

    protected/mk_regions.pl --files  
    protected/prebuild/get_geo_js.pl  
    protected/prebuild/get_metro_js.pl

Готовим миграцию для запуска скрипта

    protected/mk_regions.pl --db

4. Импортируем регионы в java, см.
    <https://a.yandex-team.ru/arc/trunk/arcadia/direct/common/src/main/resources/externalData>

5. В DNA используется тот же статический json-файл, который генерится mk_regions.pl для фронтэнда.
Для того чтобы обновить файл с регионами в DNA берем его из:  
`svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/direct/perl/data3/desktop.blocks/i-utils/i-utils.regions/all.regions.json`  
и коммитим в:  
`svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/adv/frontend/services/dna/src/service/RegionsHelpers/all.regions.json`

Альтернативный способ:

    cd dna && npm run updateAllRegions
