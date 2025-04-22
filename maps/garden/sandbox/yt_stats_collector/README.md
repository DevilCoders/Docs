# Описание
Приложение предназначено для сбора статистических данных об огородных YT операциях для возможности последующей визуализации и оффлайн анализа.

Приложение состоит из двух логических компонент: парсер логов YT и генератор данных для визуализации статистики.

## Парсер логов
Исходные данные для приложения - таблицы с логами YT `//logs/yt-scheduler-logs/1d`.

Последовательность действий парсера:
* Фильтрует данные, соответствующие событиям окончания операций и `fair_share_info` планировщика
* Выбирает только данные, относящиеся к пулам Огорода (из `libs_server/task/yt_pool_impl.h`)
* Раскладывает результаты по 3-м папкам:
  * task_operation - провязки operation_id к идентификаторам тасок
  * operation_snapshot - представление YT scheduler о запущенных garden операциях (снапшоты примерно раз в 10 секунд)
  * pool_snapshot - представление YT scheduler о garden пуле

Информация для snapshot представлений получается из логов типа `fair_share_info` (https://yt.yandex-team.ru/docs/other/event_logs#fair_share_info).

Для изначальной фильтрации таблиц с логами YT был написан mapper на C++, т.к. ожидалось, что он будет рабоать быстрее, чем на python.
Однако это оказалось [не так](https://st.yandex-team.ru/YTADMINREQ-26857). Возможно в будущем проблему пофиксят, но пока фильтрация одной таблицы занимает около 30 минут.

## Генератор статистики
Запускается серия YQL скриптов, каждый из которых формирует свой срез агрегированной статистики. Результат выполнения - таблицы на YT.

Создаются серии таблиц с разбиением по дням:
* resource_consumption_module_series
* resource_consumption_task_series
* yt_alerts_series
* yt_pool_usage_module_series
* yt_pool_usage_operation_type_series
* yt_pool_usage_task_series

# Сборка
При изменении кода приложения CI автоматически запускает сборку бинарника в проекте [garden](https://a.yandex-team.ru/projects/maps-core-garden/ci/actions/launches?dir=maps%2Fgarden%2Fsandbox%2Fyt_stats_collector&id=build).

# Тестирование
Собрать бинарник локально или скачать из sandbox. Запускать при помощи команды
```
./GARDEN_YT_STATS_COLLECTOR run --enable-taskbox --type GARDEN_YT_STATS_COLLECTOR --create-only
```
После этого будет создана таска в sandbox, в которой нужно будет выставить правильный параметр "Environment type" и запустить её.

# Релиз
Релиз производится через sedem.

Sedem [автоматически создаёт](https://docs.yandex-team.ru/sedem/services/sandbox) sandbox scheduler который можно [найти тут](https://sandbox.yandex-team.ru/schedulers?created=14_days&limit=20&offset=0&owner=MAPS_GARDEN)
В результате выполнения задачи результаты данные запишутся на Hahn в `//home/maps/core/garden/stats`

# Графики
Все графики доступны со страницы дашборда статистики https://dash.yandex-team.ru/rlc80mom129go.
И со страницы дашборда модуля https://datalens.yandex-team.ru/d53hr6hdox6s6-module?module_name=example_map.
