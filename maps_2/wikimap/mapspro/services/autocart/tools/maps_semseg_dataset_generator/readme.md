# Инструмент для загрузки данных с карт

Инструмент может быть использован для загрузки данных с как с ymapsdf, так и с личных разработческих стендов.

**Пример использования:**
Загрузка с ymapsdf:
> ./maps_semseg_dataset_generator \
> --tile-source 'http://core-sat-internal.maps.yandex.net/tiles' \
> --bbox '37.611688,55.789893~37.617481,55.792105' \
> --zoom 18 \
> --connstr "dbname=garden host=garden-pgm-rus01h.tst.maps.yandex.ru user=mapsgarden password=gardenTst port=5432 options=--search_path=public,ymapsdf_yandex_cis1_20180731_224721_822_96508406" \
> --shift_bld 1

Загрузка со стенда
> ./maps_semseg_dataset_generator
> --tile-source 'http://core-sat-internal.maps.yandex.net/tiles'
> --bbox '37.611688,55.789893~37.617481,55.792105'
> --zoom 18
> --config services.local.dolotov-e.xml
> --shift_bld 1

**Описание параметров:**
* **tile-source** - источник спутниковых снимков
* **bbox** - границы региона. Формат <min_lon>,<min_lat>~<max_lon>,<max_lat>
* **zoom** - масштаб снимка
* **connstr** - параметры подключения к базе ymapsdf
* **config** - конфигурационный файл для подключения к базе стенда
* **shift_bld** - флаг, отвечающий за сдвиг домов по спутнику.

**Инструкция для получения connstr к ymapsdf:**
Шаблон строки:
dbname=garden host=**host** user=mapsgarden password=gardenTst port=5432 options=--search_path=public,ymapsdf_yandex_**region**_**shipment_date**
1. Зайти на https://garden.tst.maps.yandex-team.ru/
2. Выбрать строчку с интересующим регионом (Cis1 - Россия, Tr - турция), в которой status=completed
3. Скопировать название региона на место region
4. Скопировать поле Shipment date на место shipment_date
5. Зайти на https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/conf/cluster/environment_settings.d/postgresql_servers.json.testing
6. По имени региона выбрать host и скопировать его на место host
