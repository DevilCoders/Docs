Пример запуска кубика для отладки:

```
VH3_DEV=1 ./dmp-gp-to-yt run-block dmp_gp_yt \
  --gp-path snb_models.art_dates \
  --yt-path //tmp/art-dates/test \
  --yt-schema '[{"name": "utc_created_dttm", "type": "string"}, {"name": "creation_date_as_str", "type": "date"}]' \
  --gpt-endpoint butthead \
  --dmp-config art-dmo-config-butthead
```
