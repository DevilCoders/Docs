Библиотека для оценки времени проезда по маршруту
===

Процесс обучения и применения модели
====
Для обучения моделей предсказания ETA мы используем различные входные данные (треки):
- [training_tracks](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/training_tracks)
- [training_travel_times](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/training_travel_times)
- [fixprice_training_tracks](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/fixprice_training_tracks)

Из входных данных регулярно считаются фичи и сохраняются в пулы. Пул представляет из себя подневные таблички со значениями фичей в формате TSV. Мы обучаем несколько моделей, которые различаются конфигами. Соответственно, каждая модель имеет свой пул в директории с пулами:
- [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/whole_track_model/pools)
- [продкашен](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/pools)

Для расчета пулов используется sandbox-процесс [prepare_training_pools](/arc/trunk/arcadia/maps/analyzer/sandbox/prepare_training_pools):
- [шедулер (тестинг)](https://sandbox.yandex-team.ru/scheduler/15260/view)
- [шедулер (продакшен)](https://sandbox.yandex-team.ru/scheduler/16128/view)

Из пулов регулярно (раз в 12 часов) обучаются модели в Нирване. Для обучения используется sandbox-процесс [train_model](/arc/trunk/arcadia/maps/analyzer/sandbox/train_model).

Готовые модели складываются в поддиректории директории с моделями:
- [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/whole_track_model/models)
- [продкашен](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/models)

Каждая поддиректория с моделями имеет симлинку `latest` на последнюю версию, которая обновляется в процессе загрузки модели на YT.
В процессе генерации моделей они также загружаются в ecstatic в датасеты с именами вида `yandex-maps-whole-track-model-...-info`. Версия датасета состоит из даты и часа генерации модели и совпадает с версией на YT.

Регулярную оценку получившихся моделей в оффлайне проводит процесс [offline_eta_quality](/arc/trunk/arcadia/maps/analyzer/sandbox/offline_eta_quality), который сохраняет результаты на YT:
- [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/offline-eta-quality)
- [продкашен](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/offline-eta-quality)

Агрегированные значения в виде графиков представлены на [дашборде](https://dash.yandex-team.ru/5q70qk3wf8ww2?tab=YW)

В таблице приведлены актуальные модели, ссылки на их данные и текущий статус:
| Модель | Используемые треки | Конфиг | Пул | Модели | Датасет в ecstatic | Статус | Описание |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Future | [training_tracks](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/training_tracks) | [future](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/eta_prediction/configs/future.meta) | [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/pools/future) | [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/models/future) | [yandex-maps-whole-track-model-future-info](http://ecstatic.maps.yandex.net/pkg/yandex-maps-whole-track-model-future-info/versions) | В продакшене | Предсказывает время проезда по маршруту в будущем, без использования реалтайм-пробок |
| Taxi | [fixprice_training_tracks](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/fixprice_training_tracks) | [statistical_features_no_offset_no_min_len](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/eta_prediction/configs/statistical_features_no_offset_no_min_len.meta) | [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/pools/taxi) | [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/models/taxi) | [yandex-maps-whole-track-model-taxi-info](http://ecstatic.maps.yandex.net/pkg/yandex-maps-whole-track-model-taxi-info/versions) | В продакшене | Предсказывает время проезда по маршруту для прайсинга такси |
| User traits weighted p75 w4 | [training_travel_times](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/training_travel_times) | [statistical_features_no_offset_no_min_len](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/eta_prediction/configs/statistical_features_no_offset_no_min_len.meta) | [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/whole_track_model/pools/user_traits_weighted_p75_w4) | [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/whole_track_model/models/user_traits_weighted_p75_w4) | [yandex-maps-whole-track-model-user-traits-weighted-info](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-whole-track-model-user-traits-weighted-info/versions) | В продакшене | Использует user traits, взвешенный пул |
| User traits local time | [training_travel_times](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/training_travel_times) | [user_traits_local_time_day_type](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/eta_prediction/configs/user_traits_local_time_day_type.meta) | [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/pools/user_local_time) | [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/models/user_local_time) | [yandex-maps-whole-track-model-user-local-time](http://ecstatic.maps.yandex.net/pkg/yandex-maps-whole-track-model-user-local-time/versions) | В продакшене | Использует user traits (актуальная модель) |

В онлайне модели применяются в сервисе [router](https://abc.yandex-team.ru/services/2850/).
Используемые в сервисе модели описаны в [конфиге роутера](/arc/trunk/arcadia/maps/routing/router/yacare/config.cpp)

Описание структуры модели
====
Трек делится на `partsCount` частей.
Все фичи модели делятся на 2 вида: первые относятся к треку целиком (время старта и пр.), остальные – считаются отдельно на всем треке и каждой из `partsCount` частей. Большинство фичей относятся ко второму виду.
Таргет модели – результат некоторой функции от средней скорости на треке.

_Offset_ – устаревший параметр, используйте всегда _null_ в качестве его значения.

Описание интерфейса библиотеки
====
Для использования библиотеки следует ознакомиться с интерфейсами, описанными в следующих хэдерах:
- [`model.h`](include/model.h) – описывает конфигурацию модели (т.е. ее параметры)
- [`predict_time.h`](include/predict_time.h) – содержит функции для расчета предсказания по модели и его применения
- [`calc_factors.h`](include/calc_factors.h) – содержит функции для расчета значений фичей (используется при обучении)

Процесс применения модели
====
```
// load `graph`
// load `edgePersistentIndex` and `statisticalData` if needed
// get `route`, `timestamp` (now / in the future), `userPosition` from user request
// calculate `jamsInfo`

const std::string modelFilePath = ...
const std::string modelConfigPath = ...
const Model model{modelFilePath, modelConfigPath};

const auto prediction = predict(
    graph,
    edgePersistentIndex,
    jamsData,
    statisticalData,
    calendar,
    geobase,
    edges,
    model,
    timestamp,
    userTraitsData,
    uuid
);

if (prediction) {
    applyModelPrediction(
        jamsInfo.segments,
        *prediction,
        userPosition
    );
}
```

Процесс добавления новой фичи
====
1. Добавить фичу в `enum` в файле [`features.h`](include/features.h)
2. Добавить в [`model_part_features-tpl.h`](impl/model_part_features-tpl.h) / [`model_track_features-tpl.h`](impl/model_track_features-tpl.h) специализацию метода расчета фичи
3. Добавить в [`model.cpp`](impl/model.cpp) маппинг из строкового имени фичи в метод ее расчета
4. Добавить строковое имя фичи в собственный файл конфигурации модели и запустить обучение
5. Запустить оценку качества новой модели с конфигурационным файлом из предыдущего пункта

Пример конфига для дефолтной модели:
```
{
    "track_features": [
        "TIME_MINUTE",
        "TIME_MONTH",
        "TIME_WEEKDAY"
    ],
    "part_features": [
        "ANGLE",
        "BRIDGE",
        "CATEGORY",
        "CATEGORY_UNIQUE",
        "CATEGORY_MAX",
        "CATEGORY_MIN",
        "DEFAULT_COVERED_KMPH",
        "JAMS_COVERED_KMPH",
        "JAMS_COVERED_KMPH_VARIANCE",
        "DEFAULT_KMPH_AND_JAMS_KMPH_DIFF",
        "DEFAULT_GEO_KMPH",
        "DEFAULT_KMPH",
        "FERRY",
        "GEODISTANCE",
        "GEODISTANCE_RATIO",
        "EDGES_IN",
        "JAMS_GEO_KMPH",
        "JAMS_KMPH",
        "JUNCTION",
        "END_LAT",
        "START_LAT",
        "LENGTH",
        "END_LON",
        "START_LON",
        "DEFAULT_NON_COVERED_KMPH",
        "NON_COVERED_RATIO",
        "EDGES_OUT",
        "ROUNDABOUT",
        "SEGMENTS_PER_KM",
        "SPEED_LIMIT_AND_DEFAULT_KMPH_DIFF",
        "SPEED_LIMIT_AND_JAMS_KMPH_DIFF",
        "SPEED_LIMIT_GEO_KMPH",
        "SPEED_LIMIT_KMPH",
        "SPEED_LIMIT_MAX",
        "SPEED_LIMIT_MIN",
        "SPEED_LIMIT_UNIQUE",
        "TRAFFIC_LIGHTS",
        "TUNNEL"
    ],
    "parts_count": 8,
    "offset_length": null,
    "min_track_len_for_model": 1000.0,
    "load_jams": true,
    "load_stats": false,
    "normalization": "LOG_SPKM"
}
```

Изменение множества моделей по-умолчанию
====
Есть дефолтные модели - `DefaultModel`. Нужны для того, чтобы на роутере выбирать актуальную модель для каждого вида запросов. Для этого генерируется конфиг в [train-model](https://a.yandex-team.ru/arcadia/maps/analyzer/sandbox/eta_prediction/train_model) Если дефолтная модель добавляется, то сначала добавляем генерацию в `train-model`, ждем появления датасета на роутере, после уже обновляем `time_estimator`
