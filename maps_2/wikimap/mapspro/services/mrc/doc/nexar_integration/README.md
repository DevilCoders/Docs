# Введение

Компания [Nexar](https://www.getnexar.com/) производит и распространяет умные видеорегистраторы, они автоматически детектируют опасные ситуации и выгружают видео в облако. Их продукты широко распространены в Израиле и США. С помощью своих устройств Nexar собирает фотографии с дорог, скрывает с них приватную информацию и предоставляет платное API для поиска и скачивания фотографий. Предлагается научиться использовать их API как источник данных, потенциально он может заменить регулярные объезды в Израиле.


# Nexar API

Nexar предоставляет API для поиска и скачивания изображений. Из соображений конфиденциальности они стараются по возможности прореживать снимки проездов, поэтому вероятность того, что в некоторой локальной окрестности найдется несколько снимков, снятых в одном проезде, крайне мала.

Каждый запрос должен содержать авторизационный токен в заголовке `Authorization`.

Для поиска фотографий предлагается использовать ручку `POST /api/roadItem/findRawFrames/v2`. Параметры передаются в теле запроса в формате JSON со следующими ключами:
- `start_timestamp` (required) all images having capture time greater than specified time (Epoch milliseconds)
- `end_timestamp`  (required) all images having capture
time less than specified time (Epoch milliseconds)
- `h3_indices`  List of Uber [H3 indices](https://eng.uber.com/h3/)
identifiers, at resolutions 10 to 15
- `bounding_box`  Geo based polygon area: (lat,lon) for the Southwest
point to (lat,lon) for the Northeast point. The input
bounding box is polyfilled with Uber H3 hexagons at
resolution 10.
- `limit`  Maximum number of image metadata items to return per
hexagon in the response. If the limit is 0, default will be
used.
- `heading`  Nexar car heading direction
at image capture time, one of: NORTH, NORTH_WEST,
WEST, SOUTH_WEST,
SOUTH, SOUTH_EAST,
EAST, NORTH_EAST

**Пример запроса**:
```
curl 'https://live-api.nexar.mobi/api/roadItem/findRawFrames/v2' \
-H 'authority: live-api.nexar.mobi' \
-H 'authorization: Bearer <Token>' \
--data-raw
'{"limit":15,"filters":{"bounding_box":{"south_west_point":{"latitu
de": 32.06849839548089,"longtitude":
34.768159600303214},"north_east_point":{"latitude":
32.07292122543956,"longtitude":
34.77966458485795}},"start_timestamp":1619015943376,"end_timestamp"
:1621607943376}}' \
--compressed ;
```

**Пример ответа**:
```
{
    "raw_frames": [
        {
            "frame_id": "3eff49272dc534da88517dffe94023ea",
            "image_ref":
"timelapses/rideTimeLapse__0_20210520_085005.mp4/frame_3eff49272dc534da88517dffe94023e
a.jpg",
"image_url":
"https://images-cdn-api.getnexar.com/aod/full/timelapses/rideTimeLapse__0_20210520_085
005.mp4/frame_3eff49272dc534da88517dffe94023ea.jpg",
"course_of_camera": 242.4992218017578,
            "captured_on_ms": 1621489872000,
            "h3_indices": {
                "h3_index_res0": "577586652210266111",
                "h3_index_res1": "581769194442326015",
                "h3_index_res2": "586272244313882623",
                "h3_index_res3": "590775362904915967",
                "h3_index_res4": "595278953942351871",
                "h3_index_res5": "599782549274755071",
                "h3_index_res6": "604286147962601471",
                "h3_index_res7": "608789747472531455",
                "h3_index_res8": "613293347091513343",
                "h3_index_res9": "617796946717310975",
                "h3_index_res10": "622300546344452095",
                "h3_index_res11": "626804145971793919",
                "h3_index_res12": "631307745599160831",
                "h3_index_res13": "635811345226530943",
                "h3_index_res14": "640314944853901431",
                "h3_index_res15": "644818544481271925"
            },
            "gps_point": {
                "latitude": 32.070294,
                "longtitude": 34.771114,
                "altitude": 0.0
            },
            "thumbnail_url":
"https://images-cdn-api.getnexar.com/aod/thumbnail/timelapses/rideTimeLapse__0_2021052
0_085005.mp4/frame_3eff49272dc534da88517dffe94023ea.jpg",
"heading": "SOUTH_WEST",
            "captured_timezone_offset": 0
        },

...
]
}
```

Расшифровка полей:
- `frame_id` -- внутренний идентификатор снимка в Nexar
- `image_url` -- URL по которому можно скачать изображение
- `course_of_camera` -- азимут снимка в градусах (угол по отношению к направлению на сервер по часовой стрелке)
- `gps_point` -- координата снимка
- `captured_on_ms` -- время создания снимка, в milliseconds since epoch
- `captured_timezone_offset` -- смещение временной зоны от UTC, единицы измерения неизвестны

По соглашению, тарифицироваться будут только запросы на скачивание изображений, при этом пользоваться ручкой `/api/roadItem/findRawFrames/v2` можно без ограничений.


# Описание процесса импорта

Nexar рассматривается как потенциальная замена регулярным объездам в Израиле. Наше текущее покрытие там составляет около 17 тыс. км, а общая длина дорожной сети фанклассов 1-7 составляет около 60 тыс. км. Nexar реконмендует использовать H3-hexagon 12-го масштаба, их диаметр составляет около 27.5 метров, поэтому с их помощью можно достаточно точно отбирать фотографии, относящиеся к конкретной дороге. Для поиска фотографий для всей дорожной сети потребуется выполнить более 2 млн. запросов.

Чтобы сделать процесс обновления устойчивым к рестартам, и отзывчивым к изменению параметров импорта предлагается разделить территорию, подлежащую обновлению, на части, запоминать дату последнего обновления для каждой из частей, и выбирать для обновления в первую очередь те регионы, которые наиболее остро нуждаются в обновлении.

Разделять регионы предлагается по тайловой сетке 12-го масштаба, линейный размер одного тайла в районе экватора составляет около 10 км. Вся территория Израиля будет разедлена примерно на 330 тайлов.

## Описание служебных таблиц

Процесс будет использовать две таблицы для хранения служебной информации:
- существующую таблицу `service.import_config` с целевыми показателями по возрасту покрытия в регионе
- новую таблицу `service.nexar_tiles_update_info` -- с данными, собранными за прошлые обновления.

### service.import_config

```
     Column     |   Type
----------------+---------
 dataset        | text
 geo_id         | integer
 fc             | smallint
 threshold_days | integer
 Indexes:
    "import_config_pkey" PRIMARY KEY, btree (dataset, geo_id, fc)
 ```

### service.nexar_tiles_update_info

```
     Column     |   Type
----------------+----------
geo_id          | integer
fc              | smallint
x               | smallint
y               | smallint
z               | smallint
checked_at      | timestamp with time zone
median_photo_age  | interval day
Indexes:
    "nexar_tiles_update_info_pkey" PRIMARY KEY, btree (geo_id, fc, x, y, z)
```

### signals.nexar_frame_to_feature

В данной таблице будут сохранятся соответствия между снимками Nexar и нашими.

```
     Column     |   Type
----------------+----------
frame_id        | text
feature_id      | bigint
Indexes:
    "nexar_frame_to_feature" PRIMARY KEY, btree (frame_id)
```

## Алгоритм работы

1. Загрузить из БД содержимое `service.import_config`.
2. Загрузить данные о текущем покрытии дорожного графа.
3. Загрузить содержимое `service.nexar_tiles_update_info`.
4. Сформировать из загруженных данных список тайлов для обновления `[geo_id, fc, x, y, z]`.
5. Для каждого тайла `tile in [geo_id, fc, x, y, z]`:
    
    5.1. Вычислить медианное и максимальное значение возраста покрытия дорог `max_coverage_age` данного фанкласса внутри данного тайла.
    
    5.2. Если максимальный возраст меньше threshold_days, перейти к следующему тайлу на шаг 5.1
    
    5.3. На основании `nexar_tiles_update_info` для этого тайла оценить целесообразность проверки этого тайла. Если ранее этот тайл еще не проверялся -- однозначно целесообразно проверить. Если `now() > checked_at + median_photo_age`, то также есть вероятность, что внутри тайла что-то поменялось, целесообразно проверить.
    
    5.4. Вычислить коэффициент срочности проверки `update_priority = max_coverage_age / threshold_days`
6. В результате получится список тайлов для проверки `[geo_id, fc, x, y, z, update_priority]`, отсортировать полученный список по убыванию `update_priority`.
7. Для каждого тайла `tile in [geo_id, fc, x, y, z, update_priority]`:

    7.1 Получить все ребра дорожного графа фанкласса `fc`, пересекающиеся с тайлом.

    7.2 Вычислить их объединенную геометрию.

    7.3 Определить список `H3, heading`, покрывающих эту геометрию.

    7.4 Загрузить через Nexar API фотографии.

    7.5 Сопоставить загруженные фотографии с ребрами дорожного графа, определить множество фотографий, формирующих самое свежее покрытие для них.

    7.6 Вычислить медианный возраст фотографии `median_photo_age`.

    7.7 Отобрать среди фотографий те, что улучшают текущую свежесть покрытия.

    7.8 Загрузить изображения для отобранных фотографий.

    7.9 Сохранить загруженные фотографии в MDS и в базе.
    
    7.10 Обновить данные в таблице `service.nexar_tiles_update_info`.


## Логирования тарифицируемых запросов

Все запросы к Nexar API (сейчас это только запросы на скачивание изображений) подлежат логированию и сохранению в YT-таблицах. Предлагается использовать ту же [схему](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/doc/ugc_events_log), что используется для логирования событий UGC:
1. Процесс логирует все запросы к Nexar API в tskv-файл
2. Связка из logbroker + logfeller доставляет эти данные до YT-таблиц.
