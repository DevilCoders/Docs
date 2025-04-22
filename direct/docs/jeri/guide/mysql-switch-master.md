# Переключение БД MySQL

{% note alert %}

Все действия выполняются из под пользователем **root**.  
Невнимательное переключение баз может привести к поломке всего сервиса! 

Не выполняй никаких действий не прочитав инструкцию до конца.
Если видишь эту инструкцию в первый раз - попроси помочь/понаблюдать кого-нибудь уже выполнявшего переключение.

{% endnote %}

## Переключение ppcdata/ppcmonitor/ppcdict { #switch-non-clustered-db }

### Подготовка { #preparation-for-non-clustered-db }

Здесь и далее в примерах вместо `{instance}` следует указать нужный инстанс, например `ppcdata22`.
Часть инстансов переехала в MDB и не нуждаются в переключении dt-mymgr. Узнать какие это машины, можно посмотрев dbconfig:
сервера MDB имеют суффикс "db.yandex.net".

Заходим на ppcback сервер и смотрим, где сейчас мастер по мнению zkguard, dbconfig и какой статус преключения:  
```sh
dt-mymgr {instance} show;
```
Он должен показать диагностику и завершиться без ошибок.

### Разные варианты переключения { #ways-to-switch-non-clustered-db }

#### Автовыбор хоста { #auto-switch-non-clustered-db }
Переключение на новый мастер, где автоматически выбирается наиболее подходящий хост.  
Сначала запускаем в dry-run режиме:
```sh
dt-mymgr {instance} switchover --new-master auto;
```
(на этом этапе делаются пречеки, но не выбирается новый мастер, не надо искать его в листинге)

Если все нормально, то выполняем переключение (новый мастер будет выбран на этом шаге):
```sh
dt-mymgr {instance} switchover --new-master auto --apply
```

#### Ручной выбор хоста { #manual-switch-non-clustered-db }
Переключение на новый мастер, где хост выбирается администратором.  
Сначала запускаем в dry-run режиме:
```sh
dt-mymgr {instance} switchover --new-master $fqdn;
```
Если все нормально, то выполняем переключение:
```sh
dt-mymgr {instance} switchover --new-master $fqdn --apply
```

#### С исключением реплики { #exclude-replica-from-non-clustered-db }
Переключение с исключением реплики.  
Сначала запускаем в dry-run режиме:
```sh
dt-mymgr {instance} switchover --new-master auto --exclude $repl1 --exclude $repl2
```
Если все нормально, то выполняем преключение:
```sh
dt-mymgr {instance} switchover --new-master auto --exclude $repl1 --exclude $repl2 --apply
```

### Проверка { #check-switched-non-clustered-db }

1. Смотрим, что direct-db-config обновился и база доступна.  
   Например:
   ```sh
   direct-db-config | grep {instance}; direct-sql pr:ppc:1 "select @@hostname"
   ```
1. Смотрим, что на новый мастер пошла нагрузка и интерфейс работает.  
   Для этого надо зайти на сервер с базой и выполнить следующие команды:
   ```sh
   lm {instance} status; lm {instance} innotop
   ```
   На работающем мастере будет видна нагрука (много Sleep, Query, Execute):
   ```text
   ppcdata1-01i/ppcdata1, 2020-09-30 17:34:52, sql_log_bin=ON, server_id=62268, uuid=b6f6b628-188b-0c87-8d36-1b60a97f1bd5: Binlog Dump:2, Binlog Dump GTID:10, Execute:15, Query:7, Sleep:3291
   ```

