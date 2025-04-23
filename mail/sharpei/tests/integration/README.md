### Общая информация

Тесты запускаются командой `ya make -ttt --private-ram-drive` из корня проекта. Последняя опция заметно ускоряет прогон тестов (MAILPG-4571).

Тесты построены на основе [devpack](https://a.yandex-team.ru/arc/trunk/arcadia/mail/devpack/) и [pytest-bdd](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/python/pytest-bdd).
Девпачный sharpei лежит [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/mail/devpack/lib/components/sharpei.py).
[Основной Шарпей](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/tests/integration/conftest.py?rev=r8464965#L161) зависит от девпачных же ShardDb (локальная shardbb) и Mdb (локальная maildb из одного или более шардов). Ответы blackbox мокаются посредством [pyremock](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/testing/pyremock?rev=r8274749).
[Sharpei-cloud](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/tests/integration/conftest.py?rev=r8464965#L93) зависит от девпачного [CloudCluster](https://a.yandex-team.ru/arc/trunk/arcadia/mail/devpack/lib/components/cloud_cluster.py?rev=r8440163#L4). Ответы iam и yc мокаются посредством pyremock.

Как и положено в pytest, все зависимости приносятся через структуру 
[context](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/tests/integration/conftest.py?rev=r7930281#L62).
Она не случайно имеет `scope='module'`: тесты [распараллелены](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/tests/integration/ya.make?rev=r7930281#L14) по модулям, при этом каждый модуль содержит тесты ровно из одной фикстуры. \
Также стоит отметить, что в некоторых фикстурах ([пример](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/tests/integration/feature/conninfo_when_shard_has_only_replica_host.feature?rev=r7006103#L8)) первым шагом делается необходимая подготовительная работа. Это означает, что нельзя запускать отдельные тесты из этого модуля без этого подготовительного шага.

Тестируются все три семейства [API](https://wiki.yandex-team.ru/mail/pg/sharpei/interface/): почтовое, дисковое и датасинковое.
Тесты последних двух живут в поддиректории `datasync_and_disk_tests`.
API [настраивается](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/tests/integration/datasync_and_disk_tests/create_user_tests_for_disk_api.py?rev=r7930281#L9) через структуру `settings`, о которой написано ниже.
Также есть тесты для sharpei-cloud. Они живут в поддиректории `cloud`. Для них в структурке `settings` выставляется `kind = cloud`.

### Settings

Параметры вроде конфигурации шардов и типа апи (почта / диск / датасинк) конфигурируются для каждого модуля с тестами отдельно посредствам определения объекта с названием settings.
Выглядит это [так](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/tests/integration/test_conninfo_only_master.py?rev=r6839226#L5).
Схема этого объекта расположена [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/tests/integration/schemas/test_settings.json?rev=r6839226).
Можно не определять этот объект вовсе или определить только часть полей - остальное будет заполнено
[автоматикой](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei/tests/integration/util.py?rev=r6839226#L26) дефолтными значениями, которые указаны в схеме.
