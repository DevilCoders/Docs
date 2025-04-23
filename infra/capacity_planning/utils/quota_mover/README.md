# Quota mover

## Токен

Получаем токен [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=0e38277ed0e24567a833cdc7e2cb1683)
и сохраням его в `~/.d/token`

## Сборка

`ya make -r`

## Параметры

 - `--list-providers` - вывести список всех провайдеров<br>
 - `--list-resources` - вывести список доступных ресурсов<br>
 - `--list-segments` - выыести список сегментов<br>
 - `--folder-state` - вывести состояние фолдера<br>
 - `--move` - передать ресурсы из одного фолдера в другой<br>
 - `--rise` - поднять квоту из акаунта<br>
 - `--drop` - спустить квоту в акаунт<br>
 - `--token` - токен, если не указан, ищется в `~/.d/token`<br>
 - `--test` - использовать тестовый d-api<br>
 - `--provider <provider>` - slug провайдера<br>
 - `--segments <segment1> <segment2>` - сегменты,
     если имена сегментов не пересекаются по типам сегментов - допустимо указывать их без типа сегментации
     например `--segment sas default`, если же имя сегмента встречается в разных типах сегментации необходимо дополнительно указывать и его<br>
     т.е. `--segment cluster:sas node_segment:default`<br>
 - `--from-service <id>` - сервис-источник, если не указан - берется сервис провайдера<br>
 - `--to-service <id>` - целевой сервис<br>
 - `--from-folder <name>` - фолдер-источник, если не указан - используется default, или reserve, если это сервис провайдера<br>
 - `--to-folder <name>` - целевой фолдер сервиса, если не указан - используется default<br>
 - `--from-account <account_id>` - акуаунт, из которого будет происходить подьем<br>
 - `--to-account <account_id>` - акаунт, в который будет спущена квота<br>
 - `--resource <res:amount:unit> <res:amount:unit> ...` передаваемые ресурсы<br>

## Примеры комманд

### Просмотр доступных провайдеров
`./quota_mover --list-providers`

### Типы ресурсов провайдера
`./quota_mover --list-resources --provider yp-prod`

### Сегменты провайдера
`./quota_mover --list-resources --provider yp-prod`

### Текущая квота сервиса
`./quota_mover --folder-state --from-service 4136`

### Перенос квоты между балансами двух сервисов
переносим 10Mb/s ssd_bandwidth из сервиса 4136 в сервис 35027
```
./quota_mover
--move
--provider yp-prod
--segments sas gpu-dev
--from-service 4136
--to-service 35027
--resource ssd_disk_bandwidth:10:mebibytesPerSecond
```

### Перенос квоты между двумя сервисами с подъемом и спуском
поднимаем 10Mb/s ssd_bandwidth и 1 core cpu из сервиса 4136, передаем его в сервис 35027 и спускаем в аккаунт
```
./quota_mover
--rise
--move
--drop
--provider yp-prod
--segments sas gpu-dev
--from-service 4136
--to-service 35027
--resource ssd_disk_bandwidth:10:mebibytesPerSecond cpu_capacity:1:cores
```

### Перенос всей квоты из одного сервиса в другой
работает для сервисов, в котором выбранный ресурс вообще не аллоцирован, т.е. подходит для выноса освободившейся квоты из закрывающегося сервиса
```
./quota_mover
--rise
--move
--provider yp-prod
--segments sas gpu-dev
--from-service 35027
--to-service 4136
--resource ssd_disk_bandwidth:all cpu_capacity:all
```

### Запросить квоту у провайдера
```
./quota_mover
--move
--provider yp-prod
--segments sas gpu-dev
--to-service 4136
--resource ssd_disk_bandwidth:10:mebibytesPerSecond
```

### Вернуть квоту провайдеру
```
./quota_mover
--move
--provider yp-prod
--segments sas gpu-dev
--from-service 4136
--resource ssd_disk_bandwidth:10:mebibytesPerSecond
```
