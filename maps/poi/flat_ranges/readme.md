# Пайплайн `flat_ranges`

Flat range — (от английского flat — квартира, range — отрезок, промежуток) это последовательности квартир, представленные как промежутки, разбитые по подъездам и этажам домов.

Хотим, чтобы в Геокодере по запросу квартиры в доме уточнялся подъезд и этаж. Для этого нам регулярно отгружают [логи Яндекс.Еды](https://yt.yandex-team.ru/hahn/navigation?path=//home/eda-dwh/export/geo),
[логи Яндекс.Маркета](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/tpl/cdc/market_tpl_production_order_delivery) и
данные [Росреестра](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/__private_export/maps/smartdeal_rosreestr_data), которые мы обрабатываем этим пайплайном. Результирующая табличка в дальнейшем экспортируется [в YMapsDF](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/entrance_flat_range), откуда их забирает [индексер Геокодера](https://garden.maps.yandex-team.ru/stable/geocoder_indexer).

## Важные ссылки

| Что? | Где? |
| --- | --- |
| ABC | [maps-core-flats-information](https://abc.yandex-team.ru/services/maps-core-flats-information/) |
| Робот | [robot-flats-export](https://staff.yandex-team.ru/robot-flats-export) ([Пароль](https://yav.yandex-team.ru/secret/sec-01f0xtmvdch80xredzrgs3cfjr/explore/versions)) |
| Графики | [Графики](https://datalens.yandex-team.ru/u5dphv7qku7ko-flat-ranges) |
| YT | Stable: [//home/maps/poi/flats/stable](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/flats/stable)<br>Testing: [//home/maps/poi/flats/testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/flats/testing) |
| Sandbox | [Testing BUILD_FLATS_EXPORT](https://sandbox.yandex-team.ru/scheduler/696853)<br>[Stable BUILD_FLATS_EXPORT](https://sandbox.yandex-team.ru/scheduler/696885)<br>Аркадия: [maps/poi/flat_ranges/task](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/flat_ranges/task) |
| Исходные данные | Логи Яндекс.Еды: [//home/eda-dwh/export/geo](https://yt.yandex-team.ru/hahn/navigation?path=//home/eda-dwh/export/geo) ([Документация](https://doc.yandex-team.ru/taxi/dmp/services/Eda/yt/export/geo/))<br>[логи Яндекс.Маркета](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/tpl/cdc/market_tpl_production_order_delivery)<br>[Данные Росреестра](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/__private_export/maps/smartdeal_rosreestr_data)<br>ABC-группа: [taxiyamapsordersusers](https://abc.yandex-team.ru/services/taxiyamapsordersusers/) |
| Garden | Свежий экспорт на YT:<br>&emsp;[//home/maps/core/garden/stable/ymapsdf/latest/cis1/entrance_flat_range](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/entrance_flat_range)<br>Модуль экспорта бандла в Аркадии:<br>&emsp;[maps/garden/modules/flats_bundle](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/flats_bundle)<br>Добавление бандла в YMapsDF в Аркадии:<br>&emsp;[maps/garden/modules/ymapsdf/lib/merge_flats](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/ymapsdf/lib/merge_flats) |


## Структура проекта

| Папка | Описание |
| --- | --- |
| [orders_entrances_matcher](orders_entrances_matcher/) | Отвечает за парсинг данных и матчинг — сопоставление человекочитаемых адресов с `ft_id` подъездов. |
| [builder](builder/) | Отвечает за фильтрацию и объединение квартир в ренжи, которые в последствии экспортируются в YMapsDF. |

## Стадии пайплайна

1. Логи Яндекс.Еды ([таблицы на YT]((https://yt.yandex-team.ru/hahn/navigation?path=//home/eda-dwh/export/geo))) — непосредственно то, что мы используем для построения экспорта.
1. `orders_entrance_matcher` ([Arcadia](orders_entrance_matcher/)) — превращает адреса из логов в ft_id .
1. `builder` ([Arcadia](builder/)) — превращает выходную таблицу `Matcher`-а в промежутки квартир (`flat-range`-ы).
1. `flats_bundle` в YMapsDF ([Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/flats_bundle)) — "находит" таблицы из builder и объявляет её ресурсом Огорода.
1. `merge_flats` в YMapsDF ([Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/ymapsdf/lib/merge_flats)) — перекладывает ресурс в YMapsDF.

## Как запустить?

Если требуется разовый запуск всего пайплайна, то можно сделать manual run [в тестовом Sandbox шедулере](https://sandbox.yandex-team.ru/scheduler/44584) (или скопировав один из последних запусков, если нужно поменять пути или другие параметры запуска). Запускаться в стейбле можно [в этом шедулере](https://sandbox.yandex-team.ru/scheduler/44626).

Если нужно сделать локальный запуск, то Sandbox таска делает следующее. 

Запускает [`orders_entrances_matcher`](orders_entrances_matcher/), чтобы получить из логов заказов Еды → `ft_id` подъездов.

```bash
$ ./orders_entrances_matcher --input-tables {input_tables_paths} --addresses-cache {cache_path} --output-table {matched_orders_path}
```

где:
1. `input_tables_paths` — пути к [логам Яндекс.Еды](https://yt.yandex-team.ru/hahn/navigation?path=//home/eda-dwh/export/geo) *(Внимание! Для чтения логов нужны доступы, имеют их участники этой [ABC-группы](https://abc.yandex-team.ru/services/taxiyamapsordersusers/))*
1. `cache_path` — куда положить кэш матчера на YT. Может быть любым.
1. `matched_orders_path` — куда положить результат на YT. Может быть любым.

Дальше запускает [builder](builder/), чтобы получить из обработанных логов с `ft_id`-шниками → таблицы с промежутками квартир.

```bash
$ ./flat_ranges_builder --matched-orders-table {matched_orders_path} --output-dir {output_dir}
```

где:
1. `matched_orders_path` — путь, куда положили результат запуска [`orders_entrances_matcher`](orders_entrances_matcher/).
1. `output_dir` — директория на YT, в которой лежат таблицы с промежутками. Может быть любым.
