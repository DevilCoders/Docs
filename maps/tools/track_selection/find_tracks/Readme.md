## tracks_finder

Утилита для поиска треков, которые матчер строит неправильно


##Логика

Мы берем "сырые" сигналы, матчим их 2мя конфигами матчера и смотрим на места, где они построили разные сегменты. Мы берем сегмент, который построил ровно один из матчеров и строим какие-то метрики и если они нам нравятся, то мы обрезаем трек до интересного фрагмента и заносим в таблицу всю информацию об этом фрагменте
## Как запускать:
Есть 3 способа это сделать:

1)В аргументе --table-name указать путь до таблицы с сигналами. Таблица должна иметь схему как здесь: //home/maps/jams/production/signals тогда она заматчится с помощью двух конфигов матчера которые можно указать в аргументах --config-one --config-two дефолтные значения которых OFFLINE и ONLINE соответственно (имена конфигов можно посмотреть в [maps/analyzer/pylibs/graphmatching/conf](/arc/trunk/arcadia/maps/analyzer/pylibs/graphmatching/conf/__init__.py)) также в аргументе --graph-version можно указать версию графа, если ее не указать, то будет взята версия графа из таблицы input-table(или ошибка, если у нее не указана версия графа)
2) В аргументе --tables указать таблицу с сигналами и 2 таблицы с замaтченными треками
3) В аргументе --date указать дату, например 2019-09-09 и тогда обработаются таблицы //home/maps/jams/production/signals/[date] //home/maps/jams/production/assessors/[date] //home/maps/jams/production/travel_times/[date]

Есть опциональные аргументы --eps-len и --eps-time отвечающие за то, каким будет интересный фрагмент: в интересный фрагмент попадают сигналы и сегменты которые не дальше чем на eps-len метров дальше интересного сегмента и разница между временем проезда через интересный сегмент и этот сигнал(сегмент) не больше eps-time

###Метрики

МЫ нашли сегмент, который построил ровно один из матчеров, выбрали сегменты, которые расположены недалеко от него и через которые автомобилист проехал не так давно(за это отвечают аргументы --eps-len и --eps-time) и назвали это фрагментом. Дальше смотрим на:
```
1)Суммарная длина сегментов в фрагменте хотя бы у одного из конфигов матчера >= 180
2)Для каждого конфига матчера нет разрывов(колличество разных track_start_time == 1)
3)Суммарная длина трека с этим track_start_time > 5000(Мы не хотим давать толокерам много приватных данных)
```
Если все выполняется, то фрагмент нам нравится

### Help
```
./tracks_finder --help

Usage: tracks_finder [OPTIONS]

Options:
  --only-signals TEXT   table where we search bad tracks
  --output-table TEXT   table with result  [required]
  --config-one TEXT     first config of matcher
  --config-two TEXT     second config of matcher
  --eps-len FLOAT       radius of picture in meters
  --eps-time FLOAT      max difference in seconds between intresting moment
                        and other painted moment
  --max-accuracy FLOAT  max accuracy in intresting moment in metres
  --date TEXT           use --tables //home/maps/jams/production/data[signals
                        |travel_times | assessors] + date
  --signals-table TEXT  table with signals, --left-result and --right-result
                        are required
  --left-result TEXT    table with matched signals, --signals-table and
                        --right-result are required
  --right-result TEXT   table with matched signals, --left-result and
                        --signals-table are required
  --graph-version TEXT  available graph version
  --help                Show this message and exit.
```
