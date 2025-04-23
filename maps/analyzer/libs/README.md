# Библиотеки анализатора

| Библиотека | Описание |
--- | ---
[`backtrace`](backtrace) | Микро-либа для вывода бектрейса исключения
[`calendar`](calendar) | Библиотека для работы с календарем рабочих дней
[`cmdline_graph`](cmdline_graph) | Парсинг аргументов командной строки для загрузки файлов графа
[`common`](common) | Различные полезные функции
[`consts`](consts) | Constants of many kinds (math, time, etc.)
[`constexpr_types`](constexpr_types) | Библиотека constexpr-типов
[`event_loop`](event_loop) | Многопоточная обработка событий / очередей на базе libevent
[`exp_regions`](exp_regions) | Библиотека для работы с наборами областей, в которых проводятся a/b эксперименты
[`external/geo`](external/geo) | Mapkit cross-compilable geometric library
[`data`](data) | Обёртки протобуфных данных
[`geoinfo`](geoinfo) | Получение региона и информации о нём по точке, geobase на coverage-костылях
[`gpssignal_parser`](gpssignal_parser) | Парсинг GPS-сигналов
[`graphmatching`](graphmatching) | Привязка точек/сигналов к графу (должна заменить [`mapmatcher`](mapmatchcer))
[`guidance`](guidance) | Ведение по маршруту
[`hgram`](hgram) | Гистограммные метрики для сервисов
[`http`](http) | HTTP
[`interval_tree`](interval_tree) | Дерево интервалов (что-то типа 1d rtree)
[`jams_level_prediction`](jams_level_prediction) | Библиотека предсказания пробочных баллов
[`jams_statistical_data_4`](jams_statistical_data_4) | Исторические статистики
[`lru_cache`](lru_cache) | LRU-кэш
[`manoeuvres`](manoeuvres) | Библиотека для работы с маневрами
[`mapmatching`](mapmatching) | Общая библиотеки привязки
[`mapmatching_likelihoods`](mapmatching_likelihoods) | Функции правдоподобия для привязки сигналов
[`masstransit`](masstransit) | Общественный транспорт
[`metrics_handler`](metrics_handler) | Логгирование метрик
[`ml`](ml) | Библиотека для описания фичей, конфига и моделей машинного обучения
[`mt_jobs`](mt_jobs) | Библиотека для многопоточного запуска мапперов и редьюсеров
[`realtime_jams`](realtime_jams) | Estimation of current speed of car flow
[`regression`](regression) | -
[`requests`](requests) | HTTP-запросы
[`rtp`](rtp) | Reschedulable Thread Pool
[`shortest_path`](shortest_path) | Кратчашие пути в графе (для [`road_graph`](/arc/trunk/arcadia/maps/libs/road_graph))
[`signal_filters`](signal_filters) | Фильтрация сигналов
[`state`](state) | Сохранение состояние [`rtp`](rtp) в протобуфном формате
[`time_interpolator`](time_interpolator) | Библиотека для усреднение времён проездов для построения пробки
[`track_generator`](track_generator) | Генератор треков
[`travel_time`](travel_time) | Types and tools for travel time manipulations
[`types`](types) | Общие типы (`TrackId`, `VehicleId`, ...)
[`udf`](udf) | Упрощение написания YQL UDF на C++
[`user_traits`](user_traits) | Характеристики водителей для ML-модели
[`utils`](utils) | Вспомогательные функции без лишних зависимостей
[`whitelist_dataset`](whitelist_dataset) | Библиотека для работы с белыми списками

# Ссылки

[Сборка под Мапкит и Аркадию](https://wiki.yandex-team.ru/users/voidex/arcadia/cross-mapsmobi-build/)
