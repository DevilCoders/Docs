## Instance configuration for graph-tile-builder

## Disk storage

All disk partitions (aka `volumes`) are of the same type - HDD. Overall disk storage is equal to 390 GB.

390 GB = 80 GB + 300 GB + 10 GB

### Ecstatic datasets volume - `/persistent`

Below ecstatic datasets are big enough to take their size into account
* yandex-maps-graph-compact - 5.0 GB
* yandex-maps-graph-compact-rtree - 1.2 GB

5 graph versions are stored in Garden system at the same time. Because one new version is built in parallel we should reserve storage for 6 graph versions.

There is alert [disk_quota](https://a.yandex-team.ru/arcadia/maps/infra/sedem/lib/config/builtin_configs/rtc.yaml?rev=r9575214#L47) which monitors disk volume usage. WARN is equal to 75%, CRIT is equal to 85%.

So we can calculate necessary disk volume.

50 GB ~ (5.0 + 1.2) * 6 / 0.75

Current persistent volume size is set to 80 GB for future growth.

### Logs volume - `/logs`

Below logs are big enough to take their size into account
* /var/log/nginx/access-tskv.log - [10.0 GB](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/graph-tile-builder/docker/install/etc/template_generator/config.d/02_graph-tile-builder_setup.yaml?rev=r8410649#L20), (10 + 1 + 1) files, not compressed
* /var/log/nginx/error.log - [1.0 GB](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/graph-tile-builder/docker/install/etc/template_generator/config.d/02_graph-tile-builder_setup.yaml?rev=r8410649#L24), (7 + 1 + 1) files
* /var/log/yandex/maps/graph-tile-builder - [5 GB](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/graph-tile-builder/docker/install/etc/template_generator/config.d/02_graph-tile-builder_setup.yaml?rev=r8410649#L27), (7 + 1 + 1) files

So we can calculate necessary disk volume.

240 GB ~ (12 * 10 GB + 9 * 1 GB + 9 * 5 GB) / 0.75

Current logs volume size is set to 300 GB.

### /root_dir + /work_dir

Each is equal t0o 1 GB. Storage is used for each of 5 snapshots.

10 GB = (5 * 1 GB + 5 * 1 GB)
