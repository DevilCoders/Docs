# Yellow Zones aka Popular Zones

Yellow Zones are zones of high concentration of popular shops, bars, restaurants,
cinemas, museums, etc. These zones are shown on maps to help users find attractive lively city areas.

These zones are being built on a daily basis by means of sandbox scheduler. YmapsDF uses YT export as a source for yellow_zones_bundle.

# Entry Points

| Key | Value |
|---|---|
| SRE | Dmitry [tswr@](https://staff.yandex-team.ru/tswr) Kornev  |
| Sources | [/maps/poi/yellow_zones](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/yellow_zones) <br/> [/sandbox/projects/maps/BuildYellowZones](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/BuildYellowZones) |
| Sandbox Scheduler | https://sandbox.yandex-team.ru/scheduler/17597/view |
| YT Export | [hahn.//home/maps/poi/yellow_zones/export](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/yellow_zones/export) |

# Algorithm

*Input*:
* features_table: Path to yt table group/features from Personalized POI,
* ymasdf_prefix: Path to yt directory with ymapsdf tables.

*Output*
* oid_dataset_table: Path to yt table, where intermediate oid dataset should be stored,
* shapes_table: Path to yt table, where the final table with yellow zones should be stored.
* yellow_oids_table: Path to yt table, where yellow zones POIs oids should be stored.

*Algorithm*
1. Select organizations of specific rubrics like shops, bars, restaurants,
cinemas, museums from features_table.
2. Count total number of deep clicks for each organization.
3. For each organization calculate a weighted average of deep clicks of other organizations in its vicinity.
4. In each city choose organizations that have the weighted average above some predefined quantile.
5. For each such organization take its building footprint and dilate it. 
6. Save resulting polygons. Merge of the polygons is carried out in denormalization.

# Dev Notes
*Download / upload*
```
YT_PROXY='hahn' yt read '//home/maps/poi/yellow_zones/shapes-2019.08.29' --format=json > shapes-2019.08.29.json
ya upload --ttl=inf shapes-2019.08.29.json
```

*Publish to ymapsdf testing*

```
curl -k -X POST -H "Content-Type: application/json" -d '{"resources": [{"version": {"properties": {"release_name": "1101697275-20190902", "file_list": [{"name": "yellow_zones_file", "url": "https://proxy.sandbox.yandex-team.ru/1101697275"}]}}, "name": "yellow_zones_bundle"}], "suppress_known_source_check": true}' https://core-garden-server.testing.maps.yandex.net/modules/yellow_zones_bundle/builds/
```

*Publish to ymapsdf stable*
```
curl -k -X POST -H "Content-Type: application/json" -d '{"resources": [{"version": {"properties": {"release_name": "1101697275-20190902", "file_list": [{"name": "yellow_zones_file", "url": "https://proxy.sandbox.yandex-team.ru/1101697275"}]}}, "name": "yellow_zones_bundle"}], "suppress_known_source_check": true}' https://core-garden-server.maps.yandex.net/modules/yellow_zones_bundle/builds/
```
