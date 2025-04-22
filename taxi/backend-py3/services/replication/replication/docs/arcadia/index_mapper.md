## Маппер `$index`

Данный маппер предназначен для создания т.н. индексных таблиц. Так в YT не поддержаны индексы, то
необходимо создавать такие таблицы, которые являются склеиванием ключей разных таблиц.

Пример index-таблицы в yt: [ссылка](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/taxi/production/replica/postgres/cargo_c2c/indexes/clients_orders_created)

Пример правила с `$index` маппером: [ссылка](https://a.yandex-team.ru/arc_vcs/taxi/dmp/dwh/replication_rules/replication_rules/cargo_c2c/clients_orders.yaml#L23)

Настройки в секции `target` правила репликации у этого маппера следующие:

* `index_settings` *required* — секция настроек маппера.
    * `yt_columns_info` *required* — поле для описания колонок в YT-таблице с ключами.
       Здесь должны указываться только ключи.
        * `name` *required* — имя колонки в YT-таблице.
        * `type` *required* — тип колонки в YT-таблице.
        * `sort_order` - указать `ascending`
        * `description` - описание колонки в YT-таблиц
        * `cast` — алиас функции, которая будет использоваться для обработки
        колонки. См. доступные функции в секции [мапперы](mappers.md#rabota-s-mapperami)
        * `input_column` — имя входной колонки, если оно отличается от имени колонки на YT.
        * `input_transform` — алиас функции, которая принимает на вход документ целиком и отдает
         единственное значение. См. подробное описание в секции [мапперы](mappers.md#rabota-s-mapperami)
        * `expression` - техническое поле, указывать не обязательно. См. подробное описание в секции [yt-таргета](yt_target.md#strukturirovannyj-sloj-yt-targets//tableyaml)
    * `description` — опциональное поле, позволяющее указать описание таблицы на YT. Если оно не указано,
    описание будет сгенерировано автоматически.
    * `pre_map_funcs` - опциональное поле для добавления дополнительных премапперов.
    * `yt_attributes` - опциональное поле для передачи дополнительных параметров
      (см. описание атрибутов для [yt-таргета](yt_target.md#strukturirovannyj-sloj-yt-targets//tableyaml) - все, кроме `schema`).
{% note warning %}

Если вы указываете `partial_update: true` для таргета-индекса, то также укажите `common_mapper_columns: true`.
Подробнее про `partial_update` в описании [таргетов](how_to_start.md#target)

{% endnote %}
