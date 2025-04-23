# `orders_entrances_matcher`

Сопоставляет адреса заказов из [логов Яндекс.Еды](https://yt.yandex-team.ru/hahn/navigation?path=//home/eda-dwh/export/geo),
[логов Яндекс.Маркета](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/tpl/cdc/market_tpl_production_order_delivery) и
данных [Росреестра](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/__private_export/maps/smartdeal_rosreestr_data)
с `ft_id` подъездов и `addr_id` адресов через [Геокодер](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo).

| Что? | Где? |
| --- | --- |
| YT | Stable: [//home/maps/poi/flats/stable](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/flats/stable)<br>Testing: [//home/maps/poi/flats/testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/flats/testing) |

## Выходная таблица

Выходная таблица имеет схему

| Имя | Тип | Описание |
| --- | --- | --- |
| `isocode` | `string` | [isocode страны](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) |
| `ft_id` | `int64` | Идентификатор подъезда ([`ft` объекта](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/ft.html) с `ft_type_id == 1904 [URBAN_ENTRANCE]`) в YMapsDF. Может отсутствовать, если не был найден. |
| `addr_id` | `int64` | Идентификатор адреса ([`addr` объекта](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/addres.html) в YMapsDF. Может отсутствовать, если не был найден. |
| `geocoder_address` | `string` | Отформатированный адрес объекта, возращенный Геокодером |
| `address_constructed` | `string` | Сконструированный адрес объекта, использовавшийся для запроса в Геокодер. Отличается от `geocoder_address` тем, что Гекодер возвращает более полный адрес. Иногда Геокодер может вернуть неправильный адрес, в таком случае различие тоже будет |
| `address_full` | `string` | Полный адрес, предоставленный нам в логах Еды. Может отличаться от `address_constructed` |
| `address_floor` | `string` | Номер этажа |
| `address_office` | `string` | Номер квартиры |
| `weight` | `double` | Условное значение, обозначающее надёжность данной записи (больше - лучше). Для доставок - просто количество заказов. |

## Форматирование адресов

В выгрузке есть колонка `address_full`, в которой содержится полный адрес заказа (`{город}, {улица}, {дом (с корпусом)}, {подъезд}`), но она отсутствует практически всегда. Поэтому мы собираем адреса из остальных полей (`address_city`, `address_street`, `address_house`, `address_entrance`). Тут есть несколько корнер-кейсов:

- Адрес может содержать шумовые слова (например `{'address_entrance': 'подъезд номер 4'}`, где `подъезд` и `номер` — шумовые, но при этом в `{'address_street': 'улица Пушкина'}` слово улица шумовым не является).
- Адрес может быть написан на иностранном языке вне зависимости от страны/города заказа (например `{'address_city': 'Moscow', 'address_street': 'ulitsa Pushkina', 'address_house': 'dom Kolotushkina'}`).

Поэтому сборка адреса выглядит примерно так

```py
address_constructed = f'{address_city}, {address_street}, {address_house}, {entrance_token} {address_entrance}'
```

где `{entrance_token}` это слово `подъезд` на языке адреса.

Особенным случаем является иврит. Приведенное выше описание для него верно, 
слово `подъезд` добавляется на английском языке (в Геокодере форматированные 
адреса выглядят аналогично). Нюанс в том, что иврит содержит символы, при отображении 
которых меняется порядок слов. Поэтому часто мы при просмотре YT-таблиц/тестов 
можем заметить, что компоненты адреса выстроились в обратном порядке: 
`{address_house}, {address_street}, {address_city}`, но на самом деле это не так - 
порядок символов сохраняется.

## Кэш

Так как мы не хотим устраивать ежедневные обстрелы Геокодера на несколько миллионов запросов, "поматченные" адреса кэшируются в табличку на YT. Так как геокодинг не всегда может быть успешным (например Геокодер может вернуть неправильный адрес), каждая запись перезапрашивается раз в 31 день.
День, после которого запись должна быть перезапрошена, указывается в `expiration_day`.

Идентификаторы подъездов [`ft_id`](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/ft.html) могут протухать, если объект был удален и создан заново. В таком случае этот `ft_id` исчезает из YMapDF и его никто не может больше занять.

Также не гарантируется, что Геокодер не будет таймаутить или пятисотить, так как 
по умолчанию создаваемая нагрузка может достигать 1к RPS. Ответы на такие запросы 
не стоит класть в кэш, так как при следующем запуске нужно сделать перезапросы.

**Важно**: запросы к геокодеру происходят с хоста, на котором исполняется бинарь, 
а не с помощью YT-операций. Запросы производятся батчами асинхронно, но все равно 
следует помнить про потребление RAM во время исполнения.

Кэш имеет схему

| Имя | Тип | Описание |
| --- | --- | --- |
| `address_full` | `string` | Полный адрес предоставленный нам в логах Еды |
| `address_city` | `string` | Город |
| `address_street` | `string` | Улица |
| `address_house` | `string` | Дом |
| `address_entrance` | `string` | Подъезд |
| `ft_id` | `int64` | Идентификатор подъезда ([`ft` объекта](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/ft.html) с `ft_type_id == 1904 [URBAN_ENTRANCE]`) в YMapsDF. Может отсутствовать, если не был найден. |
| `addr_id` | `int64` | Идентификатор адреса ([`addr` объекта](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/addres.html) в YMapsDF. Может отсутствовать, если не был найден. |
| `geocoder_address` | `string` | Отформатированный адрес объекта, возращенный Геокодером |
| `isocode` | `string` | [isocode страны](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) |
| `expiration_day` | `uint64` | Номер дня с 01.01.1970, когда текущая запись истекает |

## Алгоритм выбора expiration_day

Для каждой записи в таблице считается хэш - число от 0 до `PARTS_COUNT`. 
Далее из чисел, таких что `START_TIME + PARTS_COUNT*K + h` где h - хэш посчитанный на предыдущем шаге, а К - натуральное число, выбирается наименьшее, большее номера текущего дня.

Значение констант по умолчанию:

`PARTS_COUNT = 31` - количество дней, за которое кэш полностью обновится
`START_TIME = datetime(1970, 1, 1)` - дата, с которой считаются номера дней в `expiration_day`


Преимущества данного алгоритма:

- Кэш обновляется равномерно, то есть каждый день запрашивается примерно 1/31 записей 
- Есть гарантия, что каждая запись в кэше хранится не более 31 дня, так как в N-ный день перезапрашиваются все записи, у которых `expiration_day`<= текушего дня.
- Смена парамера `PARTS_COUNT` не повлияет на корректность выполнения процесса. Равномерность восстановится через N дней, где N - значение параметра `PARTS_COUNT` до смены.

Недостатки данного алгоритма:

- При первом запуске алгоритма нужно для каждой записи посчитать `expiration_day`
- Если процесс не запускался N дней, то при следующем запуске будут запрошены все записи, истекщие за это время, что может создать большую нагрузку на геокодер.

## `--help`

```
usage: orders_entrances_matcher [-h] [--input-tables INPUT_TABLES [INPUT_TABLES ...]] [--addresses-cache ADDRESSES_CACHE] [--output-table OUTPUT_TABLE]

optional arguments:
  -h, --help            show this help message and exit
  --input-tables INPUT_TABLES [INPUT_TABLES ...]
  --addresses-cache ADDRESSES_CACHE
  --output-table OUTPUT_TABLE
```
