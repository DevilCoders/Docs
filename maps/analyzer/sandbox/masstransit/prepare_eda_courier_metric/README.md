## Особенности определения типа движения и выбор подходящих запросов в роутер

---

**`unknown`**

Если для этапа заказа слишком мало сигналов с движением курьера, тип не устанавливается

**`pedestrian`**

1. Пешеходы в исходной таблице с заказами (`eda_vehicle_type` == pedestrian )
2. Максимальная скорость (`max_smoothed_speed`) не может превышать 2,5 (м/с)

Маршруты получаем из [логов ОТ роутера][mtroute_log]

**`bicycle`**

1. Велосипедисты в исходной таблице с заказами (`eda_vehicle_type` == bicycle )

Маршруты получаем из [логов велороутера][bicycle_log]

**`other`**

Необработанные типы из таблицы заказов

---

## Описание колонок результирующей метрики

| параметры метрики | тип | описание |
|-|-|-|
| `order_id` | 	`Uint64` | ID заказа из [логов доставки заказов][order_table] (order_id) |
| `order_stage` | `Uint64` | Этап заказа (1 - путь до ресторана, 2 - путь до клиента) из [логов доставки заказов][order_table] (order_stage) |
| `eda_start_time` | `Datetime` | Время старта заказа из [логов доставки заказов][order_table] (utc_start_point_fact_dttm) |
| `travel_start_time` | `Datetime`| Определённое время начала движения |
| `eda_end_time` | `Datetime` | Время завершения заказа из [логов доставки заказов][order_table] (utc_destination_arrival_fact_dttm) |
| `travel_end_time` | `Datetime` | Определённое время окончания движения |
| `eda_vehicle_type` | `String` | Тип курьера из [логов доставки заказов][order_table] (vehicle_type) |
| `movement_type` | `String` | Установленный тип движения курьера |
| `region_id` | `Int32` | Определяется для координат окончания маршрута из [логов доставки заказов][order_table] (`destination_plan_lat`, `destination_plan_lon`) |
| `num_signals_without_stupidity` | `Uint64` | Количество сигналов без стояния в начале и конце маршрута |
| `num_start_stupidity_signals` | `Uint64` | Количество сигналов на интервале между стартом заказа и началом движения |
| `num_finish_stupidity_signals` | `Uint64` | Количество сигналов на интервале между завершением заказа и концом движения |
| `num_signals_on_route` | `Uint64` | Количество сматченных сигналов (по дефолту расстояние до полилинии маршрута меньше 80 метров) для наилучшего ответа роутера |
| `signal_coverage` | `Double` | Отношение сматченных к сигналам без тупления |
| `max_delta_signals_time` | `Uint64` | Наибольшее время между парами курьерских сигналов во время движения (с уникальными `utc_created_dttm`) |
| `max_smoothed_speed` | `Double` | Наибольшая медиана в скользящем окне по сигналам во время движения, оценивается как максимальная скорость курьера |
| `min_signal_distance_to_start` | `Double` | Минимальное расстояние между сигналами и началом заказа |
| `min_signal_distance_to_finish` |`Double` |  Минимальное расстояние между сигналами и финишем заказа |
| `route_id` | `String` | ID наилучшего сматченного маршрута |
| `router_time` | `Double` | Время наилучшего маршрута из ответов роутера |
| `router_length` | `Double` | Дистанция наилучшего маршрута из ответов роутера |
| `route_distance_to_start` | `Double` | Дистанция между началом заказа и стартом выбранного машрута |
| `route_distance_to_finish` | `Double` | Дистанция между финишем заказа и концом выбранного машрута |
| `num_routers_requests` | `Uint64` | Количество всех запросов ко всем роутерам по всем ручкам за время заказа |
| `num_success_router_responses` | `Uint64` | Количество запросов в соотвествующие [определенному типу движения](#особенности-определения-типа-движения-и-выбор-подходящих-запросов-в-роутер) ручку и роутер с дистанцией меньшей 300 метров для старта и финиша у заказа и маршрута роутера |
| `num_show_bike_route_events` | `Uint64` | Количество событий просмотра маршрута на велосипеде в [логах мобильного приложения][maps_cooked_metrika_mobile_log] |
| `num_show_car_route_events` | `Uint64` | Количество событий просмотра маршрута на авто в [логах мобильного приложения][maps_cooked_metrika_mobile_log] |
| `num_show_pedestrian_route_events` | `Uint64` | Количество событий просмотра пешеходного маршрута в [логах мобильного приложения][maps_cooked_metrika_mobile_log] |
| `num_show_scooter_route_events` | `Uint64` | Количество событий просмотра маршрута на самокате в [логах мобильного приложения][maps_cooked_metrika_mobile_log] |
| `num_show_taxi_route_events` | `Uint64` | Количество событий просмотра маршрута на такси в [логах мобильного приложения][maps_cooked_metrika_mobile_log] |
| `num_show_transport_route_events` |`Uint64` |  Количество событий просмотра маршрута на общественном транспорте в [логах мобильного приложения][maps_cooked_metrika_mobile_log] |
| `num_navigation_pedestrian_started` | `Uint64` | Количесвто событий запуска пешеходного ведения в [логах мобильного приложения][maps_cooked_metrika_mobile_log] |
| `num_navigation_auto_started` | `Uint64` | Количесвто событий запуска автомобильного ведения в [логах мобильного приложения][maps_cooked_metrika_mobile_log] |
| `test_buckets` | `List(Struct(bucket:Int16, id:Int32))` | Список уникальных пар {bucket, id} по событиям из [лога мобильного приложения][maps_cooked_metrika_mobile_log] |

## Воронки по заказам

| | |
|-|-|
| `funnel_existence_travel_signals` | Воронка наличия не менее 10 сигналов с движением |
| `funnel_visit_start_and_destination` | Воронка наличия курьерских сигналов в радиусе 300 метров от старта и финиша |
| `funnel_without_holes` | Воронка для фильтрации заказов с дырками в сигналах более 120 секунд |
| `funnel_requests_to_router` | Воронка наличия запросов в роутер |
| `funnel_relevant_request` | Воронка наличия ответа роутера совпадающего по типу движения и близкого к старту и концу заказа |
| `funnel_on_route_coverage` | Воронка наличия ответа роутера с покрытием не меньшим 90% |

[order_table]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/statistics/eda_order_delivery_log
[mtroute_log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-mtroute-production-log/1d
[bicycle_log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-bicycle-production-log/1d
[maps_cooked_metrika_mobile_log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/mobile-maps

Шедулеры: https://sandbox.yandex-team.ru/schedulers?tags=prepare-eda-courier-metric
