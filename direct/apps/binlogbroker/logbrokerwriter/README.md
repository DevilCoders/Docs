# logbrokerwriter - демон, который записывает бинлоги в топик Logbroker

Настройки доступа к logbroker берутся средствами DirectConfig, из неймспейса `binlogbroker.logbroker`. 

### Пример запуска для одного mysql

    java -cp binlogbroker-logbrokerwriter.jar:binlogbroker-logbrokerwriter/'*' \
        -Djava.library.path=binlogbroker-logbrokerwriter \
        ru.yandex.direct.binlogbroker.logbrokerwriter.BinlogbrokerTool \
        --single-host-mysql \
        --mysql-database ppc --mysql-host localhost --mysql-port 3307 --mysql-username root

Как запустить тестовый MySQL в Docker - см. [direct/libs/binlog-model](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/binlog-model/README.md)

### Пример запуска для синхронизации devtest/dev7/test/prod

    java -cp binlogbroker-logbrokerwriter.jar:binlogbroker-logbrokerwriter/'*' \
        ru.yandex.direct.binlogbroker.logbrokerwriter.BinlogbrokerTool

Обычно не нужно указывать никакие аргументы, всё, что надо, берёт из окружения.
Можно указать аргументы:
 * `--shards` -- синхронизировать только указанные базы из db-config. По умолчанию синхронизируются все ppc.
 * `--db-config-env` -- трактовать db-config как конфиг для указанной среды, не меняя при этом среду для всего приложения. Путь к файлу db-config переопределяется pак обычно через system properties. 
 * `--logbroker-source-id-prefix` -- некая строка, с которой будут начинаться все передаваемые в logbroker source id. Может пригодиться чтобы записать данные не запоминая sequence id.
 * `--dont-truncate-fields` -- колонки, которые следует всегда оставлять в update/delete сообщениях (может быть полезно, если хочется по удаляемому объекту что-то узнавать, например, id родительского объекта)


### TVM2-аутентификация

Для logbroker-pre на ppcdevN нужно использовать дополнительные опции

    --logbroker-tvm-secret-path /etc/direct-tokens/tvm2_direct-ppcdata-binlog-test \
    --logbroker-tvm-client-id 2001405 \
    --logbroker-tvm-dst-client-id 2001147

Детали в DIRECTADMIN-6482.
