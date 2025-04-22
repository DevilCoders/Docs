Чтобы с некоторой периодичностью запускался эвал на фиксированном датасете нужно 
1. добавить callback, который создает ltp.offline_eval.offline_eval_callback(callbacks_info, config_path, train_tables)
2. добавить в верхний уровень конфига описание эвала
```
    "offline_evaluation": {
        "start_date": "202101231000",
        "end_date": "202101231400",
        "hour_frequency": 48,
        "table": "//home/ads/ltp/users/jruziev/multi_uid/multi_uid_hit.hash1.rsya.torch"
    },
```

Нужно чтобы был хотя был один обычный онлайновый эвалуатор в конфиге, иначе не будет работать (временный костыль :) )
