Регулярные процессы
===

Здесь собраные регулярные процессы, запускаемые по расписанию в [sandbox'е](https://sandbox.yandex-team.ru) при помощи [специальной таски](/arc/trunk/arcadia/sandbox/projects/maps/AnalyzerRegularYtProcess) ([шедулеры в sandbox'е](https://sandbox.yandex-team.ru/schedulers?page=1&pageCapacity=20&order=-id&task_type=ANALYZER_REGULAR_YT_PROCESS&limit=100), [таски в sandbox'е](https://sandbox.yandex-team.ru/tasks?page=1&pageCapacity=20&forPage=tasks&type=ANALYZER_REGULAR_YT_PROCESS&recipients=)), а также [sedem-managed](https://docs.yandex-team.ru/sedem/services/sandbox) регулярные процессы

См. тулзу [sandboxy](/arc/trunk/arcadia/maps/analyzer/tools/sandboxy) для чтения параметров и обновления ревизий запускаемых задач через консоль.

| Процесс | Описание | Ссылки | sedem-managed |
--- | --- | --- | ---
[`ab_tables_daily`](ab_tables_daily) | Готовит таблицы для метрик проезда в экспериментах | Результаты в [тестинге](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/ab-tables-daily), [продакшне](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/ab-tables-daily) |
[`build_calendar`](build_calendar) | Построение и загрузка календаря в ecstatic | ecstatic в [продакшене](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-calendar/versions), [тестинге](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-calendar/versions) |
[`data_freshness`](data_freshness) | Проверка свежести метрик, моделей и датасетов | - |
[`eta_prediction`](eta_prediction) | Папка, в которой собраны процессы, связанные **только** с подсчетом данных (или их изменений) для предсказания времени (поездки) | см. [`eta_prediction`](eta_prediction/README.md) |
[`generate_statistical_data`](generate_statistical_data) | Генерация статистических данных для моделей предсказания времени (ETA поездки и движение ОТ) |  Результаты для пробочных скоростей в [тестинге](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams_statistical_data), [продакшне](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams_statistical_data); результаты для скоростей движения ОТ в [тестинге](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/statistical_data), [продакшне](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/statistical_data) |
[`infopoints_hourly`](infopoints_hourly) | <<Яндекс врёт>> в разговорчиках | Результаты в [тестинге](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/infopoints_hourly/metrics), [продакшне](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/infopoints_hourly/metrics). [Панель на дашборде](https://datalens.yandex-team.ru/5q70qk3wf8ww2-probki?tab=eWd) |
[`jams_level_prediction`](jams_level_prediction) | Регулярные процессы сервиса предсказания пробочных баллов | см. [`jams_level_prediction`](jams_level_prediction/README.md) |
[`masstransit`](masstransit) | Папка, в которой собраны процессы, связанные с предсказанием движения общественного транспорта | - |
[`navi_metrics_daily`](navi_metrics_daily) | Метрики Навигатора | Результаты в [тестинге](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/navi-metrics-daily), [продакшне](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/navi-metrics-daily). [Панель на дашборде](https://datalens.yandex-team.ru/5q70qk3wf8ww2-probki?tab=aEq) |
[`prepare_matched_data`](prepare_matched_data) | Подготовка данных, связанная с привязкой сигналов к графу - сигналов, треков | [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data), [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data) |
[`prepare_matched_routes`](prepare_matched_routes) | Подготовка данных, связанная с привязкой маршрутов к графу. На данный момент привязываются только маршруты пользователей, для которых нашлись события установки маршрута от навигатора | [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data), [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data) |
[`retain_graphs`](retain_graphs) | Продление жизни графов на YT в архивных целях | [Графы](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/graph) |
[`route_quality`](route_quality) | Оценка качества маршрутов | Результаты в [тестинге](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/route-quality), [продакшне](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/route-quality). [Панель на дашборде](https://datalens.yandex-team.ru/5q70qk3wf8ww2-probki?tab=PaQ) |
[`signals_reports`](signals_reports) | Отчёт по сигналам партнёров | Данные в [тестинге](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/signals-reports/clid_region_stats), [продакшне](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/signals-reports/clid_region_stats) | ✓
[`update_historic_jams`](update_historic_jams) | Обновление исторических пробок | Результаты в [тестинге](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data/historic_jams), [продакшне](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/historic_jams) |
[`prepare_router_events`](prepare_router_events) | Получение событий из логов роутера | Результаты в [тестинге](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data/router), [продакшне](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/router) |

Данные
===

Так как при подготовке разного типа данных нужны знания о "завтра", результаты появляются с задержкой. Краткое описание, когда данные уже есть, и причин отставания:

| Данные | Кто создаёт | Ссылки | -4 | -3 | -2 | Вчера | Сегодня | Примечание |
--- | --- | --- | --- | --- | --- | --- | --- | ---
Логи навигатора | | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/logs/cooked-metrika-mobile-log/navi) | ✓| ✓ | ✓ | ✓\* | | Логи навигатора, как правило появляются за предудыщий день около 5 утра. По этой причине матчинг должен запускаться после 5 утра, иначе этих голов ещё не будет
Логи мобильных карт | | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/logs/cooked-metrika-mobile-log/mobile-maps) | ✓| ✓ | ✓ | ✓\* | | Логи морбильных карт, создаются аналогично логам навигатора
Логи роутера | | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-route-geometry-log) | ✓| ✓ | ✓ | ✓ | Частично | Пишутся потоком
Логи заказов такси | | [Продкашн](https://yt.yandex-team.ru/hahn/navigation?//home/taxi-dwh/public/maps/order) | ? | ? | ?  | ? | ? | |
 | | | | | | | |
Логи сигналов | [Диспатчер](/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer/modules/dispatcher) через логброкер | [Продкашн](https://yt.yandex-team.ru/hahn/navigation?path=//logs/analyzer-dispatcher-signals-log) | ✓ | ✓ | ✓ | ✓ | Частично | Логи сигналов, пишутся потоком, разбиваются по дням согласно локальному времени
Сессии, пинги, события из навигатора | [`navi_metrics_daily`](navi_metrics_daily) | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/navi-metrics-daily), [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/navi-metrics-daily) | ✓ | ✓ | ✓ | ✓\* | | Зависят от логов навигатора, которые появляются в 5 утра, плюс сами вносят задержку, так что данные за "вчера" появляются сегодня днём
Сигналы | [`prepare_matched_data`](prepare_matched_data) | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/signals), [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data/signals) | ✓ | ✓ | ✓ | * | | Сконвертированные сигналы. (\*) не хранятся, но могут быть созданы; используются при матчинге асессоров
Пробочные проезды (travel times) | [`prepare_matched_data`](prepare_matched_data) | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/travel_times), [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data/travel_times) | ✓ | ✓ | | | | Привязанные сигналы с "пробочным" конфигом. Создаются одновременно с асессорами, ограничиваются ими, хотя могут быть созданы из сигналов за "сегодня"
Асессоры | [`prepare_matched_data`](prepare_matched_data) | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/assessors), [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data/assessors) | ✓ | ✓ | | | | Поездка может оканчиваться "завтра", а для нарезки требуются события навигатора, потому отстают от сессий/пингов на день. Матчинг запускается ночью, так что вчерашние события ещё не застаёт
Асессоры с пробками для машинного обучения | [`prepare_training_tracks`](prepare_training_tracks) | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/training_tracks), [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data/training_tracks) | ✓ | | | | | Для добавления пробок к асессорам нужны пробки за "завтра", потому отставание от асессоров на день
Трейн-пулы для для машинного обучения | [`prepare_training_pools`](prepare_training_pools) | [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data/training_tracks), [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/training_tracks) | ✓ | | | | | зависят от задачи подготовки асессоров с пробками
Маршруты | [`prepare_matched_routes`](prepare_matched_routes) | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data), [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data) | ✓ | | | | | Зависят от асессоров, логов роутера и заказов такси
События роутера | [`prepare_router_events`](prepare_router_events) | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/router/events), [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data/router/events) | ✓| ✓ | ✓ | ✓ | Частично | Зависят от логов роутера
События роутера для нарезки ассесоров | [`prepare_router_events`](prepare_router_events) | [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/router/events_log), [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/data/router/events_log) | ✓| ✓ | ✓ | ✓ | Частично | Зависят от логов роутера

