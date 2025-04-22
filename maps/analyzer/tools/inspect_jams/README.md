Inspect jams
===

Простая тулза для отрисовки пробок в заданном bbox или без него 
Принимает файлы пробок (протобуф) и может принимать координаты bbox'а, отдаёт результат в yson-формате, пригодном для отрисовки при помощи [`maps/tools/easyview`](/arc/trunk/arcadia/maps/tools/easyview)
Кроме этого вывод содержит информацию о пробках приближенную к расчитанным


Примеры:
```
$ ./inspect -t 31.999743 -l 34.871864 -b 31.998015 -r 34.874461 --easyview jams.pb jams2.pb | ~/arcadia/maps/tools/easyview/bin
$ ./inspect --easyview jams.pb jams2.pb | ~/arcadia/maps/tools/easyview/bin
$ ./inspect -t 31.999743 -l 34.871864 -b 31.998015 -r 34.874461 jams.pb jams2.pb | yt write //tmp/table --format yson
$ ./inspect jams.pb jams2.pb| yt write //tmp/table --format yson

```
