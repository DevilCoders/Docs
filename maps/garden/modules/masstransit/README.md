# masstransit


## Общее описание модуля

Модуль агрегирует собранные другими модулями статические данные общественного транспорта, пешеходный граф, а также варит по ним следующие данные:
* привязки остановок к пешеходному графу (используется плюсовая утилита [build_stops_binding](https://a.yandex-team.ru/arc_vcs/maps/masstransit/tools/data_build/build-stops-binding))
* пересадки между остановками одной компоненты (используется питоновский биндинг к библиотеке [build_pedestrian_transfers](https://a.yandex-team.ru/arc_vcs/maps/masstransit/tools/data_build/build_pedestrian_transfers/pylib))

Модуль также загружает ресурсы с вышеуказанными данными в YT, ecstatic и sandbox.


## Потребители данных

Модуль варит дополнительные данные для пешеходного графа, см. потребителей модуля `pedestrian_graph`.
Модуль также загружает данные (в YT, ecstatic и Sandbox), сваренные модулем `masstransit_static`, см. потребителей модуля `masstransit_static`.


## Входные данные

Ресурсы входных данных подготавливаются модулями:
* Модуль [masstransit_static](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/masstransit_static):
  * Ресурс `masstransit_rasp_data`
  * Ресурс `masstransit_data`
* Модуль [pedestrian_graph](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/pedestrian_graph):
  * Ресурс `pedestrian_graph_build_barriers_rtree`
  * Ресурс `pedestrian_graph_build_compact`
  * Ресурс `pedestrian_graph_build_compact_rtree`
  * Ресурс `pedestrian_graph_build_compact_persistent_index`
  * Ресурс `pedestrian_graph_build_leptidea_data_7`
  * Ресурс `pedestrian_graph_build_leptidea_topology_7`
  * Ресурс `pedestrian_graph_properties`


## Этапы сборки

### Выходные ресурсы

* `masstransit_stops_bindings` (FileResource)
* `masstransit_on_foot_transfers` (FileResource)
Данные варятся для пешеходного графа на основе статических данных ОТ, отсюда возникает версионная привязка данных ОТ и пешеходного графа. На сервисы пеш.граф и статические данные ОТ должны выгружаться с одинаковой версией.

### Привязка остановок к пешеходному графу

Запускается утилита [build_stops_binding](https://a.yandex-team.ru/arc_vcs/maps/masstransit/tools/data_build/build-stops-binding) со следующими фходными данными:
* статические данные общественного транспорта из ресурса `masstransit_data`
* пешеходный граф в формате fb из ресурса `pedestrian_graph_build_compact`
* rtree пеш. графа из ресурса `pedestrian_graph_build_compact_rtree`
* rtree барьеров пеш. графа из ресурса `pedestrian_graph_build_barriers_rtree`
* дополнительно: `geobase5` и `tzdata` загружаются из Кипариса перед запуском таски

Выходной файл с привязками `stops_bindings.fb` пишется в ресурс `masstransit_stops_bindings`

### Пересадки между остановками одной компоненты

Зовётся метод сборки пересадок [build_pedestrian_transfers](https://a.yandex-team.ru/arc_vcs/maps/masstransit/tools/data_build/build_pedestrian_transfers/pylib/create_data.pyx?rev=r9250947#L24) со следующими входными данными:
* статические данные общественного транспорта из ресурса `masstransit_data`
* конфиг графа (сгенерён самой таской из [шаблона](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/masstransit/lib/data/transfers_config_template.yaml))
* файлы пешеходного графа (тянутся конфигом)
  * пешеходный граф в формате fb из ресурса `pedestrian_graph_build_compact`
  * rtree пеш. графа из `pedestrian_graph_build_compact_rtree`
  * лептидийные данные из `pedestrian_graph_build_leptidea_data_7`
  * лептидийная топология из `pedestrian_graph_build_leptidea_topology_7`
  * rtree барьеров из `pedestrian_graph_build_barriers_rtree`
  * привязки остановок к пешеходному графу из `masstransit_stops_bindings`

Выхоной файл `on_foot_transfers` пишется в ресурс `masstransit_on_foot_transfers`.
По завершению сборки данных создаётся барьерный ресурс `masstransit_build_barrier`.


## Upload данных во все места

### Загрузка файлов пешеходного графа на YT (в Кипарис)

Загрузка файлов графа на YT начинается вместе с запуском модуля и выполняется во временную директорию, таким образом почти все файлы графа оказываются загружены ещё до завершения варки `on_foot_transfers`.  Как только все файлы, включая `stops_bindings.fb` и `on_foot_transfers` загружены во временную директорию, они копируются из временной в целевую директорию.

### Загрузка статических данных ОТ

* Загрузка текстовых файлов из ресурса `masstransit_rasp_data` в Кипарис в виде файлов
* Загрузка текстовых файлов из ресурса `masstransit_rasp_data` в Кипарис в виде таблиц, таска [UploadDataRaspToYtAsTables](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/masstransit/lib/rasp_yt_tables.py?rev=r9197002#L14)
* Экспорт остановок в виде таблиц на YT для справочника, таска [MakeDumpForSprav](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/masstransit/lib/rasp_yt_tables.py?rev=r9197002#L31)
* Загрузка данных в формате flatbuffer из ресурса `masstransit_data` в ecstatic в датасет `yandex-maps-masstransit-data` -- после создания барьерного ресурса `masstransit_build_barrier`. Датасет активируется в testing-ветке ecstatic и ставится в hold в stable-ветке
* Загрузка данных в формате flatbuffer из ресурса `masstransit_data` в Кипарис

### Загрузка пешеходного графа

* Загрузка файлов пеш. графа в т.ч. включая собранные в этом модуле ресурсы `masstransit_on_foot_transfers` и `masstransit_stops_bindings` в ecstatic в датасет `yandex-maps-pedestrian-graph-fb`. Датасет активируется в testing-ветке ecstatic и ставится в hold в stable-ветке.

### Загрузка данных в Sandbox

* Загрузка текстовых файлов из ресурса `masstransit_rasp_data` в Sandbox, тип ресурса `MASSTRANSIT_DATA_RASP`
* Загрузка данных в формате flatbuffer из ресурса `masstransit_data` в Sandbox, тип ресурса `MASSTRANSIT_DATA`
* Загрузка файлов пеш.графа в т.ч. включая собранные в этом модуле ресурсы `masstransit_on_foot_transfers` и `masstransit_stops_bindings` в Sandbox, тип ресурса `MAPS_MASSTRANSIT_PEDESTRIAN_GRAPH_FB`


## Валидация данных

В самом модуле валидации данных не происходит.
Статические данные ОТ валидируются модулем `masstransit_tester`, см. документацию этого модуля.
Пешеходный граф валидируется модулями `pedestrian_graph` и `pedestrian_tester`, см. документацию этих модулей.


## Свежесть данных

Данные собираются не реже, чем раз в сутки.

При невыкатке статических данных ОТ в течение некоторого времени на использующих их сервисах начинают устаревать данные о расписаниях ОТ, нитках, маршрутах, остановках и т.д., которые были изменены с момента взятия последних актуальных данных. При этом может также возникать расхождение, например, со справочником, в случае чего на картах могут отображаться остановки ОТ, но без каарточек расаписания и т.д.

При невыкатке пешеходного графа может пострадать актуальность маршрутов в роутере ОТ, может возникнуть расхождение между подложкой и графом. Например, не будет строиться маршрут там, где недавно нарисовали пешеходную дорожку и т.д.


## Решение проблем сборки модуля

### Ошибки работы самого модуля
* `maps.pylibs.utils.lib.process.ExecutionFailed`
Возникает при падении в вызываемом модулем плюсовом бинарнике.
Смотреть логи выполнения тасок (название таски есть в тикете в очереди MAPSGARDENBUILD). Как правило, случаются при некорректных входных данных. Падения также могут случаться при обновлениях сторонних билиотек (например, обновился формат данных leptidea, модуль pedestrian_graph уже был обновлён и собрал данные в обновлённом формате, а данный модуль не был, и не смог прочитать данные).
* TODO

### Временные проблемы, не связанные с модулем
* `maps.garden.sdk.ecstatic.tasks.EcstaticError`
Обычно возникает во время учений и регламентных работ и сопровождается ошибкой типа
```
Dataset yandex-maps-masstransit-data=22.03.22-1 is not active on all groups after 7200 seconds of waiting.
URL: http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-masstransit-data/versions
```
Попробовать перезапустить модуль позже.

