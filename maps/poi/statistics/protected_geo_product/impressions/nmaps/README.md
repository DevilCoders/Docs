### How to run
```bash
# prepare table with required info about geoproduct POIs
env YQL_TOKEN=$(cat ~/.yql_token) ../collect_geoproduct_info/collect_geoproduct_info --output-table $GEOPRODUCT_TABLE

# run binary to check nmaps conflicts
env YT_TOKEN=$(cat ~/.yt/token) ./calc_conflicts --protected-geo-product-table $GEOPRODUCT_TABLE --output-table $IMPRESSIONS_TABLE --environment testing
```
