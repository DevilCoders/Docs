## Скрипты

### dataproddb_to_mdb.sh
Скрипт для копирования базы с dataprod-db в новый кластер mdb4scmh2qhed40lergn

Пример запуска: ./dataproddb_to_mdb.sh mapspro_user


### new_db_from_template.sh
Скрипт для копирования базы mapspro_template в другую внутри кластера mdb4scmh2qhed40lergn

Пример запуска: ./new_db_from_template.sh mapspro_user


### update_acl.sh
Скрипт для копирования схемы acl из продакшена (core/mapspro) в другую базу в кластере mdb4scmh2qhed40lergn<br/>
Можно использовать для обновления шаблона mapspro_template

Пример запуска: ./update_acl.sh mapspro_template


### upgrade.sh
Скрипт для накатывания миграции на чистую базу в кластере mdb4scmh2qhed40lergn

Необходимо прописать environment/dbname в ../config.development.yaml

Пример запуска: ./upgrade.sh mapspro_tmp


### Новая база для нового пользователя
Нужна роль администратора MDB https://abc.yandex-team.ru/services/maps-core-nmaps

1. Добавить базу mapspro_`user` в кластер (пользователь mapspro, лучше указать en_US.UTF8 вместо C в LC_COLLATE/LC_TYPE)<br/>
Перед списком баз в правом верхнем углу есть кнопка в UI: "+ Добавить"
[databases](https://yc.yandex-team.ru/folders/foodd8k45ru3cjjo3nte/managed-postgresql/cluster/mdb4scmh2qhed40lergn?section=databases)

2. Добавить расширения.
В списке баз справа 3 точки, выбрать пункт "Настроить расширения PostgreSQL)
[databases](https://yc.yandex-team.ru/folders/foodd8k45ru3cjjo3nte/managed-postgresql/cluster/mdb4scmh2qhed40lergn?section=databases)
   * btree_gin
   * btree_gist
   * hstore
   * pg_trgm
   * postgis

3. Запусить скрипт:
PGPASSWORD=`dev-пароль в MDB` ./new_db_from_template.sh mapspro_`user`

4. Необходимо прописать environment/dbname в ../config.development.yaml
