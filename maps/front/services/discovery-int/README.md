# Discovery Int

[![oko health][oko-badge]][oko-link]

[oko-badge]: https://badger.yandex-team.ru/oko/repo/maps/discovery-int/health.svg
[oko-link]: https://oko.yandex-team.ru/repo/maps/discovery-int?statusFilter=all

## General Information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-discovery-int |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-discovery-int |

## Instances

| Environment | URL |
|---|---|
| Testing | http://discovery-int.tst.c.maps.yandex.net |
| Production | http://discovery-int.maps.yandex.net |

## Secrets

| Environment | URL |
|---|---|
| Testing | https://yav.yandex-team.ru/secret/sec-01eaxtyhc5qckwqw1xznd82k1h/explore/versions |
| Production | https://yav.yandex-team.ru/secret/sec-01ecwz4rezk0gw3f6c4qn2h5ms/explore/versions |
| S3 Podrick | https://yav.yandex-team.ru/secret/sec-01dqfh23hvdxth95hnqne2hd9a/explore/versions |

## Database

| Environment | DB name | Cluster ID | Yandex Cloud |
|---|---|---|---|
| Testing | maps_discovery_testing | 28598aac-f568-402c-89e8-017961a178e5 | https://yc.yandex-team.ru/folders/foo58ac41h7o7lod6pu7/managed-postgresql/cluster/28598aac-f568-402c-89e8-017961a178e5 |
| Production | maps_discovery_production | 9f8dc2b0-47af-4d24-bd56-270ef69982d4 | https://yc.yandex-team.ru/folders/foo58ac41h7o7lod6pu7/managed-postgresql/cluster/9f8dc2b0-47af-4d24-bd56-270ef69982d4 |

[Yandex Managed Service for PostgreSQL Documentation](https://doc.yandex-team.ru/cloud/managed-postgresql/index.html)

## S3 Storage

**Avatars MDS**
https://yasm.yandex-team.ru/template/panel/avatars_mds/ns=discovery-int

**Actual quota:** https://st.yandex-team.ru/MDS-10900

**Converted video**
https://yasm.yandex-team.ru/template/panel/s3_client/bucket=vh-maps-converted;owner=3940

**Original video**
https://yasm.yandex-team.ru/template/panel/s3_client/bucket=vh-maps-src;owner=3940

**Legacy video**
https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-stories-original;owner=2513

## Known clients

- [Yandex Maps](https://abc.yandex-team.ru/services/maps-front-maps)
- [Mobile.Maps Proxy](https://abc.yandex-team.ru/services/maps-front-mobmaps-proxy-api)
- [Discovery Admin](https://abc.yandex-team.ru/services/maps-front-discovery-admin)

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-discovery-int_production.app |

## Dashboards

| Name | URL |
|---|---|
| Golovan | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-discovery-int_production;mode=full/ |
| DB Monitorings (testing) | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=28598aac-f568-402c-89e8-017961a178e5;dbname=maps_discovery_testing |
| DB Monitorings (production) | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=9f8dc2b0-47af-4d24-bd56-270ef69982d4;dbname=maps_discovery_production |

## Backend dashboards

| Name | URL |
|---|---|
| search | https://yasm.yandex-team.ru/template/panel/addrs_kpi |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/porto_log_files/app_workload_stdout.portolog`, `/porto_log_files/app_workload_stderr.portolog` |
| Nginx, Juggler Client, Push client | /var/log/supervisor/ |
| YT (maps) | `home/logfeller/logs/maps-front-production-log/1d`, `tskv_format = "front-discovery-int_app"` |
| YT (qloud) | `home/logfeller/logs/qloud-runtime-log` |

### Schedulers

| Scheduler | URL |
|---|---|
| export-events-oid | https://a.yandex-team.ru/arc_vcs/maps/front/services/discovery-int/src/schedulers/scripts/export-events-oid |
| refresh-block-links | https://a.yandex-team.ru/arc_vcs/maps/front/services/discovery-int/src/schedulers/scripts/refresh-block-links |
| refresh-pages-content | https://a.yandex-team.ru/arc_vcs/maps/front/services/discovery-int/src/schedulers/scripts/refresh-pages-content |
| refresh-tracker-info | https://a.yandex-team.ru/arc_vcs/maps/front/services/discovery-int/src/schedulers/scripts/refresh-tracker-info |
| rewrite-yt-images | https://a.yandex-team.ru/arc_vcs/maps/front/services/discovery-int/src/schedulers/scripts/rewrite-yt-images |
| rewrite-yt-pages | https://a.yandex-team.ru/arc_vcs/maps/front/services/discovery-int/src/schedulers/scripts/rewrite-yt-pages |
| rewrite-yt-rubrics | https://a.yandex-team.ru/arc_vcs/maps/front/services/discovery-int/src/schedulers/scripts/rewrite-yt-rubrics |
| rewrite-yt-snippets | https://a.yandex-team.ru/arc_vcs/maps/front/services/discovery-int/src/schedulers/scripts/rewrite-yt-snippets |
| import-device-segments | https://a.yandex-team.ru/arc_vcs/maps/front/services/discovery-int/src/schedulers/scripts/import-device-segments |

## API Information

### Snippets
Every organization have a snippet about main information about every page where it use.
The snippets create after publication pages. If you want to get the information you should set snippet `discovery/1.x` for request to [geosearch](https://wiki.yandex-team.ru/maps/api/http/internal/search/?from=%252Fmaps%252Fapi%252Finternal%252Fsearch%252F). For example:
`http://search.maps.yandex.net/1.x/?lang=ru&business_oid=1083877125&format=json&snippets=discovery/1.x`

### Avatars MDS
Discovery API uses a url template to provide image. Clients must replace "%s" in the url with one values from table:

| %s | Value in pixels |
|---|---|
| XXXS | 50x33 |
| XXS | 75x50 |
| XS | 100x67 |
| S | 150x100 |
| small208 | 208x208 |
| M | 300x200 |
| medium312 | 312x312 |
| L | 500x333 |
| XL | 800x533 |
| XXL | 1024x683 |
| XXXL | 1280x853 |
| orig | original |

*Based on [http-api-stub](https://github.yandex-team.ru/maps/http-api-stub)*