В метриках могут требоваться маршруты и асессоры с пробками, так что они будут отставать в лучшем случае на 4 дня.

Очистка временных папок в yt
==
Регулярные процессы в ходе своей работы создают временные таблицы в папках `//home/maps/jams/{env}/tmp`. Есть 2 механизма очистки таких таблиц:
- их перечень запоминается в YtContext и потом они явно удаляются
- им выставляется атрибут `expiration_time` в неделю, после чего они сами удалятся YT.

YQL-запросы, перезаписывающие таблицы с помощью `INSERT INTO WITH TRUNCATE` сбрасывают их атрибуты, в т.ч. и `expiration_time`. Поэтому в случае аварийного завершения процесса, они не удаляются: контекст не очищается, а атрибут сброшен.
Чтобы этого избежать, был придуман третий механизм в виде ежедневного процесса удаляющего старые таблицы. [Описание](https://yt.yandex-team.ru/docs/description/common/regular_system_processes#tmp_cleaning) процесса в документации.


| Окружение | Максимально допустимый возраст таблиц в папке (max-age) |
--- | ---
| [Продакшн](https://sandbox.yandex-team.ru/scheduler/697989/view) | 30 дней |
| [Тестинг](https://sandbox.yandex-team.ru/scheduler/697988/view) | 30 дней |
