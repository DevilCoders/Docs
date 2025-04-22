# Введение

Здесь описано предложение по реализации импорта видео и треков от внешних камер безопасности SignalQ2 из инфраструктуры Яндекс.Такси в Зеркала.

Ожидается, что к концу 2021 года камерами безопасности SignalQ2 будут оснащены 20 тысяч машин по всей России. Потенциально, это очень мощный источник свежих снимков. В настоящее время камеры безопасности уже выгружают выборочные видео с проездов, в дальнейшем можно сделать процесс сбора управляемым.

# Исходные данные

Данные по всем устройствам собраны в таблице [//home/taxi/production/replica/postgres/signal_device_api_meta_db/events](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/taxi/production/replica/postgres/signal_device_api_meta_db/devices), среди всего множества полей нам интересны:
- `id` -- внутренний идентификатор устройства
- `serial_number` -- серийный номер

Все события с камер безопасности содержатся в одной YT-таблице [//home/taxi/production/replica/postgres/signal_device_api_meta_db/events](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/taxi/production/replica/postgres/signal_device_api_meta_db/events).

Она содержит поля:
- `id` -- идентификатор события
- `device_id` -- идентификатор устройства
- `event_type` -- тип события
- `presigned_external_video_url` -- урл на видео с внешней камеры
- `presigned_external_video_url_expires_at` -- срок хранения видео
- `extra` -- дополнительные атрибуты события
- `event_at` -- UTC timestamp события

Пример содержимого поля `extra`:

```(json)
{
    "version": "0.0.9-1",
    "with_fallback": False,
    "LocationFilter": {
        "history": {
            "max_serialize_length": 30,
            "contained_type": "signalq_pyml.core.types.Location",
            "history_length": 20,
            "count": 5112,
            "values": [
                {
                    "speed": 6.070444392000001,
                    "lon": 37.608773983333336,
                    "lat": 55.86778344999999
                },
                {
                    "speed": 5.504555507999999,
                    "lon": 37.60869365,
                    "lat": 55.86777441666667
                },
                {
                    "speed": 5.247333288,
                    "lon": 37.60860586666667,
                    "lat": 55.86775901666666
                },
                {
                    "speed": 4.938666624,
                    "lon": 37.608531533333334,
                    "lat": 55.867749466666666
                },
                {
                    "speed": 4.938666624,
                    "lon": 37.60845463333333,
                    "lat": 55.8677363
                },
                {
                    "speed": 5.041555512,
                    "lon": 37.608376583333325,
                    "lat": 55.867725500000006
                },
                {
                    "speed": 4.835777736,
                    "lon": 37.60830371666667,
                    "lat": 55.86771565000001
                },
                {
                    "speed": 4.475666628,
                    "lon": 37.60823558333334,
                    "lat": 55.86769588333334
                },
                {
                    "speed": 4.938666624,
                    "lon": 37.60818204999999,
                    "lat": 55.8676715
                },
                {
                    "speed": 5.813222172000001,
                    "lon": 37.6081333,
                    "lat": 55.867633600000005
                },
                {
                    "speed": 7.510888824,
                    "lon": 37.608119383333324,
                    "lat": 55.86757118333333
                },
                {
                    "speed": 9.25999992,
                    "lon": 37.608138149999995,
                    "lat": 55.86749868333333
                },
                {
                    "speed": 10.2888888,
                    "lon": 37.60817723333333,
                    "lat": 55.867418799999996
                },
                {
                    "speed": 12.500999892000001,
                    "lon": 37.60827473333333,
                    "lat": 55.8672192
                },
                {
                    "speed": 11.009111015999999,
                    "lon": 37.60832065000001,
                    "lat": 55.86712073333333
                },
                {
                    "speed": 7.099333272,
                    "lon": 37.60835061666667,
                    "lat": 55.867050783333326
                },
                {
                    "speed": 7.099333272,
                    "lon": 37.60835061666667,
                    "lat": 55.867050783333326
                },
                {
                    "speed": 0.308666664,
                    "lon": 37.608374633333334,
                    "lat": 55.866991549999995
                },
                {
                    "speed": 0.7202222159999999,
                    "lon": 37.608380833333335,
                    "lat": 55.866978416666676
                },
                {
                    "speed": 0.8231111040000001,
                    "lon": 37.608378916666666,
                    "lat": 55.86696688333333
                }
            ],
            "timestamps": [
                5280.458321281,
                5281.526358443,
                5282.534460939,
                5283.542860006,
                5284.57049846,
                5285.582051601,
                5286.601755769,
                5287.612601207,
                5288.628107047,
                5289.633634072,
                5290.655481287,
                5291.682838895,
                5292.722866427,
                5293.761110236,
                5294.818629768,
                5295.830991016,
                5296.860780009,
                5297.871876918,
                5298.892183033,
                5299.898653719
            ]
        },
        "nan_cast_history": {
            "max_serialize_length": 0,
            "contained_type": "signalq_pyml.core.types.Location",
            "history_length": 20,
            "count": 5112,
            "values": None,
            "timestamps": None
        },
        "bad_location": False,
        "curvature": 0.21326951792484203
    }
}
```

Значения в массиве `LocationFilter.history.values` соответствуют значениям в `LocationFilter.history.timestamps`. Timestamp хранится как число секунд с момента загрузки устройства.

К сожалению, на текущий момент в таблице нет информации о точном времени начала видео, также нет возможности установить соответствие между фреймами видео и `LocationFilter.history.timestamps`.


Пример стоп-кадра из видео внешней камеры
![example of the external camera frame](https://jing.yandex-team.ru/files/quoter/sda-videos.s3.mds.yandex.netv1d363e937527947949e5ab9145d393bf3d363e937527947949e5ab9145d393bf3mediaemmcinternal20210813_2021-08-17_19-55-20.png)


# Описание процесса импорта данных

Процесс будет отслеживать появление новых видео от внешней камеры в YT-таблице [//home/taxi/production/replica/postgres/signal_device_api_meta_db/events](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/taxi/production/replica/postgres/signal_device_api_meta_db/events), принимать решение, следует ли импортировать его и импортировать его в инфраструктуру MRC.

## Предположения

Алгоритм работы процесса опирается на следующие предположения о данных в YT-таблице [//home/taxi/production/replica/postgres/signal_device_api_meta_db/events](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/taxi/production/replica/postgres/signal_device_api_meta_db/events):
1. Поле `id` задает хронологический порядок добавления записей в таблицу.
2. Поле `event_at` обозначает время создания события и совпадает со временем послелднего фрейма видео и последней точки GPS-трека.
3. Треки проходят по актуальному дорожному графу.

## Конфигурация процесса импорта данных

Процесс конфигурируется желаемой частотой обновления снимков, она зависит от гео-региона и важности дороги. Конфигурацию можно представить как массив кортежей из следующих параметров:
- `geo_id` -- идентификатор региона в геобазе
- `fc` -- функциональный класс ребра дорожного графа
- `threshold_days` -- пороговое значение возраста покрытия ребра снимками.

## Изменение в модели данных

```(sql)
ALTER TABLE signals.assignment_video RENAME TO signals.video;
ALTER TABLE signals.video ALTER COLUMN assignment_id DROP NUT NULL;

CREATE TABLE signals.frame_to_video (
    id bigserial PRIMARY KEY,
    frame_id bigint NOT NULL REFERENCES signals.feature (feature_id) ON DELETE CASCADE,
    video_id bigint NOT NULL REFERENCES signals.video (id) ON DELETE CASCADE,
    seconds_from_start real NOT NULL
);
```

## Цикл работы алгоритма

Процесс сохраняет в постоянную память, в переменную `last_processed_event_id`, `id` последнего обработанного события.

1. Прочитать из YT-таблицы [//home/taxi/production/replica/postgres/signal_device_api_meta_db/events](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/taxi/production/replica/postgres/signal_device_api_meta_db/events) запись, с `id > last_processed_event_id`.
2. Если `presigned_external_video_url` пуст или если `presigned_external_video_url_expires_at` меньше текущего времени, обновить `last_processed_event_id = id`, перейти к шагу 1.
3. Распарсить GPS-трек, сматчить его на дорожный граф.
4. Для каждого из сматченных ребер:
    4.1 Вычислить список регионов геобазы, к которым ребро принадлежит.
    4.2 На основе конфигурации определить минимальное значение `threshold_days`, подходящее для этого ребра.
    4.3 Определить текущий возраст покрытия ребра фотографиями
    4.4 Если возраст покрытия превышает `threshold_days`, перейти к шагу 6, импорту данных.
5. Если ни для одного из сматченных ребер не было принято решения об импорте, обновить `last_processed_event_id = id`, перейти к шагу 1.
6. Сохранить видео-файл в MDS, добавить запись в `signals.video`.
7. Извлечь снимки из видео, расстояние между двумя последовательными снимками должно быть не менее 5 м, разница по времени не должна быть меньше 1 секунды.
8. Сохранить полученные снимки в MDS, в таблицу `signals.feature`, а также сохранить соответствие между снимками и видео в таблице `signals.frame_to_video`. Установить для импортированных снимков `dataset=taxi_signalq2`.
9. Сохранить GPS-трек в `signals.track_point`
10. Обновить `last_processed_event_id = id`, перейти к шагу 1
