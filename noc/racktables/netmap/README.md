# Зачем?
Этот readme описывает создание БД для netmap, если не получается воспользоваться традиционным для него способом - dump/restore. 

# Создание БД
## Права
### racktables
```sql
GRANT ALL PRIVILEGES ON `netmap`.* TO 'racktables'@'%';
```

### racktables_ro
```sql
GRANT SELECT ON `netmap`.* TO 'racktables_ro'@'%';
```

## Создание таблиц
```sql

CREATE TABLE `InstantL1` (
    `ttime`     int(11) NOT NULL,
    `object_id` int(11) NOT NULL,
    `port_id`   int(11) NOT NULL,
    `status`    enum('up','down','disabled') NOT NULL,
    PRIMARY KEY (`port_id`),
    UNIQUE KEY  `obj_port` (`object_id`,`port_id`),
    KEY         `object_id` (`object_id`),
    KEY         `ttime` (`ttime`)
)

CREATE TABLE `InstantL12` (
    `ttime`     int(10) unsigned NOT NULL,
    `mac`       binary(6) NOT NULL,
    `port_id`   int(10) unsigned NOT NULL,
    PRIMARY KEY (`mac`)
)

CREATE TABLE `L1` (
    `ttime`         int(11) NOT NULL,
    `object_id`     int(11) NOT NULL,
    `port_id`       int(11) NOT NULL,
    `status`        enum('up','down','disabled') NOT NULL,
    KEY             `object_id` (`object_id`),
    KEY             `port_id` (`port_id`)
) PARTITION BY LIST (ttime)
(PARTITION p1612311460 VALUES IN (1612311460));

CREATE TABLE `L12` (
    `ttime`     int(11) NOT NULL,
    `mac`       binary(6) NOT NULL,
    `port_id`   int(11) NOT NULL,
    KEY `port`  (`port_id`),
    KEY `mac`   (`mac`)
) PARTITION BY LIST (ttime)
(PARTITION p1612311460 VALUES IN (1612311460));

CREATE TABLE `L23` (
    `ttime` int(11) NOT NULL,
    `mac`   binary(6) NOT NULL,
    `ip`    varbinary(16) NOT NULL,
    KEY     `mac` (`mac`),
    KEY     `ip` (`ip`)
) PARTITION BY LIST (ttime)
(PARTITION p1612311460 VALUES IN (1612311460));

CREATE TABLE `PortsIndexNameMap` (
    `ttime`     int(11) NOT NULL,
    `object_id` int(11) NOT NULL,
    `port_idx`  int(11) NOT NULL,
    `port_name` varchar(45) NOT NULL,
    UNIQUE KEY  `port` (`object_id`,`port_idx`),
    KEY         `object_id` (`object_id`)
)
```

### Расположение
- `/netmap` - директория с файлами
- `/netmap/src -> /usr/share/rt-yandex/netmap` - ссылка на код в расположении RT

### Данные

Данные проще всего стянуть `/netmap/src/DO_netmap_slave.sh`
```shell
cd /netmap && sudo -H -u racktables src/DO_netmap_slave.sh
```
Если что-то не получилось и надо повторить - `sudo rm /netmap/ttime` и заново ^
