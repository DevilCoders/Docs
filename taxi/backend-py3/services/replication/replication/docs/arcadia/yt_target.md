## Структурированный слой yt-targets/.../table.yaml
Здесь должно храниться описание YT таблицы.

* `description` — обязательное поле, краткое описание данных таблицы.
* `attributes` — атрибуты таблицы.
    * `schema` — список колонок таблицы, обязательное поле.
    Формат описания следующий:
        * `description` — текстовое описание колонки (обязательное).
        * `name` — имя колонки (обязательное).
        * `type` — тип колонки в YT (обязательное).
        Обычно используются только следующие типы:
        **any**, **boolean**, **string**,
        **double**, **int64**, **uint64**.
        * `sort_order` — **ascending**, если колонка является
        ключом сортировки.
        * `expression` — служебное поле для YT.
        Обычно использование выглядит так: **farm_hash(id)**.
        Нужно для того, чтобы YT на своей стороне равномерно распределял
        по таблетам строки таблиц — для этого его нужно добавлять
        самым первым и использовать `sort_order`.
    * `optimize_for` — **lookup** по умолчанию, можно выставить **scan**.
    * `dynamic` — **true** по умолчанию, для загрузки снапшотом должно быть явно указано **false**.
    * `compression_codec` — можно указать кастомный кодек компрессии.
    * `primary_medium` — можно выставить явно, по умолчанию будет стоять
    **default** для **map_reduce** кластеров и
    **ssd_blobs** для **runtime**.
  * `partitioning` — указывается для партицирования таблицы по дням/месяцам/годам. Формат:
      * `field_name` — имя поля по которому выбирается таблица (неизменяемая дата).
      * `items_to_keep` — количество таблиц, которое нужно хранить.
      * `rotate_policy` — как ротировать таблицы. Доступные опции:
        * `remove` - удаляет неактивные партиции
        * `eternal` - сохраняет все партиции. Если приходит документ из несуществующей
        еще партиции, создает её и вставляет запись
        * `none` - как `eternal`, но не создает партиции
        * `raw_history` - [сжимает](yt_raw_history.md) неактивные партиции и скипает статические при записи. Если приходит документ из несуществующей
        еще партиции, создает её и вставляет документ. При [перегрузке](faq.md#reinit) истории статические таблицы будут скипаться
        при записи.

        Для `eternal` не нужно указывать `items_to_keep`.
      * `rotate_settings` — кодеки сжатия. Указываются только для `rotate_policy: raw_history`,
      если нужно использовать не дефолтные. По умолчанию это
        * `compression_codec='brotli_8'` - подробнее про кодек можно посмотреть [тут](https://yt.yandex-team.ru/docs/description/common/compression#get_compression)
        * `erasure_codec='lrc_12_2_2'` - подробнее про кодек можно посмотреть [тут](https://yt.yandex-team.ru/docs/description/common/replication#erasure)

      * `type` — период партиционирования. Доступные опции:
      **by_days**, **by_months**, **by_years**.
      **by_field** — в этом случае имя партиции будет совпадать
      с значением поля `field_name`, и также нужно указать `output_table`,
      итоговый путь будет формата /path/{partition_value}/{output_table},
      где {partition_value} - значение, взятое из поля `field_name` в документе,
      **months_slice** - хранить в разрезе по месяцям, их количество при
      этом будет задаваться параметром `items_in_partition`.
      * `cast_to_date` — каст из типа `field_name` в utc дату. Доступные опции:
      **utc_from_timestamp** (по умолчанию), **utc_from_isostring**, **utc_from_microseconds**.
      * `output_table` — указывается только для типа **by_field**.
* `custom_bundles` - опциональное поле для динамических таблиц, дает
возможность указывать кастомные бандлы по окружениям для кластеров YT.
Бандлы указываются по кластерам для каждого окружения отдельно.
Если бандлы для какого-то окружения/кластера не указаны, используются бандлы по умолчанию. Пример:
    * `testing`:
        * `hahn`: `hahn-bundle`
    * `production`:
        * `arnold`: `arnold-bundle`
* `overrides` — список, с помощью которого можно переопределить любой из
атрибутов выше, в том числе поле `description` или схему таблицы
`attributes.schema`. Формат элементов:
    * `description` — необязательное поле с новым описанием.
    * `attributes` — формат тот же, но обязательных полей нет.
    * `partitioning` — формат тот же.
    * `cluster_groups` — список кластерных групп, для которых необходимо
    применить текущие параметры для переопределения.
    * `client_names` — список клиентов, для которых необходимо применить
    текущие параметры. Ключ не используется совместно с `cluster_groups`.
