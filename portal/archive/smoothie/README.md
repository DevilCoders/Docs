morda's magic oriented open-source tool huddling important events

### documentation

https://wiki.yandex-team.ru/Morda/push-notify/Dokumentacija-pro-proektu/

### run

```sudo -u www-data plackup -r --port 5000 smoothie.psgi```

or look at upstart_porta-morda-smoothie.conf

### logs

/var/log/www/portal-morda-smoothie

### special dependencies not reported in debian/control

libdbd-mysql-perl                       4.020-1build2

### other soft

percona-xtradb-cluster-57                5.7.12-26.16-1.rc1.trusty

haproxy                                  1.6.7-2

### useful docs



### mysql cookbook

```SET foreign_key_checks = 0;``` - отключить чеки FK

```mmysqldump -d -usmoothie -p smoothie --single-transaction > db/db_schema.sql``` dump scheme only

```mysqldump -c -Q --extended-insert=0 -usmoothie -p smoothie --single-transaction --no-create-info --add-locks=0 > db/db_data.sql``` dump data

Посмотреть все текущие настройки каналов (таймлайны, гео, таргеты...)

```SELECT s.id, s.name, s.ttl, s.ttv, s.ttp, s.enabled, s.push_enabled, s.push_approved, sg.value as geo, st.time_from, st.time_to, stg.value, stg.enabled FROM settings AS s LEFT JOIN settings_geos AS sg ON s.id=sg.settings_id LEFT JOIN settings_timelines AS st ON s.id = st.settings_id LEFT JOIN settings_targetings AS stg ON s.id=stg.settings_id ORDER BY s.id\G```

### Notes
'DBI.pm' => '1.63 from /usr/lib/perl5/DBI.pm'

### geobase

./scripts/get_geobase

### view

Плагин для админки https://github.com/micc83/editTable

client markdown https://github.com/markdown-it/markdown-it

### test

prove -lsv --merge

### docker

build base image 

```docker build --network=host -f docker/Dockerfile_baseimage -t registry.yandex.net/portal/smoothie:base .```

build prod image 

```docker build --network=host -f docker/Dockerfile_prodimage -t registry.yandex.net/portal/smoothie:prod .```

 
deploy

```docker push registry.yandex.net/portal/smoothie```

platform

https://platform-int.yandex-team.ru/projects/junk/smoothie-wwax/dev - здесь нужно использовать prod

### git-pre-commit-hook

```ln -s /home/wwax/smoothie/tools/git-pre-commit-hook /home/wwax/smoothie/.git/hooks/pre-commit``` etc
