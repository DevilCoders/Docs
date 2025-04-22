# Актуальные рутины

`api_models_routine` - проверяет что нужные признаки готовы и применяет к ним модель.

Модели описаны в таблице `//home/x-products/production/config/datacloud/api-models-config`.

Бинарники лежат в `//home/x-products/production/datacloud/bins/partner_models`.

Готовые скоры в  `//home/x-products/production/datacloud/models`.

`snapshot_routine` - взять текущие таблицы крипты и сохранить в `//home/x-products/production/crypta_v2/snapshots`. Нужно для последующего грепа и применения моделей.

`dssm_routine` - проверить что нужные логи готовы и насчитать dssm-признаки. Признаки лежат в `//home/x-products/production/datacloud/aggregates/dssm`.

`cluster_routine` - проверить что нужные логи готовы и насчитать кластерные признаки. Признаки лежат в `//home/x-products/production/datacloud/aggregates/cluster` и `//home/x-products/production/datacloud/aggregates/normed_s2v`.

`phone_range_routine` - посчитать phone-range признаки.

`time_hist_routine` - посчитать time-hist признаки.
