
Диагностика:

Чтобы понять, почему сработало [событие](https://juggler.yandex-team.ru/raw_events/?query=service%3Dbalancer_status%26tag%3Dtype_balancer_status&project=nocdev) **balancer_status** идем на мастера и грепаем логи
```shell
journalctl -u slbcloghandler-server.service -S -10m | grep vla2-9lb18b
```
Например, так:
```
июл 27 12:29:42 vla-sch1.net.yandex.net slbcloghandler[75234]: time="2022-07-27T12:29:42+03:00" level=error msg="bad data status" host=vla2-9lb18b.yndx.net status="unable to get sta ConnectionRefusedError(111, 'Con"
```
Дальше идем на хост с проблемой и смотрим
```shell
sudo -u slbcloghandler slbch_client -o - | python3 -m json.tool
```
```
2022-07-27 12:35:35,291 noc.slbcloghandler.cmd.slbch_client.slbch_client - slbch_client.py:132 - _update_data() - ERROR - unable to get sta. [Errno 111] Connection refused <urlopen error [Errno 13] Permission denied>
2022-07-27 12:35:35,301 noc.slbcloghandler.cmd.slbch_client.slbch_client - slbch_client.py:132 - _update_data() - ERROR - unable to get sta. [Errno 111] Connection refused <urlopen error [Errno 13] Permission denied>
{
    "sta": {},
    "status": "unable to get sta ConnectionRefusedError(111, 'Connection refused') URLError(PermissionError(13, 'Permission denied'))",
    "addrs": {
...
```
Если самостоятельно не удалось разобраться почему slbch_client выдает ошибку, привлекаем команду ТТ.
