### How to run
```bash
# Prepare table with required info about POIs
env YQL_TOKEN=$(cat ~/.yql_token) ../protected_geo_product/impressions/collect_geoproduct_info/collect_geoproduct_info --output-table $POSITIONS

# Fetch all tiles with such positions and make (permalink, zoom, is_indoor_covered) table
./process_tiles/process_tiles --positions $POSITIONS --destination $ZOOMS

# Join all zooms per permalink & final POI filtering
./merge_zooms/merge_zooms --unpacked-zooms $ZOOMS --impressions $IMPRESSIONS
```

Optional TVM params for `process_tiles`:
 - `IMPRESSIONS_TVM_SECRET` - env variable with TVM secret
 - `--tvm-self-id` - current app TVM app id
 - `--tvm-renderer-id` - renderer TVM app id

 E.g.
```bash
IMPRESSIONS_TVM_SECRET=tvmappsecret123 --positions $POSITIONS --destination $ZOOMS --tvm-self-id 2025240 --tvm-renderer-id 2023928
```
