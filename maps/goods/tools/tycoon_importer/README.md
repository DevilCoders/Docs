# Как выполнять импорт с нуля

Сперва надо всё очистить (если в базу что-то неудачно импортировали до этого):

1. Останавливаем async_processor
```bash
ya tool sedem p_exec --cmd 'yacare detach all' maps_geoapp_goods_async_processor_testing
```
Либо (для стейбла):
```bash
ya tool sedem p_exec --cmd 'yacare detach all' maps_geoapp_goods_async_processor_prestable maps_geoapp_goods_async_processor_stable
```
2. Чистим БД
```sql
TRUNCATE TABLE groups CASCADE;
TRUNCATE TABLE items CASCADE;
TRUNCATE TABLE photos CASCADE;
TRUNCATE TABLE tycoon_categories_to_groups CASCADE;
TRUNCATE TABLE published_items CASCADE;

ALTER SEQUENCE groups_id_seq RESTART WITH 1;
ALTER SEQUENCE photos_id_seq RESTART WITH 1;
ALTER SEQUENCE items_id_seq RESTART WITH 1;
```
3. Удаляем таблицу https://yt.yandex-team.ru/hahn/navigation?filter=old&path=//home/maps/geoapp/goods/experimental_trash/old_ids_table с YT
4. Запускаем скрипт companies_blacklist.sql для получения списка "плохих" компаний (не публикуемые: дубликаты, закрытые, геоспам, импорт из Фундука и т.п.)
```bash
yql --syntax-version 1 -i sql/companies_blacklist.sql
```

Запускаем импорт:

1. Выставить в настройках кластера ``log_statement=none``
2. Запустить скрипт и дождаться его завершения
```bash
export OAUTH=$(ya vault oauth)
export YQL_TOKEN=... # https://wiki.yandex-team.ru/market/analytics/stackoverflow-analitiki-marketa/yt/gde-vzjat-token-dlja-yt/

./tycoon_importer --import-categories --import-goods --env <stable|testing>
```
3. Запомнить номер последнего импортированного коммита на случай повторной заливки
4. Вернуть в настройках кластера ``log_statement=ddl``
5. Снова запустить async_processor
```bash
ya tool sedem p_exec --cmd 'yacare attach all' maps_geoapp_goods_async_processor_testing
```

# Как дозалить данные

Не забываем про ``log_statement=none``. Выполняем следующую команду:
```bash
./tycoon_importer --last-commit 1234 --import-categories --import-goods
```

Где ``--last-commit 1234`` &mdash; это последний коммит, импортированный в прошлый раз.

# Как залить модерационную информацию по фотографиям

Сначала надо запустить YQL-скрипт photo_moderation_verdicts_tycoon.sql, чтобы вытащить модерационные статусы из Фундука.
```bash
yql --syntax-version 1 -i sql/photo_moderation_verdicts_tycoon.sql
```

Затем выполнить следующую команду:

```bash
./tycoon_importer --import-moderations
```

# Как залить хэши

Сначала надо залить модерационную инфу по инструкции. Потом с помощью инструмента photo_moderations (есть свой README) выкачать хэши из Аватарницы на YT. Затем можно выполнить команду заливки хэшей:

```bash
./tycoon_importer --import-hashes
```

## FAQ по ошибкам

- При заливке хэшей вылетела ошибка уникальности, что делать?

Если текст ошибки примерно следующий:

```
psycopg2.errors.UniqueViolation: duplicate key value violates unique constraint "hash_unique_idx_moderation"
DETAIL:  Key (subject_hash)=(B4232185167255FBA996D56741C5E198) already exists.
```

То попробуйте выполнить в БД SQL-запрос следующего вида:

```sql
INSERT INTO image_hashes_with_urls (hash, url)
SELECT
    subject_hash AS hash,
    subject AS url
FROM moderation
WHERE
    subject_type='Image' AND
    LENGTH(subject_hash) = 32 AND
    subject_hash NOT IN (
        SELECT hash FROM image_hashes_with_urls
    );
```

- При заливке хэшей операция вылетела из-за lock timeout

Обычно такое происходит, если в данный момент кто-то создаёт сильную нагрузку на базу. Например, публикатор.
Операцию заливки хэшей можно просто перезапустить, т.к. она идемпотентна.

