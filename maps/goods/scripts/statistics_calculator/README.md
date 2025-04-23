# Usage examples

## Freshness statistics

```bash
./statistics_calculator freshness
```

## Recall statistics

```bash
./statistics_calculator recall \
    \
    --output-table //home/maps/geoapp/goods/testing/statistics/recall/shown_premalinks_with_prices_ratio_by_sprav_rubrics \
    --value-field parent_rubric \
    \
    --output-table //home/maps/geoapp/goods/testing/statistics/recall/shown_premalinks_with_prices_ratio_by_funduk_rubrics \
    --value-field funduk_rubric \
    \
    --output-table //home/maps/geoapp/goods/testing/statistics/recall/shown_premalinks_with_prices_ratio_by_region \
    --value-field region \
    \
    --output-table //home/maps/geoapp/goods/testing/statistics/recall/shown_premalinks_with_prices_ratio_by_service \
    --value-field service
```
