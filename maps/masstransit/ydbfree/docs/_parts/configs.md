# Конфиги

## Конфиг модели
Конфиг модели содержит описание структуры модели и используемых фичей, а также некоторых ее параметров.
Используется при обучении модели, а также дистрибуцируется вместе с ней в дальнейшем.
Применить модель без конфига невозможно – необходимо определить какие фичи считать и в какой индекс класть.

Конфиг модели основан на базовом конфиге [analyzer ml lib](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/libs/ml)

Описание основных параметров:
* `max_forecast_horizon` – максимальный горизонт прогноза, в секундах
* `stop_duration` – константа базового времени стояния автобуса на остановке
* `features` – фичи
* `normalization` – тип нормализации таргета
* `part_lengths` – длины агрегируемых партов проеханной части

{% cut "Пример конфига" %}

```(json)
{
    "max_forecast_horizon": 1800,
    "stop_duration": 7,
    "features": {
        "passed_track_part": {
            "numerical": [
                "LENGTH",
                "SPEED",
                "STOPS_COUNT"
            ]
        },
        "signal": {
            "numerical": [
                "LOCAL_DAY_TYPE",
                "LOCAL_DAY_HOUR",
                "REGION"
            ]
        },
        "predicted_segment": {
            "numerical": [
                "LENGTH",
                "CURVATIVE",
                "LAT",
                "LON",
                "FORECAST_OFFSET",
                "DISTANCE_FROM_PREV_STOP",
                "DISTANCE_TO_NEXT_STOP",
                "STOPS_FROM_FORECAST",
                "TYPE_IS_STOP_SEGMENT",
                "TYPE_IS_STAGE_SEGMENT",
                "FORECAST_HORIZON",
                "STATISTICAL_AVG",
                "STATISTICAL_P50",
                "STATISTICAL_MIN",
                "STATISTICAL_MAX",
                "STATISTICAL_CNT",
                "STATISTICAL_INT"
            ]
        },
        "common": {
            "numerical": [
                "VEHICLE_TYPE_IS_BUS",
                "VEHICLE_TYPE_IS_TROLLEYBUS",
                "VEHICLE_TYPE_IS_TRAMWAY"
            ]
        }
    },
    "normalization": "LOG_SPKM",
    "part_lengths": [
        200,
        200,
        200,
        200
    ]
}
```

{% endcut %}
