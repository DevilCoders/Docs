# Бинарь для генерации bs конфига

Бинарь ищет последний совместимый валидационный конфиг и строит по нему bs конфиг __prod_models.json__ вида:

```json
{
    "models": [
        {
            "key": "CPM_F6_predict_money_from_hit_mse_9__TEST",
            "version": "2017-07-30T00:00:00",
            "dump_key": "model",
            "type": "mx",
            "meta": {}
        },
        {
            "key": "CPM_F7_catboost_sample_ratio_19",
            "version": "2019-11-16T00:00:00",
            "dump_key": "model",
            "type": "mx",
            "meta": {},
        },
        {
            "key": "vw_realcost_rsya_even_pt234_w1",
            "version": "2021-09-23T00:00:00",
            "dump_key": "model",
            "type": "lm",
            "meta": {},
        },
        ...
    ]
}
```

И дифф __prod_diff.json__ между последней релизной версией bs конфига и новой, созданный либой __deepdiff__

usage:

```sh
yam
./generate
```

Для тестирования на локальном конфиге:

```sh
yam
./generate --config-path=<abs_path_to_config>
```
