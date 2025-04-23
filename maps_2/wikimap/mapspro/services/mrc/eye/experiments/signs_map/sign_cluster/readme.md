    # sign-cluster

## Overview
Finds sign detection clusters for specified mrc features set. To run the tool you need [upload](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/tool/upload_mrc_feature) features into yt table in yson format and optionaly import sign recognitions in json [format](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/experiments/signs_map/readme.md) (to skip detection step). All necessary services are run in playgroud and results can be exported:
- Detections in json [format](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/experiments/signs_map/readme.md), use ```--export-detections```
- Sign clusters in json [format](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/experiments/signs_map/readme.md), use ```--export-clusters```

```
# Run recognition on YT
sign-cluster \
    --secret-version "ver-12345" \
    --mrc-config confing.xml \
    --features //tmp/example \
    --export-detections detections.json \
    --export-clusters clusters.json

# Import ground truth recognitions
# Use detections from export.json for quality tool!
sign-cluster \
    --secret-version "ver-12345" \
    --mrc-config confing.xml \
    --features //tmp/example \
    --import-detections import.json \
    --export-detections export.json \
    --export-clusters clusters.json
```
