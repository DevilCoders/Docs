# Мониторинги

> Страница в процессе переезда с [wiki](https://wiki.yandex-team.ru/testpalm/testpalm-fe/).

## Основные ссылки

* AWACS: [балансер](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/testpalm-deploy.yandex-team.ru/show/), [мониторинги](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/testpalm-deploy.yandex-team.ru/monitoring/common/)
* [YDeploy](https://deploy.yandex-team.ru/stages/testpalm-production)
* ErrorBooster: [www](https://error.yandex-team.ru/projects/testpalm/projectDashboard), [api](https://error.yandex-team.ru/projects/testpalm-api/projectDashboard)
* [Время работы со смежными сервисами](https://yasm.yandex-team.ru/panel/robot-testpalm.testpalm.external/)
* [Время работы API](https://yasm.yandex-team.ru/panel/robot-testpalm.testpalm.handlers/)
* Базы данных
  * PostgreSQL. Хранится информация о пользовательских доступах (IDM).
    * [Кластер в Yandex Cloud](https://yc.yandex-team.ru/folders/foo17p6g2fdiaeousi4j/managed-postgresql/cluster/mdbongte1j9r2b65qes6)
  * MongoDB. Хранятся пользовательские данные (тест-кейсы, тест-раны, версии, …).
    * Основной кластер: [Yandex Cloud](https://yc.yandex-team.ru/folders/foo17p6g2fdiaeousi4j/managed-mongodb/cluster/mdber6ffp09r237ujnoo), [Панель в YASM](https://yasm.yandex-team.ru/panel/mrmlnc.testpalm_db1/)
    * Второй кластер: [Yandex Cloud](https://yc.yandex-team.ru/folders/foo17p6g2fdiaeousi4j/managed-mongodb/cluster/mdbbqf9qb3pqeo2ul83q), [Панель в YASM](https://yasm.yandex-team.ru/panel/mrmlnc.testpalm_db2/)

## Алерты

### [m.mdb.mongodb.tms.tms.tms-mongo-prod:max_mem_usage](https://juggler.yandex-team.ru/check_details?host=m.mdb.mongodb.tms.tms.tms-mongo-prod&service=max_mem_usage)

Потребление памяти на основном кластере MongoDB.

### [m.mdb.mongodb.tms.tms.tms-mongo-prod:used_space](https://juggler.yandex-team.ru/check_details?host=m.mdb.mongodb.tms.tms.tms-mongo-prod&service=used_space)

Остаток свободного места на основном кластере MongoDB.

⚠ Критичный. Если CRIT, то нужно чистить MongoDB в ближайшие дни.
