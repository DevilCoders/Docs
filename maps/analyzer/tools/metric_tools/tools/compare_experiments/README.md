Тулза для сравнения результатов экспериментов (как online, так и offline).

---

На вход принимает:
- `--stats-pool`: путь на YT до папки с stats. [Пример](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/jams/production/online-eta-quality/route_stats&)
- `--begin`, `--end` - дни, для которых нужно сделать подсчет
- `--group-by` - колонки в stats табличках, по которым треки будут группировываться и для каждой такой группы будет подсчитано сравнение экспериментов.
- `--select-group` - имена моделей, результаты которых надо сравнить (можно как id, так и имя).
- `--control` - контрольная моделей, с которой будет производиться сравнение.
- `--use-mixed` - флаг, при наличии которого будут использоваться строки с несколькими значениями в колонке "experiments" (актуален только для online-таблиц).
- `--output` - путь на YT, куда нужно сохранить результаты. Перезапишет таблицу, если уже она есть.


Необходимо запускать из папки [pkg](maps/analyzer/tools/metric_tools/pkg), пример:
`./maps/analyzer/tools/metric_tools/tools/compare_experiments/compare_experiments -s "//home/maps/jams/production/online-eta-quality/route_stats" -b 2020-05-22 -e 2020-05-28 -g length_group region_id --select-group no_minor_roads_experiment no_minor_roads_control -o "//home/maps/jams/dev/users/yourusername/result" -c no_minor_roads_control`
