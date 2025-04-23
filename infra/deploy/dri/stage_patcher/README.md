# stage_patcher

Можно использовать для массового обновления всех stage на кластере.

## Описание

Скрипт итерируется по заданным кластерам и берет все stage, соответствующие фильтру `filter` (синтаксис как у обычных запросов в yp).

У всех выбранных stage он увеличивает ревизию на 1, что соответствует zerodiff с точки зрения спеки пользователя, но с точки зрения инфраструктурных компонент происходит обновление.

Если нужно сделать более сложное обновление, надо дописать код [вот сюда](https://a.yandex-team.ru/arc/trunk/arcadia/infra/deploy/dri/stage_patcher/__main__.py?rev=6015579#L108-111).

Продакшн лучше обновлять аккуратно - по частям. Например, фильтром вроде `-f '[/meta/id] >= "a" and [/meta/id] < "b"'` или при помощи опции `--update-window`.

Обязательно нужно указать читаемый `revision-description`, чтобы у пользователей не было вопросов, почему какой-то робот обновил их stage.

## Пример использования

Пример использования для zerodiff всех stage с id `chegoryu-test-tvm`, `chegoryu-test-tvm-new` на кластерах `sas-test` и `xdc`:

```
$ ./stage-patcher sas-test xdc --filter "[/meta/id]='chegoryu-test-tvm' or [/meta/id]='chegoryu-test-tvm-new'" --select-limit 10 --update-window 50 --time-interval 1 --revision-description 'DEPLOY-12345 test zerodiff'
--------------------------------------------------
Update cluster sas-test
Use yp token from file /home/chegoryu/.yp/token
No stages to update
Cluster sas-test skiped
--------------------------------------------------
Update cluster xdc
Use yp token from file /home/chegoryu/.yp/token
Selected 2 stages:
chegoryu-test-tvm
chegoryu-test-tvm-new

Continue? (y/n): y
Update stage chegoryu-test-tvm
Start transaction
Started
Get revision
Current revision 10
Update to revision 11
Updated
Commit
Success commit
Success update chegoryu-test-tvm

Update stage chegoryu-test-tvm-new
Start transaction
Started
Get revision
Current revision 1
Update to revision 2
Updated
Commit
Success commit
Success update chegoryu-test-tvm-new

Updated 2/2
No errors
Press enter to continue
```
