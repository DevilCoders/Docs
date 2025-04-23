# core jams external

<b>UPDATE: </b>
Сервис выключен, все данные удалены, ресурсы освобождены. Тикет закрытия сервиса: https://st.yandex-team.ru/MAPSJAMS-3316

В директории [`garden/modules`](garden/modules) лежат Огородные модули, относящиеся к сервису.

---

Получает пробочные данные от партнёров, например скачивает и преобразует пробки раз в N секунд.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Андрей Попов (andrew-pov@yandex-team.ru) <br> Александр Ручкин (voidex@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/services/jams_external <br> https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/libs/tie_here_jams |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-jams-external/ |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable |  |  |  |
| Testing | [maps_core_jams_external_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_external_testing/) | [ core-jams-external.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-jams-external-testing-panel-main/) | [ maps_core_jams_analyzer_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_analyzer_testing) |

## Additional information

Парсинг пробок HERE (в xml-формате) и загрузка в ecstatic
===

Чтение полилиний улиц HERE, привязывание их к графу и сохранение их в .mms формате
Преобразование пробок из внешнего xml-формата в тип [`Jams`](/arc/trunk/arcadia/maps/libs/jams/router/include/yandex/maps/jams/router/jams.h).
Читает полилинии из xml и привязывает их к графу при помощи [`matchGeometry`](/arc/trunk/arcadia/maps/analyzer/libs/graphmatching/include/match_geometry.h).

Сервис состоит из двух частей:
  * Огородный модуль [`tie_here_graph`](/arc/trunk/arcadia/maps/garden/modules/tie_here_graph) привязывает полилинии HERE к графу, создаёт mms-файлы и загружает их в экстатик.
  * Онлайн-сервис по крону скачивает пробки HERE в xml-формате, с помощью mms-ок из огородного модуля конвертирует их в `Jams` и загружает в экстатик готовый датасет с пробками от партнёров

Бинарники:
  * [`bin/tie_upload`](bin/tie_upload) — основной скрипт; скачивает пробки в xml-формате, берёт готовые .mms файлы матчинга полилиний HERE в граф, конвертирует пробки в `Jams`, и заливает в ecstatic
  * [`bin/convert`](bin/convert) — конвертация xml в пробки `Jams`. Выполняет конвертацию в отдельном потоке для каждой страны

  * [`bin/draw_here_jams`](bin/draw_here_jams) - отрисовка в [easyview](/arc/trunk/arcadia/maps/tools/easyview)-формате для отладки

  * [`bin/tie_graph`](bin/tie_graph) — скрипт привязывания полилиний HERE к графу; читает shapefile-ы HERE (Streets.shp, Streets.shx, Streets.dbf и Traffic.dbf), собирает из них полилинии, матчит их к графу и сохраняет результат в .mms файлы (по одному файлу для каждой страны). Запускает матчинг в отдельном процессе для каждой страны.
P.S. Этот скрипт полностью повторяет то, что происходит в огродном модуле. Можно использовать, если нужно что-то собрать руками или для теста.
  * [`bin/match_tmc_to_graph`](bin/match_tmc_to_graph) — матчинг одного конкретного региона и сохранение mms. Формат mms можно посмотреть здесь: [`tmc_storage.h`](/arc/trunk/arcadia/maps/analyzer/libs/tie_here_jams/include/tmc_storage.h)


Конфиги
===

В [`conf/tie-upload.json`](conf/tie-upload.json) лежит конфиг с полями:
 * `user`/`password` — логин/пароль для скачивания xml-файла с пробками
 * `tied_graph_files` — для каждого региона путь до mms-файла с приматченными полилиниями
 * `here_urls` — для каждого региона http-url для скачивания xml-файла с пробками

В [`conf/tie-graph.json`](conf/tie-graph.json) лежит конфиг с полями:
 * `regions` — возможные регионы для приматчивания к графу. Это просто список разрешённых регионов, какие из них на самом деле будут матчиться зависит от параметров запуска бинарника
 * `regions/<region_name>/input_directories` — список директорий, в которых лежат полилинии HERE. Важно, чтобы соответсвующие друг другу Traffic.* и Streets.* файлы были в одной директории
 * `regions/<region_name>/location_table_id` — id таблицы полилиний для региона. В файле Streets могут лежать улицы нескольких таблиц, но пробки предоставляются только для одной из таблиц, так что остальное мусор
 * `regions/<region_name>/output_file` — путь до выходного .mms файла


Бан пробок
===

Файл в yson формате со списком полилиний, где каждая полилиния — список из точек в формате `[lon; lat]`. Каждая геометрия приматчится, и на получившихся рёбрах будет выставлена скорость по умолчанию из графа.

Получить геометрию можно, например, при помощи [`maps/tools/naviguide/tools/leptidea_route`](/arc/trunk/arcadia/maps/tools/naviguide/tools/leptidea_route), а посмотреть на результат глазами при помощи [`maps/tools/easyview/bin`](/arc/trunk/arcadia/maps/tools/easyview/bin):
```bash
$ maps/tools/naviguide/tools/leptidea_route/leptidea_route --graph-version 18.12.23-0 --src-lon 30.31644952 --src-lat 60.00009412 --dst-lon 30.48950296 --dst-lat 59.94468404 > geom
$ cat geom | maps/tools/easyview/bin/easyview
...
```
Этот yson файл можно передавать с параметром `--ban-list` в скрипт `tie_upload`


Запуск
===

Скрипт [`tie_upload`](bin/tie_upload) можно запустить с сохранением промежуточных данных и логированием в stderr:
```bash
bin/tie_upload/tie_upload -c conf/tie-upload.json -l /dev/stderr -n -b bin/convert/convert -r France CzechRepublic Finland Slovenia SouthAfrica UK Poland -o tmp --ban-list conf/ban-list.yson
```
В текущей директории будет создана временная директория со скачанными и преобразованными данными.

Скрипт [`tie_graph`](bin/tie_graph) можно запустить, например, так
```bash
bin/tie_graph/tie_graph --c conf/tie-graph.json -l /dev/stderr -r France Finland Slovenia SouthAfrica UK Poland CzechRepublic -b bin/match_tmc_to_graph/match_tmc_to_graph
```
Важно понимать, что для некоторых регионов скрипт работает небыстро (максимум ~25 минут для Франции, например). Если его прервать на середине выполнения, то все изменяемые mms-файлы станут невалидными. Суммарно (для регионов, перечисленных в примере) все выходные файлы занимают ~500MB

Для бинарников [`bin/convert`](bin/convert) и [`bin/match_tmc_to_graph`](bin/match_tmc_to_graph) версия графа указывается так, как принято в [`maps/analyzer/pylibs/envkit`](/arc/trunk/arcadia/maps/analyzer/pylibs/envkit) — через указание переменной окружения `ALZ_API_GRAPH_VERSION`.

У всех скриптов и бинарников есть параметр --debug, добавляющий тонну отладочного вывода в логирование. Если скрипт запущен с --debug, то бинари, которые он запускает внутри себя, тоже будут запущены  с --debug.
