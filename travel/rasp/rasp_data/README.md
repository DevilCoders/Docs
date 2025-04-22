# Что это

`travel/rasp/rasp_data/dumper` - это приложение, отвечающее за выгрузку данных из базы Расписаний в pb2 файлы.

Используется в sandbox задаче: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/rasp/DumpRaspData

`travel/rasp/rasp_data/resource_checker` - приложение, проверяющее целостность и правильность сгенерированных дампером ресурсов.
[Подробнее](./resource_checker)

Используется в sandbox задаче: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/rasp/CheckRaspDataResources

На данный момент для того чтобы обновить дамперы, используемые в `DumpRaspData` нужно выполнить команду:
```(sh)
ya package --upload --sandbox --upload-resource-type=DUMP_RASP_DATA_RESOURCE --upload-resource-attr=resource_name=dumper dumper/pkg.json
```

# Формат хранения данных

Сериализация и запись в файл proto сообщений осуществляется при помощи библиотеки: https://a.yandex-team.ru/arc/trunk/arcadia/library/protobuf/protofile/protofile.cpp?rev=5760257#L69

В результате формат файла получается такой: `MsgLen1->Msg1->MsgLen2->Msg2->MsgLen3->Msg3`, где `MsgLenN` - длина следующего сообщения как `fixed size int32`, а `MsgN` - собственно сообщение.

# Как потреблять

На данный момент есть два способа потребить ресурсы.
1) Ресурсы `DUMP_RASP_DATA_RESOURCE`, нужные ищем по аттрибуту `resource_name`
2) Используем ресурсы вида `TRAVEL_DICT_{project}_{object_type}_{env}`, например `TRAVEL_DICT_RASP_COUNTRY_PROD`

# Разработка

## Локальный запуск

```
./ya make --checkout --yt-store travel/rasp/rasp_data/dumper/bin
./travel/rasp/rasp_data/dumper/bin/dumper --geobasePath=/var/cache/geobase/geodata4.bin --out=./ --tankerAuthToken=XXX --user=mysql-user
```
