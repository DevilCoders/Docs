# Общее
[Схема](mopsdb.sql)

## Выкатка миграций
Применение миграций происходит при помощи [pgmigrate](https://github.com/yandex/pgmigrate) ( [руководство](https://github.com/yandex/pgmigrate/blob/master/doc/tutorial.md) по использованию ).
Пример накатывания миграции (нужен доступ до хоста). Полезно будет подсмотреть в .pgpass на машинках ;)
```
gzalex@gzalex-dev:~/arcadia/mail/pg/mopsdb$ pgmigrate \
  -c "host=c-<cluster-id>.rw.db.yandex.net port=6432 dbname=mopsdb user=tech" \
  -t latest -vv \
  migrate
```

## Кроны
На каждое окружение есть по одной машинке в qloud, на которой запускаются скрипты.

Qloud: [mopsdb-crons](https://platform.yandex-team.ru/projects/mail/mopsdb-crons)

Код скриптов: <https://a.yandex-team.ru/arc/trunk/arcadia/mail/pg/mopsdb/cron>

Собираются кроны [джобой](https://common.jenkins.mail.yandex.net/job/build-mopsdb-cron-package/), выкладываются в qloud.

# Окружения
## Прод
cluster-id: mdbm8poisf3aefa4bk1v

Страница кластера в yc: <https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql/cluster/mdbm8poisf3aefa4bk1v>

Графики в головане: <https://yasm.yandex-team.ru/template/panel/mopsdb_panel/env=production/>

## Корп
cluster-id: mdbiu006uv3uvoi2791i

Страница кластера в yc: <https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql/cluster/mdbiu006uv3uvoi2791i>

Графики в головане: <https://yasm.yandex-team.ru/template/panel/mopsdb_panel/env=intranet-production/>

## QA
cluster-id: mdbjr3fs0g3tqa2ald7s

Страница кластера в yc: <https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql/cluster/mdbjr3fs0g3tqa2ald7s>

Графики в головане: <https://yasm.yandex-team.ru/template/panel/mopsdb_panel/env=prestable/>

## Корп QA
cluster-id: mdb1il09tq2hlg1sfffl

Страница кластера в yc: <https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql/cluster/mdb1il09tq2hlg1sfffl>

Графики в головане: <https://yasm.yandex-team.ru/template/panel/mopsdb_panel/env=intranet-prestable/>

## Тестинг
cluster-id: mdbr7r784pshojfeb0uh

Страница кластера в yc: <https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql/cluster/mdbr7r784pshojfeb0uh>

Графики в головане: <https://yasm.yandex-team.ru/template/panel/mopsdb_panel/env=testing/>

## Load
cluster-id: mdb9gu9a659vajjvoc32

Страница кластера в yc: <https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql/cluster/mdb9gu9a659vajjvoc32>

Графики в головане: <https://yasm.yandex-team.ru/template/panel/mopsdb_panel/env=load/>
