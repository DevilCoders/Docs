# ymod_mdb_sharder

## Что это?
Модуль для распределения шардов и пользователей почтовой метабазы между инстансами приложения.

Включает в себя два класса: ``shards_distributor`` и ``users_distributor``.

## shards_distributor
```c++
struct shards_distributor {
    void subscribe(const shard_ids_cb& on_acquire_shards, const shard_ids_cb& on_release_shards);
    void get_owner(task_context_ptr context, const shard_id& shard, const node_info_cb& cb);
};
```

Распределяет шарды почтовой базы. Позволяет подписаться на события захвата/потери шарда, а также узнавать кто владет
шардом. На случай, если шарды для приложения имеют разный вес, их можно сгруппировать в бакеты.

Для своей работы периодически получает список шардов из шарпея и захватывает распределенные локи в ylease.

### Настройки
```yaml
shards_polling_interval: 1.0 # интервал для поллинга списка шардов
sharpei: &sharpei_configuration
    host: sharpei.mail.yandex.net
    port: 80
    retries: 1 # ретраи реализуются средствами sharpei_client-а
    cache_ttl: 5s
    http_client_module: http_client # имя модуля http клиента для походов в шарпей
use_lease: true # захватывать локи через ylease сервер, либо захватывать все шарды безусловно
lease_module: lease_node # имя модуля ymod_lease
max_owned_locks: 25 # максимальное количество шардов/бакетов, которое может захватить один инстанс приложения
buckets: # разбиение шардов на бакеты
-   name: b1 # имя бакета
    shards: ['1', '5'] # id входящих в бакет шардов
open_bucket: b0 # бакет, в который помещаются шарды не указанные в конфиге
```

## users_distributor
```c++
struct users_distributor {
    void subscribe(const shard_id_with_uids_cb& on_acquire_users, const shard_id_with_uids_cb& on_release_users);
    void get_owner(task_context_ptr context, uid_t uid, const node_info_cb& cb);
    void set_polling_methods(const get_all_users_method& get_all_users, const get_changed_users_method& get_changed_users);
};
```

Распределяет почтовых пользователей. Позволяет подписаться на события захвата/потери пользователей, а также узнавать
кто владеет пользователем. Работает поверх shards_distributor.

Требует задания методов получения пользователей из шарда:

``get_all_users_method`` - метод, возвращающий всех пользователей из шарда

``get_changed_users_method`` - метод, принимающий несколько timestamp-ов и возвращающий новых/переехавших/удаленных
пользователей

С помощью этих двух методов осуществляется поллинг шарда и поддерживается актуальный спискок пользователей.

### Настройки
```yaml
shards_distributor_module: shards_distributor # имя модуля shards_distributor-а
sharpei:
    <<: *sharpei_configuration # настройки шарпея, копируются из секции shards_distributor-а средствами yaml
users_polling: # настройки для поллинга списка пользователей
    get_changed_users_interval: 20s # интервал, с которым вызывается get_changed_users_method
    get_all_users_interval: 5m # интервал, с которым вызывается get_all_users_method
```