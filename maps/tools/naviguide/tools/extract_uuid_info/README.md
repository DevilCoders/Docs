Тулза позволяет по `uuid` из логов достать версию библиотеки привязки, а также конфиг с учётом запущенных экспериментов.

Примет запуска
```bash
$ extract_uuid_info/extract_uuid_info -u $UUID -f 2019-11-14 -t 2019-11-16 -o out
```

В директорию `out` будет положен конфиг `config.yson`, например, такой:
```
{
    "_VERSION" = "0.1.13-0";
    "_EXPERIMENTS" = [
        22023,
        121001
    ];
    "ENABLE_FAIR_HEADING_CHECK" = "1";
    "IGNORE_HEADING_WHEN_SLOWER" = "4";
    "IGNORE_STOPS_IN_SMOOTH_CHECK" = "1";
    "POSITION_ON_ROUTE_BONUS_WEIGHT" = "20";
    "GPS_HEADING_ERROR_STDDEV" = "6";
    "DEFAULT_CLING_DISTANCE" = "40";
    "GPS_POSITION_ERROR_STDDEV" = "8";
    "MIN_MOVEMENT_SPEED" = "0.1";
    "IGNORE_LAST_SEQUENCE_IN_SMOOTH_CHECK" = "1";
}
```

Также в логи будет выведена краткая информация о влияющих экспериментов (заголовок, автор, ссылки на AB, тикет).<br>
Помимо этого можно указать флаг `--data`, чтобы получить данные из логов:
* сигналы (`data/signals.yson`)
* треки (`data/track.TRACK_START_TIME.yson`)
* маршруты (`data/routes.yson`)

Все логи (сигналы, треки, маршруты) кладутся в отдельную директорию, чтобы можно было их скопом преобразовать в [easyview](/arc/trunk/maps/tools/easyview)-анимацию одной командой:
```bash
$ cat output/data/* | ./draw_uuid_info/draw_uuid_info > data.ev
```

В поле `_VERSION` записана версия библиотеки, полученная из логов.<br>
В поле `_EXPERIMENTS` — эксперименты, влияющие на пользователя.<br>
Если передать также аргумент `--merged`, то в конфиг добавятся параметры из конфигов соответствующих версий, и т.о. версию можно будет не указывать при передаче в `naviguide`, так как параметры будут явно выставлены все.
