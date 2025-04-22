# Пайплайн экспорта POI из `extra_poi_bundle` в НК

## Цель процесса

Обеспечить пополнение базы [Народной карты](https://n.maps.yandex.ru/),
организациями из [справочника](https://altay.yandex-team.ru/), для последующего
уточнения взаимных позиций POI в контексте улучшения горизонтального качества
POI (полнота, бесконфликтность, точность).

Процесс заливки является автоматизированным. Это означает, что ряд краевых
случаев обрабатывается с помощью операторов через механизмы Народной карты -
модерация правок, гипотез об ошибках. К таким случаям, например, относятся
потенциальные смысловые дубли, координатные дубли.

## Технические детали

1. В таблице [`static_poi`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/static_poi/stable/latest) для каждой организации содержится информация о том,
в какие дома она попадает. Здесь и далее под домом подразумевается сущность из
ymapsdf [`bld_geom`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/bld_geom&), т.е. имеющая свой `bld_id`. Данная информация считается
в рамках [пайплайна `static_poi`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/static_poi/README.md?rev=7331445).
Как именно выбирается, к каким `bld_id` относится организация:
  * Изначально каждая организация попадает в те дома, от которых она отстоит
    не больше, чем на 1 метр. При этом используются координаты организации из
    справочника
  * Для каждой организации вычисляется набор адресов ([`addr_id`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/bld_addr)) домов,
    в которые она попала.
  * Организация приписывается также ко всем другим домам, находящимся по данным
    адресам.
2. На подложку в конечных продуктах попадают не все организации из `static_poi`,
а лишь их специальным образом отфильтрованное подмножество - `extra_poi_bundle`.
Для заливки используется не сам `extra_poi_bundle`, а таблицы [`extra_poi_nyak_export`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/extra_poi_nyak_export/stable/full_export_data/latest),
которые так же создаются пайплайном `static_poi` и отличаются от `extra_poi_bundle`
лишь набором колонок. Данный пайплайн пополняет НК только защищенными
геопродуктовыми организациями из этого подмножества и их соседями (см. пример ниже).
  * Геопродуктовые организации подразделяются на два подкласса: защищенные и нет.
    Признак защищенности поставляется [Рекламными геопродуктами](https://staff.yandex-team.ru/departments/yandex_content_7382_2577) через
    таблицу [priority_company_permanent_id](https://yt.yandex-team.ru/hahn/navigation?path=//home/geoadv/export/production/priority_company_permanent_id). Примером незащищенного геопродукта
    на момент написания была кампания сети Western Union, координаты POI которой
    обладали низким качеством.
  * Под соседями конкретного POI понимаются все POI из `extra_poi_bundle`,
    которые попадают в один и тот же дом.
  * Каждая отобранная организация загружается в НК лишь один раз вне зависимости
    от того, во скольких `bld_id` она находится.
3. Детали организации процесса:
  * В `extra_poi_nyak_export` содержатся все организации, потенциально подходящие
    для экспорта. Вышеописанная фильтрация геопродукта применяется к этим данным
    уже непосредственно перед загрузкой в НК.
  * Сама заливка состоит из запуска двух бинарей, лежащих в данной папке:
    `calc_neighbors_similarities` и `push_organizations`, и запускается через
    [сэндбокс-таску](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/ExtraPoiBundleNkExport/__init__.py?rev=7353702#L26).
  * [Текущий шедулер](https://sandbox.yandex-team.ru/scheduler/24242/view)
  * В целях отладки можно указать параметр `store_neighbor_similarities_table_dir` -
    директорию на yt, куда будет скопирована таблица кандидатов заливки после
    всех фильтраций и преобразований.
  * Для процесса загрузки считаются [статистики](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/extra_poi_nyak_export/stable/statistics) по количеству модераций,
    загрузок и т.п. [Метрики](https://datalens.yandex-team.ru/kalqabqb04ikg-poi-metrics)
4. Организации загружаются в НК по одной через интерфейс [редактора](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/libs/editor_client).
5. При заливке организации в НК учитываются следующие аспекты (подробнее см. ниже):
есть ли такой же пермалинк в НК уже (это узнаем непосредственно в момент заливки);
есть ли другие организации в том же доме, которые сильно похожи на заливаемую
(эта информация предпосчитывается перед заливкой); есть ли indoor слой в месте,
где мы хотим добавить организацию.
6. Если организация не содержится в НК, не имеет похожих и не пересекается с
indoor-ом, она заливается в НК.
7. Непосредственно в момент заливки проверяются конфликты видимости. В зависимости
от их наличия делается либо модерируемое изменение, либо обычное.
  * Под конфликтом понимается близкое расположение разных организаций, в
    результате которого одна из них оказывается не видна на подложке.
  * Для каждого зума конфликт возникает, если два пои расположены ближе, чем
    [определенный порог](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/data/zoom_conflict_meters.json?rev=7106711#L1).
  * Конфликты на 19-21 зумах считаются критическими.
  * Конфликты вычисляются у заливаемых организаций между собой, а также у
    заливаемых организаций с объектами НК (POI, адресные точки, транспортные метки).
8. Если организация пересекается с indoor-слоем, создается гипотеза на добавление indoor POI.
9. Если организация была залита недавно (на данный момент - в течение последних 10
заливок), она будет пропущена. Это позволяет удалять закрытые организации из НК
и не заливать их снова. За время кулдауна (10 дней) изменения должны успеть прорасти
в Справочник.
10. В НК существует валидация - процесс проверки данных на наличие конфликтов.
Валидация делается только для защищенных геопродуктовых POI, т.к. только для них
на момент написания дается гарантия видимости на подложке. Незащищенный геопродукт
участвует в валидации на правах обычных POI, для него никаких гарантий видимости
не дается.
11. При заливке в НК display class организации выставляется исходя из ее рубрики.
При этом для все залитых организаций гарантируется выбор display class-а из `extra_poi_bundle`
в рамках стадии `ymapsdf:merge_poi`.
12. Также реализована функциональность по упорядочиванию организаций специальным образом,
для более эффективной организации процесса заливки.
  * Как было отмечено выше, организации заливаются "подомно". При этом каждый дом (`bld_id`)
    получает некий скор ранжирования. Текущий скор устроен так, что считает дома тем более
    приоритетными, чем больше их заливка улучшит метрику конфликтов, и тем менее приоритетными,
    чем больше модерируемых правок нужно сделать в доме.
  * Организации внутри одного дома ранжируются хитрым образом, что позволяет снизить количество
    модерируемых правок. Пример того, почему так происходит, описан в [коде](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/static_poi2nmaps/push_organizations/lib/util.cpp?rev=7524910#L395). Алгоритм
    ранжирования является жадным алгоритмом поиска вершинного покрытия графа.
13. Подробное описание и схему процесса заливки следует смотреть [по ссылке](https://drawio.yandex-team.ru?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Extra%20POI%20NK%20export%20pipeline#R7Vxbc5s4FP41eYyHu%2FFjLnbaadJ2ms5uuy8dGWTQBhArZCfur18JkLkIBxzbGLd1ZhxxkITQ%2Bc6no8PBF%2FpN%2BHJHQOw%2FYBcGF5rivlzotxeaNjEs9s0F60xgaXYm8AhyM5FaCB7RT5gLlVy6RC5MKhUpxgFFcVXo4CiCDq3IACH4uVptgYPqVWPgQUnw6IBAlv6NXOpnUttUCvk7iDxfXFlV8jMhEJVzQeIDFz%2BXRPr0Qr8hGNOsFL7cwIDPnZiXrN1sy9nNwAiMaJcGaHUH7h7ezd55t%2BsP6j%2BX99PxX5d5LysQLPMb%2FjK9uv%2F6%2FmHKpJ%2BvvnzNx07XYkKSZxQGIGJH1wsc0cf8jMKOfUzQTyYDAROoTJBQQGiuU43XWKAguMEBJmlfugugvXAqLR8pcJ7y%2FhwcBCBO0HxzhRAQD0XXmFIc5iIxnlmp6win4yN4GbnQFYMR889beQFIkrzsgsTf1HJwiBzRNSX4CZbGazk2nC%2FSWmysKIIkrxmAOQw%2B4wRRhCMmc5hO%2BMnrFSQUMTTd1yqEyHX5XV2DAHmNLa7yE5uasr6F8lgL%2BFIS5fq%2FgziElKxZFXF2nGMxN0ZdYPO5gPZYWJ5fgrVh5EKQm5O36btAHCvkoNsBgJoEwI8fOF3MZeD5IOZFZx0gplY%2BV88%2BovAxBg6XPzP%2B4VCioYDfPNP%2F%2FXwjYNjyUlR8WlLWC8zlNViyararNwFA0w3DdA%2BjDN3QRqoyKT5WVTeWrBurSTXH0owuaeZCswLKMcuHQOAilVr%2FLTmDsXmnnJKv%2BEW1GRitAZv7l0sKQTgiSy4iDvumZBk9ZUfARYCPjJk4%2B%2FeMnhAr5oKYYFZKIFkhB%2FLT0EWUaYF3Lq7ISh7%2FP81PKY9ZdTHMORE1hIRft5DV8FWwhdIOrTpiFKhDqwkxCrQV2z4MYkxFaYWIqvWJEaMBI7VphZF7xddhbrmcdDm7ZguDLC5NMJslsv6WKyM9%2BM4PRqY4vH0pn7xdi6MXRL%2BJPli51IodFY34gWhTWQC26inBS%2BLAdipjt%2BZB2m5Y0K14HrLWS1o1G5QqZAQGgKJV1V9p0nR%2Bhc8YsTvbgMoytqwJoovsvvNWZf%2Bi3tGk2pE2rnWUTYzUUQq8zW2%2FHYumDD02w8I%2FwYT62MMRCKaF9Lpq80Wde4zjHA%2F%2FQkrXuQ8DlhRXYfp2tFgd0aKqHeHSGQd7WbwlWfwjZFzu81mAJGTuDKd3BUXsi6%2FkByTZxWKhOU4TybrW3DKtw5DsWJmMrHE7z%2Fa6Fo%2BPz7Pqbjxb4UxBusoOpHt8yxkWz47tKj2a6ht5dqzVOqoT9pF51j4vntW6wsUaFM9OJIv%2Fzv3g%2Fme%2BvrUlmWV039kGcFGuL%2B1rC0%2BvIJ3vFc5pZqCErRso8u7T7m%2F1vUAiFtn21Vg7NEqajdyusYVh92vkgpzK%2B3I8BPi1RlYo77g9rDLPY0i9gMYYFLWoctBvxtUkO2s%2BDufLpN1RO4TbZU5GplrFvNEUARnpurxGW8dyvIS9l%2BbqljCEaQomHojQT5DC7pdwc03DlOa7XzdX1c%2FLtxCG3e6KDowB5LjNjQ8dvnFLUIgCwKNpEdf4HBPZ6xg%2ButPYao1NzIZNnDke2ZM%2BAX5mQQrtdEtcs1%2BkTbjGFPFn14LmRn0h2OImsS0xWJeqxbxC8spl7VpEYFJ71rZbfVbIRnBYn02OzYjAt4tWIu59AwJnyXQAqyauLNIQOgRpKIcpIibYXTpUWuk2kfRSn2fIEFYtlq4pTfTAfBKrT3oYn4Ie3roB24NWOgc%2Fh7UpV08S%2BziBfswz1c%2FkpPrZMYS6h9%2FZ1X608aD0o8lRhU%2Bz2f37j3%2ByTX6DbJOuySbHW181OfLR5A4V2yBE%2Bf0kDiYNwdfenZzXbar75mjMdv5K8VGrPrRqN3lC9kgsfr14Qpocd9kh%2B2RN5fQTH%2FjMe51FYIW8zJXVZ7HI0eONfDZ0niASUL41mPEMpJkTLBNmKBvnd8Y4hsJLZ0lSrWwqMBRoFgjTyGP6LWepPMYErFJkeWxxSZpTUnIvPE2BWkDYEJKrkEwb5jhjZnyoajUaynAnUholxjpERtSB4Mr26CJndC1YQwaoao8mfbrq2klCVYdzBV9VTruDqHV1QIaVvaDJga8HEMco8rjBEbbM8ynon2fgS8zQwPkkY5bLlGc430TMJfExPxWtwdOPUIy2hW2YpVNBJKLznXLgfht60YzJyNBLy6HRyjW9ptiJvVj%2FK6EHiAt5TR4K4n3xxEx3wUrcX%2BL4agHhpoHiAgr%2BALAZgIaqDAxx2%2BOIR0ZcngocY5RyIiXgByv%2FSJlvQ5GMGvkWrQ18U96cbys%2Fva8TofIHiltcLVN6KHh6NMq5bzPEH1Yr5XzDSvS62Mf9Ijs2Ta9SxLYtmnjq0I9iBpIItqcn2%2FUR7tBCaWce6txTa%2BPz3H%2FocgD0RGl9b32%2FYsD5WHpXUz58Et9%2BoFBPC4C%2Bnip11o9uDks%2FcixyGLmQbam4VdPbkoe7MbxD5tN2V%2FWwVlX9tFG93h4gdtePfWj9vCn%2FxhA9il8RMHvIp9GbgoU03WEsTp4vq08Ungi1LWxl6nIuZ9%2B5s7ocubqDESTZwzZ3GQeMh9Kyv44x9WGCBvCQbfe3cmvvPW7egzxZGq1uDcmhUFtY7EBv3%2BpdtwRdXwvbM1PRqL1Xa%2Bg1dR8oNdG06uHD11MT6%2FUNpQ8qlYM4V66bhmqeL%2BoZhgpD1pm%2BPKobaj3veAB0YL%2FGw4BpO%2FJgmD7PPm8mVifmaFL%2BVEOZln48TbDD4pd8Mqspfg5Jn%2F4P)
14. В процессе заливки существуют гонки (физически одна организация / indoor-гипотеза
может быть создана несколько раз). Например: в доме появилась новая организация,
пользователь добавил ее в НК руками, а мы не успели узнать об этом и добавили дубликат.

## Тонкие моменты
  1. Организации, не попавшие ни в один из домов по критериям из п. 1-2, пайплайном игнорируются.
      * **Как, возможно, должно быть:** для организаций, справочные координаты
      которых не попадают ни в один `bld_id`, мы пробуем найти `addr_id` (и дома)
      через геокодер. Возможно стоит для таких организаций создавать гипотезы.
      Возможно стоит вытаскивать результат геокодирования из данных справочника.
      Возможно стоит просто увеличить константу в п.1 с 1м до 3м или 5м.
  2. После заливки организация могла быть перемещена в совсем другой дом / адрес.
  Справочник об этом может ничего не знать и продолжит считать, что она на старом
  месте. Тогда окружение данной организации может не попасть в НК, в результате
  чего на подложке возможно будет иметь место конфликт, который останется
  незамеченным данным пайплайном.
      * **Как это можно полечить:** после заливки организации в НК появляется маппинг
      из `permalink`-а в ее `ft_id`. При поиске соседей организации мы можем так
      же учитывать тот дом/адрес, по которому находится этот `ft_id` - таким
      образом будет возможность учесть координаты НК для данного POI при поиске
      окружения. Важно понимать, что эта информация берется из `ymapsdf` и то,
      будут в нем координаты НК или Справочника для конкретной организации,
      зависит от логики в `ymapsdf` (о чем ниже). st.yandex-team.ru/GEOQ-331
  3. Чтобы координаты наших организаций сохранялись на подложке
  (и не перезатирались Справочником по пути) в [`ymapsdf:merge_poi`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/ymapsdf/lib/merge_poi?rev=7349773)
  добавлена логика по защите таких POI. А именно: все пои, находящиеся по одному
  адресу с защищенным геопродуктом, не берут для себя координаты из Справочника.
  В силу особенностей реализации данный процесс имеет лаг: координаты справочника
  для новых POI начинают отвергаться не сразу, а на следующем запуске после их
  первого появления в `ymapsdf`.


#### Пример

Пусть имеются следующие организации:

| permalink | bld\_ids | is\_geoproduct | is\_protected\_geoproduct |
|:---------:|:--------:|:--------------:|:-------------------------:|
|     1     |    [ ]   |       1        |             1             |
|     2     |    [ ]   |       0        |             0             |
|     3     |    [1]   |       1        |             1             |
|     4     |    [2]   |       0        |             0             |
|     5     |  [3, 4]  |       1        |             1             |
|     6     |  [4, 5]  |       0        |             0             |
|     7     |    [3]   |       0        |             0             |
|     8     |    [ ]   |       1        |             0             |
|     9     |    [ ]   |       0        |             0             |
|    10     |    [6]   |       1        |             0             |
|    11     |    [7]   |       0        |             0             |
|    12     |  [8, 9]  |       1        |             0             |
|    13     |  [9, 10] |       0        |             0             |
|    14     |    [8]   |       0        |             0             |

Тогда кандидатами для экспорта являются организации с permalink-ами: 3, 5, 6, 7.
* Оганизации 1 и 2 не попадают в экспорт, т.к. не принадлежат ни к одному дому.
* Организация 4 не попадает в экспорт, т.к. не является геопродуктовой и не
  имеет ни одного геопродуктового соседа по дому.
* Организации 3, 5 попадают в итоговую выборку, т.к. каждая из них является
  защищенным геопродуктом.
* Организации 6, 7 попадают в итоговую выборку, т.к. каждая из них является
  соседом с защищенным геопродуктом (организацией 5).
* При этом каждая из организаций 3, 5, 6, 7 попала в экспорт только один раз.
* Организации с 8-й по 14-ю в выборку не попадают, т.к. не являются защищенным
  геопродуктом или его соседями.
