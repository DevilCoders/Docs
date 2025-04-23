Чтение пробок из внешнего xml-формата
===

_NOTE_: по факту сейчас используется только возможность "бана" пробки.

Преобразование пробок из внешнего xml-формата ([пример](tests/data/jams.xml)) в тип [`Jams`](/arc/trunk/arcadia/maps/libs/jams/router/include/yandex/maps/jams/router/jams.h).  
Читает полилинии из xml и привязывает их к графу при помощи [`mapmatcher_geometry`](/arc/trunk/arcadia/maps/analyzer/libs/mapmatcher_geometry).  
Также умеет "банить" пробки, прописывая в указанных местах пробки со скоростями по умолчанию.  
Бинарники:
  * [`bin/convert`](bin/convert) — собственно, конвертация в нужный формат
  * [`bin/draw`](bin/draw) — отрисовка в [easyview](/arc/trunk/arcadia/maps/tools/easyview)-формате для отладки
  * [`bin/tie_upload`](bin/tie_upload) — основной скрипт; скачивает пробки в xml-формате, преобразует в `Jams`, и заливает в ecstatic

Конфиг
===

В [`conf/tie-upload.json`](conf/tie-upload.json) лежит конфиг с полями:
 * `server` — FTP-сервер
 * `user`/`password` — логин/пароль от FTP
 * `remote_file` — путь до файла с пробками на FTP
 * `regions` — фильтр по регионам, только эти регионы будут добавлены. Если список пустой - фильтр отключен.
 * `max_category` — фильтрация по максимальной категории ребра

Бан пробок
===

Файл в yson формате со список полилиний, где каждая полилиния — список из точек в формате `[lon; lat]`. Каждая геометрия приматчится, и на получившихся рёбрах будет выставлена скорость по умолчанию из графа.

Получить геометрию можно, например, при помощи [`maps/tools/naviguide/tools/leptidea_route`](/arc/trunk/arcadia/maps/tools/naviguide/tools/leptidea_route), а посмотреть на результат глазами при помощи [`maps/tools/easyview/bin`](/arc/trunk/arcadia/maps/tools/easyview/bin):
```
$ maps/tools/naviguide/tools/leptidea_route/leptidea_route --graph-version 18.12.23-0 --src-lon 30.31644952 --src-lat 60.00009412 --dst-lon 30.48950296 --dst-lat 59.94468404 > geom
$ cat geom | maps/tools/easyview/bin/easyview
...
```

Отладочный запуск
===

Можно запустить с сохранением промежуточных данных и логированием в stderr:
```
bin/tie_upload/tie_upload -c conf/tie-upload.json --ban-list conf/ban-list.yson --log /dev/stderr --output . --no-upload --convert-binary bin/convert/convert
```
В текущей директории будет создана временная директория со скачанными и преобразованными данными.  
Версия графа указывается так, как принято в [`maps/analyzer/pylibs/envkit`](/arc/trunk/arcadia/maps/analyzer/pylibs/envkit) — через указание переменной окружения `ALZ_API_GRAPH_VERSION`.

Можно запустить с сохранением промежуточных данных и логированием в stderr, с указанием конкретной дирректории для dataset-a
```
bin/tie_upload/tie_upload -c conf/tie-upload.json --ban-list conf/ban-list.yson --log /dev/stderr --output . --no-upload --convert-binary bin/convert/convert -d dataset_dir
```
В текущей директории будет создана заданная в качестве параметра директория со скачанными и преобразованными данными.  
Версия графа указывается так, как принято в [`maps/analyzer/pylibs/envkit`](/arc/trunk/arcadia/maps/analyzer/pylibs/envkit) — через указание переменной окружения `ALZ_API_GRAPH_VERSION`.
