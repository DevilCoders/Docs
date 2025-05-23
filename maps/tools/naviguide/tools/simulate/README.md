# Локальный запуск симуляции на одном блобе

Читает блоб и запускает на нём [`naviguide`](/arc/trunk/arcadia/maps/tools/naviguide/bin/main.cpp)

Быстрый запуск:
```bash
$ cat blob | ./simulate/bin/simulate -c ../conf/naviguide.cfg
$ cat result.ev | ../../easyview/bin/easyview
```

Если нужно запустить [`naviguide`](/arc/trunk/arcadia/maps/tools/naviguide/bin/main.cpp) в режиме использования маршрутов из прода:
```bash
# достаём маршруты и треки из прода
$ ./extract_uuid_info -u uuid -f 2020-02-20 -o out --data
# запускаем симуляцию
# конфиг и продакшнвые данные возьмутся из `out`
$ cat blob | ./simulate/bin/simulate --user-info out
# нарисуем результат с продакшновыми данными
$ cat result.ev prod.ev | easyview
# запустим с выводом отладочной информацией (состояние слоёв алгоритма привязки)
$ cat blob | ./simulate/bin/simulate --user-info out --debug
# нарисуем результат
$ cat *.ev | easyview
```

Структура директории с результатами (расширение `.ev` значит, что можно отрисовать с помощью [`easyview`](/arc/trunk/arcadia/maps/tools/easyview)):
* `result.ev` - результат симуляции
* `debug.ev` - отладочный вывод (состояния слоёв, кандидатов)<br>
    **NOTE**: если хочется не рисовать кандидатов дабы не перегружать easyview, можно их отфильтровать с помощью `grep -v candidates`, оставив таким образом только входные сигналы
* `stderr` - stderr бинарника симулятора
* `prod.ev` - продакшновые маршруты/эталоны и пробочные сигналы, обрезанные по принадлежности к этому отчёту
* `events.yson` - входные события в виде yson-объектов (если на вход был подан блоб); их можно также подавать на вход с флагом `--events`

Основные параметры:
* `-i/--input` — файл с блобом/репортом (`/dev/stdin` by default)
* `-o/--output` — выходной файл (`/dev/stdout` by default)
* `-c/--config` — путь до конфига навигайда. Все конфиги лежат [`здесь`](/arc/trunk/arcadia/maps/tools/naviguide/conf)
* `--version` — версия симулятора (по факту — базовый конфиг, бывший основным в момент релиза, поверх которого применяется переданный)
* `--routes` — путь до файла с продовскими маршрутами
* `--etalons` — путь до файла с продовскими треками (повторяемый параметр)


Дополнительные параметры:
* `--report` — если входные данные - это строка из YT таблицы с репортом, то достать блоб по ключу "report"
* `--events` — выходные данные - yson-объекты с локейшнами и запросами маршрутов
* `--decode` — если блоб закодирован в base64
* `--graph-folder` — кастомный путь до графа (если дефолтный `/usr/share/yandex/graph` не подходит)
* `--debug` — запустить naviguide в дебаг-режиме.
