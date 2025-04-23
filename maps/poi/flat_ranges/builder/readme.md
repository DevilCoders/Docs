# `builder`

По обработанным логам Яндекс.Еды строит промежутки квартир (flat range-ы), разбитые по подъездам и этажам.

| Что? | Где? |
| --- | --- |
| Sandbox Resource | [`FLAT_RANGE_BUILDER_BINARY`](https://sandbox.yandex-team.ru/resources?type=FLAT_RANGE_BUILDER_BINARY&state=READY&limit=20) |
| YT | Stable: [//home/maps/poi/flats/stable/export_data](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/flats/stable/export_data)<br>Testing: [//home/maps/poi/flats/testing/export_data](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/flats/testing/export_data) |

## Выходные таблицы

Результатом запуска являются две таблицы: с промежутками квартир для подъездов и промежутками для этажей в подъездах.

### Подъезды

Практически все колонки (кроме одной `region`) соответствуют [спецификации](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/ymapsdf/garden/create/entrance_flat_range.sql) финальной таблички в YMapsDF. Колонка регион добавлена туда, чтобы в последствии [экспортер ресурса в YMapsDF](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/ymapsdf/lib/merge_flats) смог правильно разбить эту табличку по регионам.

Выходная таблица имеет схему (лежит [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/flat_ranges/builder/lib/schema.py))

| Имя | Тип | Описание |
| --- | --- | --- |
| `flat_range_id` | `int64` | идентификатор промежутка квартир |
| `region` | `string` | регион объекта (`cis1`, `cis2` и так далее) |
| `flat_first` | `string` | первая квартира в промежутке |
| `flat_last` | `string` | последняя квартира в промежутке |
| `ft_id` | `int64` | идентификатор подъезда ([`ft` объекта](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/ft.html) с `ft_type_id == 1904 [URBAN_ENTRANCE]`) в YMapsDF |
| `is_exact` | `bool` | является ли промежуток квартир проверенным человеком (`True`) или "предсказан" — интерполированный/экстраполированный (`False`) |

### Этажи

Аналогично подъездам. Спецификацию можно найти [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/ymapsdf/garden/create/entrance_level_flat_range.sql), также добавлена колонка `region` по причинам, описанным выше.

Схема выходной таблицы:

| Имя | Тип | Описание |
| --- | --- | --- |
| `level_flat_range_id` | `int64` | идентификатор промежутка квартир |
| `region` | `string` | регион объекта (`cis1`, `cis2` и так далее) |
| `level_universal_id` | `string` | номер этажа в подъезде. |
| `flat_first` | `string` | первая квартира в промежутке |
| `flat_last` | `string` | последняя квартира в промежутке |
| `ft_id` | `int64` | идентификатор подъезда ([`ft` объекта](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/ft.html) с `ft_type_id == 1904 [URBAN_ENTRANCE]`) в YMapsDF |
| `is_exact` | `bool` | является ли промежуток квартир проверенным человеком (`True`) или "предсказан" — интерполированный/экстраполированный (`False`) |

## Промежутки квартир (`flat_range`)

Бывает два типа нумерации квартир:
- Численные (квартиры `183`, `16`, `1337`).
- Численные с литерой (квартиры `123А`, `32/1`, `B228`).

Квартиры будем объединять в отрезки (или `flat-range`-ы) со следующими свойствами:
- Отрезки не могут быть пустыми. Они обязательно содержат хотя бы одну квартиру. Одна квартира записывается в виде отрезка с совпадающими концами.
- Отрезок содержит либо численный диапазон квартир, либо один номер квартиры с литерой.
- Для численных диапазонов левый конец отрезка всегда `<=` правому.
- Левый и правый конец отрезка входят в последовательность (например отрезок `[213, 214]`  состоит из `213` и `214` квартиры).
- Если отрезок численный, то его концы обязательно натуральные числа (строго большее нуля).

## Алгоритм

Для построения отрезков квартир из множества всех адресов заказов используются
две основные эвристики:
1. Номера квартир в одном подъезде или на этаже идут по порядку
2. Квартиры в одном и том же доме не повторяются

Известны контрпримеры для эвристик (в питерских домах часто квартиры идут
не по порядку; бывают дома в которых к квартире можно пройти из нескольких
подъездов), поэтому итоговый алгоритм должен уметь не ломаться на таких
выбросах.

На первом шаге нам требуется определить все известные заказы в одном доме.
Сложность заключается в том, что подъезд может принадлежать к нескольким
адресам, а разные адреса иметь пересекающиеся, но не совпадающие множества
подъездов. Например, такая ситуация вполне возможна:
| `addr_id` адресов | `ft_id` подъездов |
| --- | --- |
| 1 | 101, 102, 103 |
| 2 | 102, 103, 104 |

Это плохо тем, что для одного адреса у нас может сформироваться один набор
промежутков, а для другого - другой. Это может вызывать пересечение отрезков
квартир в одних и тех же подъездах - и соответственно проблемы с выкидыванием
лишних квартир.

Для разрешения этой проблемы для каждого адреса (`addr_id` в терминах `ymapsdf`)
мы находим головной адрес подъезда (альтернативно `head_addr_id`). Головной
адрес - это общий идентификатор для всех подъездов, которые находятся по одному
адресу. Так как у каждого подъезда головной адрес может быть только один, то
если у каких-то двух адресов есть общий подъезд, то всех их подъезды должны
иметь один и тот же головной адрес.

Головной адрес находится по таблице `ft_addr`. Эта таблица задает граф с ребрами
`ft_id -> addr_id` и `addr_id -> ft_id`. Для каждого `addr_id` в порядке
возрастания мы обходим этот граф в ширину, выставляя для каждого `addr_id` по
пути `head_addr_id` в изначальный `addr_id` (с которого начали обход). Обход
останавливается, если у `addr_id` уже есть `head_addr_id`.
После того, как у всех `addr_id` выяснен `head_addr_id` в изначальной таблице
`ft_addr` мы заменяем все `addr_id` на `head_addr_id` и получаем искомую таблицу
`ft_head_addr` - в которой для каждого подъезда есть головной адрес.

После этого мы приступаем к основной части алгоритма. Для каждого головного
адреса мы берем все заказы в подъездах, у которых этот головной адрес и
суммируем количество заказов в одинаковых квартирах. После этого для квартир, у
которых больше одного подъезда, мы выбираем подъезд и этаж, куда было больше всего
заказов. Далее квартиры разделяются на две части: квартиры, чей номер
является числом (будем называть их численные квартиры), и квартиры, чей номер
содержит в себе какие-либо литеры (будем называть их квартирами с литерами).

Для всех квартир с литерами мы просто генерируем отрезки длиной 1, где начало и
конец являются номером квартиры.

Все численные квартиры мы обходим в порядке возрастания и генерируем отрезки
по следующему алгоритму:
1. Запоминаем номер квартиры, и говорим что это начало отрезка.
2. Идем по списку квартир пока подъезд (или этаж в случае нарезки по этажам) 
не поменяется, либо пока расстояние между двумя соседними квартирами не превысит 
`min-flat-range-gap-to-split`, либо пока квартиры по этому `head_addr_id` 
не закончатся. Когда такое случается - запоминаем последний валидный номер 
квартиры и генерируем отрезок (см. пункт 3)
3. Отрезок генерируем с началом в квартире из пункта 1 и концом в квартире из
пункта 2. Если отрезок получается меньше `min-flat-range-length`, то отрезок
пропускаем (если `min-flat-range-length` равен 1, то отрезки пропускаться не
будут - потому что минимальная длина отрезка 1). Квартиры из пропущенных
отрезков в итоговую выгрузку не попадают.
После этого идем обратно в пункт 1.

В результате мы получаем множество отрезков квартир (и с литерами, и численных).
Данный алгоритм применяется независимо для подъездов и этажей. Далее мы для 
полученных таблиц формируем уникальные порядковые идентификаторы и получаем 
финальные таблицы:
- `entrance_flat_range` для подъездов.
- `entrance_level_flat_range` для этажей.

## `--help`

```
$ ./flat_ranges_builder --help 
usage: Prepares an export for Garden [-h] --matched-orders-table MATCHED_ORDERS_TABLE --output-dir OUTPUT_DIR [--min-flat-range-gap-to-split MIN_FLAT_RANGE_GAP_TO_SPLIT] [--min-flat-range-length MIN_FLAT_RANGE_LENGTH] [--preferred-countries PREFERRED_COUNTRIES [PREFERRED_COUNTRIES ...]]
                                     [--pool-size-limit POOL_SIZE_LIMIT]

optional arguments:
  -h, --help            show this help message and exit

Input table:
  --matched-orders-table MATCHED_ORDERS_TABLE
                        Path to the matched orders table produced by orders_entrances_matcher

Output dir:
  --output-dir OUTPUT_DIR
                        Output dir

Pipeline arguments:
  --min-flat-range-gap-to-split MIN_FLAT_RANGE_GAP_TO_SPLIT, --gap-to-split MIN_FLAT_RANGE_GAP_TO_SPLIT
                        Defines min gap distance between two flats in range to split. Must be greater than 0. If 1, then every flat will be placed in their own FlatRange (even neigbouring). If entrance "contains" numerical and alphanumerical flats, any gap will be splitted
  --min-flat-range-length MIN_FLAT_RANGE_LENGTH, --min-length MIN_FLAT_RANGE_LENGTH
                        Defines minimal flat range length. Flat ranges with length less than that number will be dropped (except alphanumerical ranges). Have to be greater than 0.
  --preferred-countries PREFERRED_COUNTRIES [PREFERRED_COUNTRIES ...], --countries PREFERRED_COUNTRIES [PREFERRED_COUNTRIES ...]
                        Accepts list of country isocodes. Flat ranges outside of this countries will be dropped.
  --pool-size-limit POOL_SIZE_LIMIT
                        Limit of YT operations launched at the same time if set.
```