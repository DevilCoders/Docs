# Mongo reader tool

Тул выполняет подключение к монге, листит её коллеции, выводит количество элементов в них и предоставляет доступ к IPython-консоли.
Внутри уже определены некоторые функции, которые кто-то когда-то нашёл полезными.

## Использование

В директории с тулом нужно запустить следующую команду:

```bash
MONGO_CONFIG_PATH='<path_to_mongo_config>' ya py -3
```

Пример конфига для тестинга:

```json
{
    "mongo": {
        "host": "sas-sp7cqv46oj8xw3bx.db.yandex.net,vla-p53l0eth3t8uvyol.db.yandex.net,sas-pj82weuiy3cszjis.db.yandex.net",
        "port": 27018,
        "dbname": "garden_server",
        "replicaset": "rs01",
        "ssl": true,
        "ssl_ca_certs": "/usr/local/share/ca-certificates/YandexInternalRootCA.crt",
        "authSource": "garden_server",
        "username": <USERNAME_HERE>,
        "password": <PASSWORD_HERE>
    }
}
```

И дальше пишем запросы. Например:

```ipython
In [1]: from collections import Counter

In [2]: c = Counter(type(unpack_resource(resource_from_proto_bytes(r['proto']))) for r in db.resources.find())

In [3]: print_table(c.most_common())
------------------------------------------------------------------------------------------  ------
<class 'maps.garden.sdk.resources.file.FileResource'>                                    104639
<class 'maps.garden.sdk.resources.yandex_mds.YMDSFileResource'>                          100409
<class 'maps.garden.sdk.resources.dir.DirResource'>                                       76219
<class 'maps.garden.sdk.yt.yt_table.YtTableResource'>                                     23818
<class 'maps.garden.sdk.resources.resource.Resource'>                                     17846
<class 'maps.garden.sdk.resources.build_params.BuildParamsResource'>                      12217
<class 'maps.garden.sdk.resources.remote_dir.RemoteDirResource'>                           6932
<class 'maps.garden.sdk.resources.python.PythonResource'>                                  4653
<class 'maps.garden.sdk.resources.flag.FlagResource'>                                      2668
<class 'maps.garden.sdk.yt.yt_source_path.YtSourcePathResource'>                           1096
<class 'maps.garden.sdk.resources.url.UrlResource'>                                         453
<class 'maps.garden.sdk.sandbox.resources.SandboxResource'>                                 349
<class 'maps.garden.sdk.yt.yt_file.YtFileResource'>                                         302
<class 'maps.garden.sdk.ecstatic.resources.DatasetResource'>                                292
<class 'maps.garden.sdk.yt.yt_directory.YtDirectoryResource'>                                32
<class 'maps.garden.sdk.sandbox.resources.SandboxReleaseStatusResource'>                      3
------------------------------------------------------------------------------------------  ------

```
