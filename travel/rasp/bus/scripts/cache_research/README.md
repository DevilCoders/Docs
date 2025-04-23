# Cache research

## Построение файла с логами

запрос: https://yql.yandex-team.ru/Operations/XpA8C2Hljg5KJLXPaR5GN01qzeOqSVrbV1KkzaXmgkM=
Пример запроса
```
USE hahn;

SELECT request, `datetime`
from `home/logfeller/logs/qloud-router-log/1d/2019-07-10`
WHERE qloud_application == 'api'
  AND qloud_project == 'yandex-bus'
  AND qloud_environment == 'production'
  AND qloud_instance like "meta%"
  AND request like "%/rides/search%"
  AND request not like "%cache-only=true%"
ORDER  BY `datetime`;
```
Чтобы сохранить, нужно выбрать вкладку Full results -> Download -> Json

## Структура конфига для warmer'а
```{
    "k_cache_age": <cache age coefficient>,
    "k_days_before_ride": <days before ride coefficient>,
    "rps_restrictions": {
        <supplier>: <rps restriction value for supplier>
    },
    "warmer_top_size": <number of directions in the top>,
    "warmer_analyse_time": <time during which warmer collects statistics and warms up directions>,
    "warmer_calendar_depth": <number of days to warm up>
}
```

## Построение графиков
Нужно собрать бинарник и запустить, указав в параметрах:
- путь до файла с логами, параметр --file
- путь до конфига warmer'а, параметр -w
- путь, куда сохранить графики, параметр --path (по умолчанию текущая директория)
- ttl, параметр --ttl в минутах (по умолчанию ttl=60)
- квантоание в минутах, --norm (по умолчанию norm=15)

Пример
```
./cache_research --ttl <ttl> --norm <norm> --file <file name> --path <path> -w <file name>
```
