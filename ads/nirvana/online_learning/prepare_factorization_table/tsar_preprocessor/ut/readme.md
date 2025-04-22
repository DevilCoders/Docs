При поломке(изменении) логов нужно проделать следующие действия:
* Поправить [tsar_preprocessor.py](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/online_learning/prepare_factorization_table/tsar_preprocessor/tsar_preprocessor.py)
* Сгенерировать свежие логи с помощью запроса (поправив везде даты) [test_tables.yql](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/online_learning/prepare_factorization_table/tsar_preprocessor/ut/test_tables.sql)
* Поправить дату в [conftest.py](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/online_learning/prepare_factorization_table/tsar_preprocessor/ut/conftest.py?rev=5293334#L20)
* Запустить `ya make -ttt . -Z --test-param download --test-stderr`
* Изменить ресурсы таблиц в [ya.make](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/online_learning/prepare_factorization_table/tsar_preprocessor/ut/ya.make) на те, которые будут написаные в stdout
