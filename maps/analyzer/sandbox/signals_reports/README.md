Отчёты по сигналам
===

Регулярный процесс подготовки статистик по партнёрским сигналам.

Исходные данные — приматченные сигналы (см [`prepare_matched_data`](/arc/trunk/arcadia/maps/analyzer/sandbox/prepare_matched_data)).

Готовит суточные статистики группируя по `clid`ам и регионам:
 * Cигналы — хорошие сигналы (`reason_id` равен `null`), а также остальные сигналы сгруппированные по `reason_id`
 * Плохие/хорошие `uuid`ы по регионам, где `uuid` считается хорошим, если есть хотя бы один "хороший" (приматченный) сигнал
 * Количество заканчивающих трек сигналов
 * Длительность треков по времени
 * Длина треков

### Шедулеры

[Тестинг&Продакшн](https://sandbox.yandex-team.ru/schedulers?task_type=JAMS_SIGNALS_REPORTS&limit=20)<br>

### Результаты

[Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/signals-reports/clid_region_stats)<br>
[Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/signals-reports/clid_region_stats)

### Скачать отчёты

Скачать результаты локально в формате `csv` можно с помощью бинарника [`bin/download_reports`](bin/download_reports). Пример запуска:
```bash
$ bin/download_reports/download_reports --begin-date 2018-01-01 --geobase <path_to_geobase> --output .
```
Скачает дневные статистики в текущую директорию (создаст поддиректорию `clid_region_stats`) начиная с `2018-01-01` и до последнего доступного дня.
