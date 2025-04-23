Тулза позволяет подключиться к базам в mdb, описанным в [конфиге](https://bishop.mtrs.yandex-team.ru/template/mdb-database-client.xml).
На данный момент поддержаны ClickHouse, PostgreSQL и MySQL.
Работоспособность приложения проверялась только на Linux.

Требования:
1. Должен работать ssh-agent. С помощью ssh включа получается OAuth токен для доступа до [сервисов](https://oauth.yandex-team.ru/client/76ce0ee44fbc4c87bd3ad5472ed96446).
2. Должны быть установлены и настроены клиенты для подключения к базам. Примеры настроек можно найти в mdb за кнопкой "подключиться".
3. У вас должен быть доступ до __всех__ секретов, указанных в конфиге. Архитектурное ограничение.

Новые базы можно свободно добавлять в конфиг в любой момент без аппрувов.

Пример работы:
```
$ ./mdb-database-client -c mtstatlog

Going to use mtstatlog cluster
Going to use host sas-2z5l516j4qtddb29.db.yandex.net

ClickHouse client version 20.5.3.27 (official build).
Connecting to sas-2z5l516j4qtddb29.db.yandex.net:9440 as user metrika.
Connected to ClickHouse server version 20.8.3 revision 54438.

ClickHouse client version is older than ClickHouse server. It may lack support for new features.

sas-2z5l516j4qtddb29.db.yandex.net :) select 1

SELECT 1

┌─1─┐
│ 1 │
└───┘

1 rows in set. Elapsed: 0.044 sec.

sas-2z5l516j4qtddb29.db.yandex.net :) Bye.
```
