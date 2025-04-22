# Crosslink
* Расположение в Platform (deploy) https://deploy.yandex-team.ru/projects/trains-crosslink
* Релизная машина https://rm.z.yandex-team.ru/component/rasp_crosslink
## Добавление данных
Код добавления данных лежит в `\tools`. Нужно собрать бинарник и запустить, указав в параметрах путь до файла с данными, токен, базу данных, endpoint и тип транспорта. Например:
```
/tools --database <db> --endpoint <endpoint> --file <file name> -t <token> (-tt | -bt)
```
База данных
* prod https://ydb.yandex-team.ru/db/ydb-ru/railway/production/train_purchase/browser
* dev https://ydb.yandex-team.ru/db/ydb-ru-prestable/railway/development/train_purchase/browser
* testing https://ydb.yandex-team.ru/db/ydb-ru-prestable/railway/testing/train_purchase/browser
## Запуск
Чтобы запустить локально достаточно сбилдить бинарник и запустить
```
cd $GOPATH/src/a.yandex-team.ru/travel/rasp/crosslink
ya make
YENV_TYPE=development YDB_TOKEN=<token> CROSSLINK_YDB_DATABASE=<db> CROSSLINK_YDB_ENDPOINT=<endpoint> ./cmd/cmd
```
## Пример
Хэндлер принимает два обязательных параметра - from_key, to_key, и два необзательных - graph_version и transport_type. По умолчанию transport_type=train. url-путь выглядит прмерно так `/crosslinks?from_key=<from_key>&to_key=<to_key>`.
В ответ придет json
```
[{"from":"Смоленск,Смоленская область","to":"Санкт-Петербург,Санкт-Петербург и Ленинградская область","toKey":"c2","toSlug":"saint-petersburg","toTitleRuGenitive":"Санкт-Петербурга","toTitleRuAccusative":"Санкт-Петербург","fromKey":"c12","fromSlug":"smolensk","fromTitleRuGenitive":"Смоленска","fromTitleRuAccusative":"Смоленск"},
{"from":"Тверь,Тверская область","to":"Санкт-Петербург,Санкт-Петербург и Ленинградская область","toKey":"c2","toSlug":"saint-petersburg","toTitleRuGenitive":"Санкт-Петербурга","toTitleRuAccusative":"Санкт-Петербург","fromKey":"c14","fromSlug":"tver","fromTitleRuGenitive":"Твери","fromTitleRuAccusative":"Тверь"},
{"from":"Санкт-Петербург,Санкт-Петербург и Ленинградская область","to":"Ярославль,Ярославская область","toKey":"c16","toSlug":"yaroslavl","toTitleRuGenitive":"Ярославля","toTitleRuAccusative":"Ярославль","fromKey":"c2","fromSlug":"saint-petersburg","fromTitleRuGenitive":"Санкт-Петербурга","fromTitleRuAccusative":"Санкт-Петербург"},
{"from":"Санкт-Петербург,Санкт-Петербург и Ленинградская область","to":"Оленегорск,Мурманская область","toKey":"c20155","toSlug":"olenegorsk","toTitleRuGenitive":"Оленегорска","toTitleRuAccusative":"Оленегорск","fromKey":"c2","fromSlug":"saint-petersburg","fromTitleRuGenitive":"Санкт-Петербурга","fromTitleRuAccusative":"Санкт-Петербург"},
{"from":"Самара,Самарская область","to":"Санкт-Петербург,Санкт-Петербург и Ленинградская область","toKey":"c2","toSlug":"saint-petersburg","toTitleRuGenitive":"Санкт-Петербурга","toTitleRuAccusative":"Санкт-Петербург","fromKey":"c51","fromSlug":"samara","fromTitleRuGenitive":"Самары","fromTitleRuAccusative":"Самару"}]
```
