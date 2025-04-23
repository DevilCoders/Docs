# loggiver2yasmagent

Инструмент для использования в связке с loggiver в качестве unistat ручки.

Для своей работы требует файл `/etc/yandex/loggiver/loggiver.commands` вида:
```
metric_group_name\tbash command string
```

В качестве `bash command string` может использоваться любая строка, которая передается в `/bin/bash -c`, так что работают пайпы.

## Как конвертировать

Допустим, у нас есть loggiver.pattern со следующим содержимым:
```
nginx=fgrep -v -e /ping -e /exec_pattern -e /timetail | tskv --status -t req,up -z
pg=/usr/bin/java-pg-stat.py
```

И конфиг комбайна:

```
---
parsing:
  groups: [test_group]
  metahost: test_group
  DataFetcher:
    logname: "nginx/access-tskv.log"
    timetail_url: "/timetail?pattern=nginx&type=tskv&log_ts="
aggregate:
  data:
    nginx_stat:
...
---
parsing:
  groups: [test_group]
  metahost: test_group
  DataFetcher:
    type: http
    port: 3132
    uri: "/exec_pattern?pattern=pg"
aggregate:
  data:
    pg_stat:
...
```

Тогда loggiver.commands будут следущими (внимание на `<TAB>` после названия группы):

```
nginx_stat  timetail -t tskv -n 5 /var/log/nginx/access-tskv.log | fgrep -v -e /ping -e /exec_pattern -e /timetail | tskv --status -t req,up -z
pg_stat /usr/bin/java-pg-stat.py
```

В `agent.<itype>.conf` в таком случае надо добавить
```ini
[sources]
loggiver = unistat

[options_loggiver]
url = /exec_pattern?pattern=unistat&timeout=7
port = 3132
timeout = 7
max_sig_count = 3000
```

