# partners-proxy-lite

Легкая версия партнерского прокси. Только проксирование через nginx.

Подходит для использования с партнерами, берущими плату за каждый ip-адрес, для которого открывают доступ.

Использование:
- Аэропорт DME: `/airport/dme/ -> http://timetable.dme.ru/`

Используемый пул ipv4-адресов:
- VLA: [5.255.209.90/31](https://racktables.yandex-team.ru/index.php?page=ipv4net&id=14150)
- SAS: [5.255.210.38/31](https://racktables.yandex-team.ru/index.php?page=ipv4net&id=14149)
- MAN: [77.88.48.208/31](https://racktables.yandex-team.ru/index.php?page=ipv4net&id=14151)

Привязка ipv4 адресов к подам, можно смотреть только по ДЦ:
```
$ ./ya tool yp select --address SAS internet_address --filter '[/meta/ip4_address_pool_id]="2029:1512"' --selector /spec/ip4_address --selector /status/pod_id
+-------------------+--------------------+
| /spec/ip4_address |   /status/pod_id   |
+-------------------+--------------------+
|   "5.255.210.38"  | "5ut65pphwnxkijdn" |
+-------------------+--------------------+
1 object(s) selected
```

## Сборка докер образа локально

```
$ ./ya package --docker --docker-registry registry.yandex.net --docker-repository avia travel/avia/partners-proxy-lite/pkg.json
```
