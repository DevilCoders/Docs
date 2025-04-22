# bstransport/proto - модель данных, экспортируемых в БК

В этом модуле хранятся proto-описания структур данных, отправляемых в БК.

[справочно: схемы контент-системы](https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/cs/libs/direct_object/protos)
[json-схема транспорта](https://a.yandex-team.ru/arc/trunk/arcadia/yabs/interface/yabs-bssoap-www/Yabs/JsonSchemas/update_data.json)

При изменении схем нужно перегенировать проект.

__НЕ ПРОДАКШН__
Код нельзя импортировать или использовать в продакшен, так как находится в стадии разработки.
Подробное описание появится позднее. Вопросы можно задавать ppalex@

##Генерация meta-информации для YQL
Парсер в YQL, кажется, чувствителен к лишним полям и несовпадению числовых типов
1. собрать protoc `ya make arcadia/contrib/tools/protoc`
2. из директории с proto выполнить
```
PATH="~/arcadia/contrib/tools/protoc:$PATH" ya yql proto_field \
-c hahn -t //home/direct/tmp/p -n data  -i ~/repo/arcadia \ 
-p requests.proto -m NDirect.NBSExport.FeedRequestMessage \
-a ~/repo/arcadia
```
Здесь `-p requests.proto` - файл который мы хотим упаковать,
`-m NDirect.NBSExport.FeedRequestMessage` - какое сообщение из него.
Команда упадет с ошибкой (нет yt, нет таблицы), но выведет meta - её нужно разэкранировать, поменять:
* `"format": "json"`
* `"view":{"enum":"number"}`
и можно использовать в YQL
