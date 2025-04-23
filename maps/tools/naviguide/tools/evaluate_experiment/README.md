Для заданной даты и `experiment_id`:
- отфильтровать `uuid`-ы пользователей, участвовавших в эксперименте
- выбрать репорты этих пользователей
- построить по этим репортам эталоны
- запустить симуляцию в `naviguide`
- посчитать качество `navimatcher_quality` и `route_quality`

## Запуск
```bash
./evaluate_experiment -f 2020-02-20 -t 2020-02-25 -e 192209 -o //home/maps/jams/dev/users/<USER>/route_quality_simulations --daily-reports //home/maps/jams/dev/users/<USER>/navigator-user-report/daily-reports --graph-folder //home/maps/jams/dev/users/<USER>/production/graph
```

### Параметры
- `-f 2020-02-20` - дата начала эксперимента
- `-d 2020-02-25` - дата конца эксперимента (по дефолту равна `-f`)
- `-e 192209` - номер эксперимента
- `-o //home/maps/jams/dev/users/<USER>/route_quality_simulations` - папка, в которой создадутся папки `etalons_2020-02-19_192209` (`uuid`-ы, эталоны, эвенты, ...) и `evaluation_2020-02-19_192209` (симуляция, `navimatcher-quality` и `route-quality`)
- `--daily-reports //home/maps/jams/dev/users/<USER>/navigator-user-report/daily-reports` - путь до папки `daily-reports` (по дефолту `//home/navigator-user-report/daily-reports`)
- `--graph-folder //home/maps/jams/dev/users/<USER>/production/graph` - путь до папки с графами (по дефолту `//home/maps/graph`)
- `-v 20.02.28-0` - версия графа (по дефолту она берётся из атрибута `//home/maps/jams/production/data/unsplit_assessors/<DATE>/@graph_version` для выбранной даты)
