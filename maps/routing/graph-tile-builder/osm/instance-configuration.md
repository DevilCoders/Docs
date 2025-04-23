## Instance configuration for graph-tile-builder over OSM

## Disk storage

All disk partitions (aka `volumes`) are of the same type - HDD. Overall disk storage is equal to 400 GB.

400 GB = 140 GB + 250 GB + 10 GB

### Ecstatic datasets volume - `/persistent`

Below ecstatic datasets are big enough to take their size into account
* yandex-maps-graph-compact - 18.0 GB
* yandex-maps-graph-compact-rtree - 4.5 GB

3 graph versions are stored in Garden system at the same time. Because one new version is built in parallel we should reserve storage for 4 graph versions.

There is alert [disk_quota](https://a.yandex-team.ru/arcadia/maps/infra/sedem/lib/config/builtin_configs/rtc.yaml?rev=r9575214#L47) which monitors disk volume usage. WARN is equal to 75%, CRIT is equal to 85%.

So we can calculate necessary disk volume.

120 GB ~ (18.0 + 4.5) * 4 / 0.75

Current persistent volume size is set to 140 GB for future growth.

### Logs volume - `/logs`

Below logs are big enough to take their size into account
* /var/log/nginx/access-tskv.log - [10.0 GB](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/graph-tile-builder/osm/docker/install/etc/template_generator/config.d/02_graph-tile-builder_setup.yaml?rev=r9072835#L20), (10 + 1 + 1) files, not compressed
* /var/log/nginx/error.log - [1.0 GB](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/graph-tile-builder/osm/docker/install/etc/template_generator/config.d/02_graph-tile-builder_setup.yaml?rev=r9072835#L20), (7 + 1 + 1) files
* /var/log/yandex/maps/graph-tile-builder - [5 GB](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/graph-tile-builder/osm/docker/install/etc/template_generator/config.d/02_graph-tile-builder_setup.yaml?rev=r9072835#L20), (7 + 1 + 1) files

So we can calculate necessary disk volume.

240 GB ~ (12 * 10 GB + 9 * 1 GB + 9 * 5 GB) / 0.75

Current logs volume size is set to 250 GB.

### /root_dir + /work_dir

Each is equal to 1 GB. Storage is used for each of 5 snapshots.

10 GB = (5 * 1 GB + 5 * 1 GB)
