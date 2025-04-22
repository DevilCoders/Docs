# Данные CDP
Тут будет храниться набор всех "мест с данными" для CDP.

## ClickHouse
Кластер `mtcdp` в MDB:
- Production - https://yc.yandex-team.ru/folders/foori5uktoh2v12cbltq/managed-clickhouse/cluster/mdbcgg3ua7bothld2oh0
- Testing - https://yc.yandex-team.ru/folders/foori5uktoh2v12cbltq/managed-clickhouse/cluster/mdb8pmtavv48juqeirlu

## Logbroker
Для нужд CDP используется LBKX инсталляция Logbroker и аккаунт metrika:
- Production - https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp
- Testing - https://logbroker.yandex-team.ru/lbkx/accounts/metrika/test/experiments/cdp

## YDB
- Production - https://ydb.yandex-team.ru/db/ydb-ru/metrika/production/cdp/browser
- Testing - https://ydb.yandex-team.ru/db/ydb-ru-prestable/metrika/testing/cdp/browser
- Development - https://ydb.yandex-team.ru/db/ydb-ru-prestable/metrika/development/cdp/browser

## MySQL
Для работы API (аутентификация и метаданные Яндекс.Метрики) используется железный MySQL кластер под название mtacs
