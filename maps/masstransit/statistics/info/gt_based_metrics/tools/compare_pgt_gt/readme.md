### Назначение
Требуется оценить качество построенного Pseudo Ground Truth (PGT) на основе Ground Truth (GT). Результат записывается на YT.

### Входные и выходные данные
Входные данные содержат две таблицы. Первая - с сигналами GT (колонки `gtid`, `timestamp`, `lon` и `lat`, отсортированные по `gtid`, `timestamp`). Вторая - с PGT, построенным по сигналам, соответствующим этому GT (колонки `gtid`, `trip_id`, `timestamp`, `lon` и `lat`, отсортированные по `gtid`, `trip_id`, `timestamp`).

Результатом является таблица с одной строкой, содержащая статистические данные о дистанционных ошибках между траекториями GT и PGT.\
`distance_error_avg` - средняя ошибка;\
`distance_error_prc_<n>` - `n`-й процентиль. Означает, что у `n`% треков (траекторий с одинаковым `gtid`) дистанционная ошибка не превосходит значения в колонке `distance_error_prc_<n>`.

### Пример запуска
```
./compare_pgt_gt --gt-path //home/yatransport/mtinfo-metrics/gt/processed/2019-07-09 --pgt-path //home/yatransport/mtinfo-metrics/pgt/2d/2019-07-09 -o //home/yatransport/mtinfo-metrics/analyzer/pgt-gt/2019-07-09
```
