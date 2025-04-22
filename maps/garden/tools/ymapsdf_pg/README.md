# Конвертер ymapsdf таблиц из YT в Postgres

Кластер Postgres: https://yc.yandex-team.ru/folders/fooj6ecqh8rsdsnj5806/managed-postgresql/cluster/mdbvi5pb5jaqt2uhnknd?section=overview
Пароль от Postgres в Секретнице: https://yav.yandex-team.ru/secret/sec-01fkgjxerd4aad67cxvjbzbprb

0. Установите сертификат:

```
mkdir -p ~/.postgresql && \
wget "https://crls.yandex.net/allCAs.pem" -O ~/.postgresql/root.crt && \
chmod 0600 ~/.postgresql/root.crt
```

1. Перейдите в папку `maps/doc/schemas/ymapsdf/package`.
2. Выполните команду `ya make`, чтобы сгенерировать SQL-скрипты в папке.
3. Перейдите в папку `maps/garden/tools/ymapsdf_pg/bin`.
4. Выполните команду `ya make -r`, чтобы собрать тул.
5. Запустите тул (нужно указать путь к таблице и путь к скрипту создания схемы):

```
./ymapsdf_pg --yt-table-path=<yt_path> --sql-schema-path ../../../../doc/schemas/ymapsdf/package/ymapsdf_create.sql
```
