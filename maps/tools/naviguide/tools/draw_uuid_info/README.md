# Отрисовка логов (сигналы, треки, маршруты)

Тулза предназначена для отрисовка скачанных сигналов, треков и маршрутов из логов при помощи [`tools/extract_uuid_info`](/arc/trunk/maps/tools/naviguide/tools/extract_uuid_info).

```bash
$ ./tools/extract_uuid_info/extract_uuid_info ... -o output
...
$ cat output/data/* | ./tools/draw_uuid_info/draw_uuid_info -e events.yson > debug.ev
```

Если указать параметром `--events` (`-e`) события отчёта, то тулза оставит только те данные, которые попадает в её временной диапазон, чтобы не рисовать лишнего. Если не указать — отрисует всё.
