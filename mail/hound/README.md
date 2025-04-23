# HOUND[2]
Сервис над почтовой метабазой для выдачи списков папок, меток, табов и списков писем с разными условиями.

<details><summary><b>Выдача хаунда в веб-интерфейсе почты:</b></summary><p>
<img src='https://jing.yandex-team.ru/files/ezagurskih/Selection_001292.png' width=800/>
</p></details>

## HTTP API
* [v1] (https://wiki.yandex-team.ru/users/jkennedy/ywmiapi/) <br/>
  http как транспорт - ошибки в теле ответа, нет 5xx - недостаточно смотреть на 5xx на графиках
* [v2] (https://a.yandex-team.ru/arc/trunk/arcadia/mail/hound/doc/api/v2/README.md) <br/>
  честные пятисотки, асинхронизируемость

Итого 50 ручек. Только 3 из них модифицирующие: reset_fresh_counter, reset_unvisited, v2/reset_tab_unvisited.

### Пример суточной нагрузки на один инстанс (18.07.2019)
<details><summary><b>sas:</b></summary><p>
<pre>
      1 /v2/changes
      1 /v2/tabs
      4 /v2/threads_by_tab
      6 /threads_by_folder_and_tab
      6 /v2/messages_by_tab
     13 /messages_by_folder_and_tab
     14 /folder_tabs_new_counters
     74 /messages_with_attaches
    353 /messages_by_label
    493 /threads_info
    804 /messages_unread_useful
   1297 /messages_unread
   1309 /in_reply_to
   1495 /counters/
   1634 /messages_unread_by_folder
   2698 /v2/folders_tree
  16007 /threads_in_folder_with_pins
  23270 /messages_in_folder_with_pins
  31338 /reset_unvisited
  44514 /ping
  45173 /messages_by_folder
  47091 /first_envelope_date
  62449 /nearest_messages
  64962 /threads_by_folder
 112069 /mailbox_revision
 131037 /attach_sid
 136161 /mimes
 136764 /reset_fresh_counter
 267535 /yamail_status
 336417 /messages_by_thread
 346064 /folders
 392663 /folders_counters
 551063 /counters
 843846 /labels
2433522 /filter_search

6032158 all

 943844 msearch
</pre>
</p></details>


<details><summary><b>myt:</b></summary><p>
<pre>
      1 /v2/threads_by_tab
      4 /v2/messages_by_tab
      9 /threads_by_folder_and_tab
     13 /messages_by_folder_and_tab
     22 /folder_tabs_new_counters
     45 /messages_with_attaches
    304 /messages_by_label
    532 /threads_info
    842 /messages_unread_useful
   1243 /in_reply_to
   1561 /messages_unread
   1727 /messages_unread_by_folder
   1852 /counters/
   2919 /v2/folders_tree
  17897 /threads_in_folder_with_pins
  25942 /messages_in_folder_with_pins
  35110 /reset_unvisited
  44488 /ping
  48688 /messages_by_folder
  53668 /first_envelope_date
  63380 /nearest_messages
  71193 /threads_by_folder
  73534 /mimes
 121650 /mailbox_revision
 136334 /attach_sid
 146349 /reset_fresh_counter
 288723 /yamail_status
 350976 /folders_counters
 374697 /folders
 389361 /messages_by_thread
 607849 /counters
 936520 /labels
1641819 /filter_search

5439266 all

 226610 msearch
</pre>
</p></details>

## Общая архитектура
* qloud: https://platform.yandex-team.ru/projects/mail/hound
* conductor:
    * prod: https://c.yandex-team.ru/groups/mail_hound_production
    * corp: https://c.yandex-team.ru/groups/mail_hound_intranet-production
<img src='https://jing.yandex-team.ru/files/ezagurskih/hound_qloud.png' width=800/>

## Logs
* nginx: /var/log/nginx/application/access.tskv
* hound:
    * /app/log/access.log (будет tskv)
    * /app/log/application.tskv
    * /app/log/http_client.tskv
    * /app/log/yplatform.log
    * /app/log/profiler.log
    * /app/log/user_journal.tskv (льётся в YT)

## Dashboards
* [gr-mg prod](https://gr-mg.yandex-team.ru/dashboard/#mail_hound)
* [gr-mg crop](https://gr-mg.yandex-team.ru/dashboard/#mail_hound_corp)
* [yasm prod](https://yasm.yandex-team.ru/template/panel/hound_panel/env=production/)
* [yasm corp](https://yasm.yandex-team.ru/template/panel/hound_panel/env=intranet-production/)

## Troubleshooting

### DB
#### Симптом
504 и 499

#### Диагностика
Посмотреть на светофоры баз и топ ошибок по шардам:
```(bash)
executer -c 'p_exec %mail_hound_production_hound@sas timetail -n 300 -t tskv /app/log/application.tskv | grep -oP "connection_info=host=[^\s]+" | cut -d'=' -f3 | sort | uniq -c | sort -n' > sas.log
head -n -3 sas.log | cut -d ":" -f2 | awk '{xdb[$2]+=$1} END { for (db in xdb) print xdb[db], db }' | sort -n | tail -n10
```
Посмотреть на выдачу ручки `/stat` у шарпея:
```(bash)
curl 'sharpei-production.mail.yandex.net/v3/stat' | jq '.[].databases[] | select(.status != "alive" or .state.lag > 1) | {"role" : .role, "host": .address.host, "lag" : .state.lag, "status": .status}'
```
Если не видно проблемы, специфичной для каких-то шардов, посмотреть на топ ошибок по запросам:
```(bash)
executer 'p_exec %mail_hound_production_hound@vla timetail -n 300 -t tskv /app/log/application.tskv | grep "connection_info=host" | sed -r "s/.*sql: ([[:alpha:]]*), .*/\1/g" | sort | uniq -c | sort -n' > vla.log
head -n -3 vla.log | cut -d ":" -f2 | awk '{xdb[$2]+=$1} END { for (db in xdb) print xdb[db], db }' | sort -n | tail -n10
```

#### Решение
Призывать DBA

### DNS
#### Симптом
Фон 504 в одном ДЦ:
<img src='https://yasm.yandex-team.ru/img/c4aac47c914227fcc96d83224cf28a93.png' width=800/><br/>
[yasm](https://yasm.yandex-team.ru/template/panel/hound_panel/env=production/2/?from=1563285641612&to=1563287141612)<br/>
#### Диагностика
Разложить сигнал 504 по засветившемуся ДЦ в топ по хостам. Найти контейнер по хосту:
```(bash)
p_exec %mail_hound_production_hound env | grep PORTO_HOST=hostname
```
Проверить, что в контейнере таймаутится резолвинг:
```(bash)
# cat /etc/resolv.conf
search search.yandex.net yandex.ru
nameserver fd53::1
nameserver 2a02:6b8::1:1
# fgrep "sharpei" /app/config/config.yml
                sharpei:
                    host: http://sharpei-production.mail.yandex.net
# dig @fd53::1 sharpei-production.mail.yandex.net
; <<>> DiG 9.9.5-3ubuntu0.18-Ubuntu <<>> @fd53::1 sharpei-production.mail.yandex.net
; (1 server found)
;; global options: +cmd
;; connection timed out; no servers could be reached
```
#### Решение
Закрыть контейнер от нагрузки:
```(bash)
supervisorctl stop nginx
```
Отписаться в qloud-support


### Поиск по почте льёт нагрузку сверх rate limit'а
#### Симптом
Пики/горбики/бугры 503 в vla и/или sas:
<img src='https://yasm.yandex-team.ru/img/0ac520dbce3c76f4f02dceea9f395d17.png' width=800/><br/>
[yasm](https://yasm.yandex-team.ru/template/panel/hound_panel/env=production/2/?from=1563438777591&to=1563440277591)

При отсутствии других симптомов реакция не требуется

