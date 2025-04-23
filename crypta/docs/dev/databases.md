CNAME для доступа к базам
=========================

Для fault tolerance в облачных базах используется CNAME, указывающий на мастер-ноду кластера. Имена достаточно длинные, поэтому для простоты мы используем свои CNAME на эти CNAME:

* `production.database.crypta.yandex-team.ru` для базы `cryptadb` (указывает на `c-8c8b283d-8154-49d9-a423-fb159d62c15f.rw.db.yandex.net`)
* `testing.database.crypta.yandex-team.ru` для базы `cryptadbtest` (указывает на `c-33d1fc5f-871a-4399-b06e-14d677f27807.rw.db.yandex.net`)
* `sentry.database.crypta.yandex-team.ru` для базы `sentry` (указывает на `c-38fbc20b-9ac0-4b13-b560-df4c6c21755e.rw.db.yandex.net`)
* `special.database.crypta.yandex.net` для баз `dating`, `mentor` и других спецпроектов (указывает на `c-mdb5b5ntga89c55sjn5h.rw.db.yandex.net`)
