## *populate_sharddb.py*

Добавляет указанные в конфиге шарды почтовой метабазы в шарддб.

### Конфигурация шардов maildb

Описывается в файле _config.yml_. Задает шарды метабазы в формате

```yaml
shards:
    - shard_name: pgload03
      instances:
        - host: pgload03e.mail.yandex.net
          dc: iva
        - host: pgload03f.mail.yandex.net
          dc: myt
          ...
```

_Для подключения к шардам maildb хосты берутся из конфига, а пароль и сертификат из [секрета](https://yav.yandex-team.ru/secret/sec-01e734b46bpyqt75y1tpkemdx2/explore/versions)._
См. `ShardDbAdaptor._get_maildb_adaptor_params`.

### Конфигурация целевой sharddb

Все параметры, необходимые для подключения, хранятся в коде в переменной `sharddb_adaptor_params`.
Пароль и сертификат берутся из
[секрета](https://yav.yandex-team.ru/secret/sec-01e734b46bpyqt75y1tpkemdx2/explore/versions).

### Запуск:

Из данной директории запускается так:

```
$ ya make && ./populate_sharddb
```

параметров командной строки у этого скрипта нет.

### Текущие ограничения

* Предполагает, что и в **sharddb**, и в **maildb** есть пользователь **sharpei** с одинаковым паролем.

* Кластер **sharddb** задается id кластера в [облаке](https://yc.yandex-team.ru/), а **maildb** - списком хостов. \
Это разница определяет то, какой из классов - `DBConnectionProvider` или `YcDBConnectionProvider` - \
будет выбран при подключении к бд.

Все hardcoded значения можно посмотреть в коде в мапке `ShardDbAdaptor.CONSTANTS`.
