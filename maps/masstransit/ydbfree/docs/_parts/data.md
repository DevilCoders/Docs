# Табличные данные

В наших процессах используются и создаются различные виды данных, для которых есть устоявшиеся названия.

## Сырые сигналы
GPS-сигналы общественного транспорта от партнёров сервиса.

Основные поля:
* _clid_ – идентификатор партнёра
* _uuid_ – идентификатор ТС
* _time_ – время замера GPS-координат (по мнению партнёра)
* _receive_time_ – время получения сигнала нашим сервисом
* _vehicle_type_ – тип ТС (автобус / троллейбус и пр.)
* _route_ – "сырой" маршрут, передается партнёров (нормализуется далее)
* _lat_, _lon_ – координаты сигнала

[Получаются обработкой](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/tools/filter_signals/) логов анализатора.

Путь на YT: [//home/yatransport-prod/production/signals](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/yatransport-prod/production/signals)

## Привязанные сигналы
Сигналы на нитках ОТ.

Основные поля:
* _clid_ – идентификатор партнёра
* _uuid_ – идентификатор ТС (также дублируется в легаси-колонку vehicle_id)
* _timestamp_ – время замера GPS-координат (по мнению партнёра)
* _trip_id_ – идентификатор поездки (алгоритм разделения является деталью реализации)
* _thread_ – идентификатор нитки
* _len_from_start_ – отступ от начала нитки

Получаются обработкой (привязкой, матчингом) сырых сигналов:
* [Старая привязка (aka баиндер)](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/masstransit/bind_signals/bin/bind_signals/)
* [Новая привязка (aka матчер)](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/masstransit/bind_signals/bin/match_signals/)

Путь на YT:
* Старым способом – [//home/maps/jams/production/masstransit/bound_signals](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/production/masstransit/bound_signals)
* Новым способом – [//home/maps/jams/production/masstransit/matched_signals](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/production/masstransit/matched_signals)

## Эталонные прибытия
Эталонные данные о времени прибытия ТС на остановки по нашим расчетам.

Основные поля:
* _clid_ – идентификатор партнёра
* _uuid_ – идентификатор ТС (также дублируется в легаси-колонку _vehicle_id_)
* _timestamp_ – время прибытия (аппроксимация)
* _thread_ –  идентификатор нитки
* _stop_id_ – идентификатор остановки

[Получаются обработкой](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/masstransit/prepare_etalon_arrivals/) привязанных сигналов или их производных.

Путь на YT: [//home/maps/jams/production/masstransit/etalon/arrivals](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/production/masstransit/etalon/arrivals)

## Прогнозные данные
Данные о реалтайм-прогнозах, сделанных сервисом.

### Прибытия
Прогнозы времени прибытия на остановку.

[Получаются обработкой](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/masstransit/process_predictor_logs/) сырых [логов сервиса](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-masstransit-predictions-stable/1d).

Основные поля:
* _clid_ – идентификатор партнёра
* _uuid_ – идентификатор ТС
* _prediction_id_ – идентификатор предсказания (включает несколько прогнозов для одного ТС вперед по нитке)
* _stop_id_ – идентификатор остановки
* _route_ – идентификатор маршрута
* _arrival_time_ – прогноз времени прибытия
* _signal_time_ – время последнего учтенного сигнала
* _prediction_time_ – время создания прогноза

Путь на YT: [//home/maps/jams/production/masstransit/forecasts/arrivals](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/production/masstransit/forecasts/arrivals)

### Траектории
Прогнозы траекторий движения меток ОТ по карте.

Основные поля:
* _clid_ – идентификатор партнёра
* _uuid_ – идентификатор ТС
* _prediction_id_ – идентификатор предсказания (включает всю траекторию ТС)
* _route_ – идентификатор маршрута
* _thread_ – идентификатор нитки
* _polyline_ – траектория движения (часть)
* _polyline_index_ – индекс части в общей траектории
* _duration_ – оценка времени движения по части (скорость считается постоянной)
* _signal_time_ – время последнего учтенного сигнала
* _prediction_time_ – время создания прогноза
* _reference_time_ – время, от которого складываются duration'ы (может быть не равно prediction_time!)
* _reference_offset_ – базовый отступ от начала нитки (на момент времени reference_time)

Путь на YT: [//home/maps/jams/production/masstransit/forecasts/trajectories](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/production/masstransit/forecasts/trajectories)

## Train-пулы
Пулы для обучения катбуста в соответствующем формате.

Основные поля:
* _prediction_id_ – идентификатор предсказания
* _prediction_segment_index_ – индекс сегмента в предсказании
* _signal_time_ – время сигнала, на основании которого было сделано предсказание
* _clid_, _uuid_, _trip_id_, _vehicle_type_, _thread_, _route_ – вспомогательные данные о сэмпле

Путь на YT: [//home/maps/jams/production/masstransit/training_pools](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/production/masstransit/training_pools)

## Roadgraph traits
Данные автомобильного (дорожного) графа. 1 строка – информация об одном ОТ-ребре. Графы ОТ и автомобильный – два разных графа, однако данные из последнего могли бы быть полезны модели. Например, ограничения скоростей, наличие выделенной полосы, расположения светофоров и пр. Более того, эта информация нужна для использования пробок.

_В данный момент задача на добавление новых фичей в модель в разработке_

Основные поля:
* _thread_id_ – идентификатор нитки
* _mt_edge_index_ – индекс ребра
* _mt_edge_length_ – длина ребра
* _covered_ratio_ – доля покрытия дорожным графом
* _masstransit_lanes_length_ – длина дороги с выделенной полосой
* _traffic_lights_count_ – количестве светофоров
* _default_speed_ – т.н. "дефолтная скорость"
* _speed_limit_ – ограничение скорости

Путь на YT: [//home/maps/jams/production/masstransit/road_graph_traits](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/production/masstransit/road_graph_traits)

## Пробки
Реалтайм-пробки на разные моменты времени. 1 строка – пробки на одном ОТ-ребре.

_В данный момент задача на добавление новых фичей в модель в разработке_

Основные поля:
* _thread_id_ – идентификатор нитки
* _mt_edge_index_ – индекс ребра
* _time_ – время, на которое представлены пробочные данные
* _jams_speed_ – пробочная скорость
* _covered_ratio_ – доля покрытия информацией о пробках

Путь на YT: [//home/maps/jams/production/masstransit/realtime_jams](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/production/masstransit/realtime_jams)
