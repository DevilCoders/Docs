# Instance configuration for router over OSM

## Disk storage

All disk partitions (aka `volumes`) are of the same type - SSD. Overall disk storage is equal to 520 GB.

520 GB = 400 GB + 110 GB + 10 GB

### Ecstatic datasets volume - `/persistent`

Below ecstatic datasets are big enough to take their size into account
* yandex-maps-geodata6 - 2.0 GB
* yandex-maps-graph-osm-compact - 18.0 GB
* yandex-maps-graph-osm-compact-edges-persistent-index - 12.0 GB
* yandex-maps-graph-osm-compact-rtree - 4.5 GB
* yandex-maps-graph-osm-router-compact-data7 - 29.0 GB
* yandex-maps-graph-osm-router-topology7 - 6.6 GB
* yandex-maps-graph-osm-routing-barriers-rtree - 5.1 GB
* yandex-maps-l6a-osm-jams-diff - 0.6 GB

3 graph versions are stored in Garden system at the same time. Because one new version is built in parallel we should reserve storage for 4 graph versions.

There is alert [disk_quota](https://a.yandex-team.ru/arcadia/maps/infra/sedem/lib/config/builtin_configs/rtc.yaml?rev=r9575214#L47) which monitors disk volume usage. WARN is equal to 75%, CRIT is equal to 85%.

So we can calculate necessary disk volume.

390 GB ~ (2 + 18 + 12 + 4.5 + 29 + 6.6 + 0.6 + 5.1) * 4 / 0.8

Current persistent volume size is set to 400 GB for future growth.

### Logs volume - `/logs`

Below logs are big enough to take their size into account
* /var/log/nginx/access-tskv.log - [5.0 GB](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/osm/docker/install/etc/template_generator/config.d/02_router-setup.yaml?rev=r9082873#L24), (3 + 1 + 1) files
* /var/log/nginx/error.log - 1.0 GB, (7 + 1 + 1) files
* /var/log/yandex/maps/router/router.log - [40 GB](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/osm/docker/install/etc/template_generator/config.d/02_router-setup.yaml?rev=r9082873#L21), (3 + 1 + 1) files

So we can calculate necessary disk volume.

105 GB ~ ((1 + 4 * 0.2) * 5 GB + (1 + 8 * 0.2) * 1 GB + (1 + 4 * 0.2) * 40 GB) / 0.8

Current logs volume size is set to 110 GB.

### /root_dir + /work_dir

Each is equal to 1 GB. Storage is used for each of 5 snapshots.

10 GB = (5 * 1 GB + 5 * 1 GB)
