# Ad-hoc действия с ZooKeeper

[Перейти к практике](#data-manipulation)

## Теория { #theory }

Больше теории и ссылок -- на [странице](../things/zookeeper.md).

Продакшеновый ZK в Директе живет на трех хостах ppcback\*.
Через этот ZK распространяется db-config, реестр приложений, реестр реплик mysql и т.п.

ZK для непродакшеновых целей живет на хостах `ppctest-zookeeper01i.sas.yp-c.yandex.net`, `ppctest-zookeeper01f.myt.yp-c.yandex.net`, `ppctest-zookeeper01v.vla.yp-c.yandex.net`.
В этом ZK живут стейты `direct-release`.

## Как "потыкать" ZooKeeper { #ad-hoc-operations }

### Скрипт direct-zkcli { #direct-zkcli }

Родные консольные инструменты для просмотра/редактирования данных в ZK неудобные, поэтому примерно каждая команда, у которой есть ZK, пишет свой cli-клиентик.

Директовый скрипт — `direct-zkcli`.
Эксплуатируем файловую метафору: `ls`, `cat`, `vim`, `rm` и т.д.

Если процесс ZK живет на той же машине, где запускается `direct-zkcli`, то можно не указывать опцию `-H`.

```
root@ppcback01f:~# direct-zkcli ls / |head -n 3
/directadmin
/clickphite
/tabula
```

### Где тренироваться { #playground }

В непродакшеновом ZK внутри ноды `/playground` можно свободно создавать и удалять ноды.

```
direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net ls /playground
```

### Что делать и чего не делать { #do-donts }

Читающие операции (`ls`, `cat`) делать безопасно. 

Пишущие операции (`touch`, `vim`, `tee`, `rm`) — опасны. 
Нужны в двух случаях:

1. Штатная инструкция явно требует ручного редактирования ZK.
Примеры: инициализация нового приложения, запуск новых perl-scripts машин. 
2. Происходит что-то сильно нештатное, ты досконально понимаешь устройство сломанной подсистемы и ничего кроме ручного исправления данных в ZK не поможет. 

## Операции с данными { #data-manipulation }

### Список нод / ls { #ls }

Один уровень вложенности:

```
direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net ls /direct/release-state
/direct/release-state/testing
/direct/release-state/stable
/direct/release-state/waiting
```

Рекурсивный список всех вложенных нод (`-R`):

```
direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net ls -R /direct/release-state/stable
/direct/release-state/stable/direct
/direct/release-state/stable/oneshot
/direct/release-state/stable/test
/direct/release-state/stable/java-recom-tracer
/direct/release-state/stable/ess-router
/direct/release-state/stable/canvas
/direct/release-state/stable/java-logviewer
/direct/release-state/stable/steps
/direct/release-state/stable/java-api5
/direct/release-state/stable/java-jobs
/direct/release-state/stable/java-web
/direct/release-state/stable/lb-moderation
/direct/release-state/stable/db-schema
/direct/release-state/stable/lb-alw
/direct/release-state/stable/java-b2yt
/direct/release-state/stable/java-intapi
/direct/release-state/stable/java-alw
/direct/release-state/stable/binlogbroker
/direct/release-state/stable/b2clh
/direct/release-state/stable/mysql2yt-full
```

### Посмотреть контент ноды / cat { #cat }

```
direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net cat /direct/release-state/stable/direct
{
    "_format_": 1,
    "build_type": "branch",
    "current_build": {
        "branch": "svn+ssh://arcadia.yandex.ru/arc/branches/direct/release/perl/release-7341741",
        "done": {
            "dmove": 1,
            "hotfix-merge": 1,
            "hotfix-plan": 1,
            "packages": 1,
...
}
```

### Создать пустую ноду / touch { #touch }

```
ppcdev$ direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net touch /playground/lena-san-20200922
ppcdev$ direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net ls /playground |grep lena-san-20200922
/playground/lena-san-20200922
```

### Неинтерактивно записать контент в ноду / tee { #tee }

```
ppcdev$ echo 'some text' | direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net tee /playground/lena-san-20200922
ppcdev$ direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net cat /playground/lena-san-20200922
some text
```

### Интерактивно поредактировать контент ноды / vim { #vim }

```
direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net vim /playground/lena-san-20200922
```

Откроет редактор (vim). Редактируем содержимое, сохраняем, выходим. `direct-zkcli` покажет дифф, с ним можно согласиться или отменить правки.

### Удалить ноду / rm { #rm }

```
direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net rm /playground/lena-san-20200922
```

## Диагностика состояния ZK

TODO. Может быть, отселить в отдельную страницу


## Ссылки { #links }

- [Самое главное, что надо знать о ZooKeper](../things/zookeeper.md), также там больше ссылок
- [Справочник: важные данные в Директовых ZooKeeper](../reference/zk-data.md)

