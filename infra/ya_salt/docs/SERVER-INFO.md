## Server info file
TL;DR:
  * located at `/etc/server_info.json`
  * contains basic information about host
  * maintained by hostmanager

## Format
This is JSON file with following fields (that are required to be present):
  * `walle_dc`
  * `walle_location`
  * `location` - alias for `walle_location`
  * `walle_project`
  * `walle_tags`
  * `lldp` - port and switch information
  * `cpu_model` - CPU model information (e.g. `Intel(R) Xeon(R) CPU E5-2660 0 @ 2.20GHz`)
  * `cpuarch` - CPU architecture (e.g. `x86_64`)

Frowned upon fields (i.e should not be used):
  * `points_info` - currently used by YASM agent

## Usage
Предполагается следующие варианты использования:
  * Human readable - для чтения людьми, администраторами.
  * Informational - использовать в сервисах для формирования сигналов в мониторингах, отправки во внешние сервера.
  * Logic switch - для изменения поведения сервисов на хосте.

### Logic switch
Нужно быть предельно аккуратным при использовании `server_info.json` для изменения логики своего сервиса в его коде, а не через настройки системы выкладки. Нужно использовать **правило**:
>Можно "вышивать" в коде по личным атрибутам хоста, т.е. те, которые можно получить не ходя никуда в сеть. Набор пакетов, версия ОС, набор железа, разбивка диска и т.д.
По всему остальному вышиваем в hostman/salt.

>При этом, как у любого другого простого правила есть **понятный минус**: оно не универсально применимо. Но в качестве первого приближения в условиях недостатка времени и информации - вполне работает.

## Historical note
Historically this file was managed by salt (i.e. using Jinja) and contains a lot of undocumented information,
some of it is still present and will be gradually removed.
