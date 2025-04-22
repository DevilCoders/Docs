# Ротация логов приложения

##  О чём? {#whatsit}
Рассмотрим способы ротации логов и стандартных потоков вывода (stderr, stdout) в RTC.

##  Ротация логов в файловой системе железной машины {#log-rotation-without-rootfs}
При запуске в файловой системе железной машины, то есть без `chroot`, единственное место, куда правильно писать логи, это путь `/place/db/www/logs/` (или `/db/www/logs/` или `/usr/local/www/logs`, которые являются симлинкой для `/place/db/www/logs`). Данные, сохранённые по другим путям, могут быть очищены в произвольный момент времени. Исключением являются файлы, которое приложение создаёт в `/ssd`, однако писать логи по этому пути не рекомендуется, причина будет развёрнута ниже.
Также писать логи в `/place/db/www/logs/` можно, если запускать приложение с флагом, включающим bind `/place/db/www/logs/` с хостовой файловой системы в файловую систему контейнера (однако этот способ доступен только на переходный период, пока сервис полностью не заедет в изолированную FS).

###  Ротация логов с rotmissingdocs {#log-rotate-rotmissingdocs}
Для ротации логов можно использовать [rotmissingdocs](https://wiki.yandex-team.ru/users/sourcerer/rotmissingdocs/). Для этого достаточно писать логи в `/place/db/www/logs`, или в `/db/www/logs/`, или в `/usr/local/www/logs`, и ни в какие другие пути, т.е. `rotmissingdocs` не умеет ротировать логи на `/ssd`.

rotmissingdocs сам определяет момент, когда пора ротировать логи, используя хитрую эвристику с учётом свободного места на железной машине. Он будет переименовывать файл лога, затем происходит следующая цепочка событий:

* выполняется запрос в API iss-agent'а `http://localhost:25536/instances/reopenlogs`;
* тот в свою очередь в контейнере каждого инстанса запускает хук `iss_hook_reopenlog`;
* этот хук через unix socket обращается к уже запущенному процессу instancectl;
* instancectl для каждой секции запускает `reopenlog_script`, в котором владелец сервиса должен описать способ, которым нужно сигнализировать его приложению, чтобы оно переоткрыло логи;
* приложение должно закрыть и открыть файл лога;
* в противном случае оно будет завершено с помощью отправки ему `SIGKILL`.
Т.е. скрипт выполняется в том же контейнере (pid namespace) и может отправить сигнал нужному процессу, либо выполнить HTTP запрос в специализированный обработчик сервиса. Пример такого скрипта можно посмотреть [тут](https://wiki.yandex-team.ru/users/sourcerer/rotmissingdocs/).

###  Ротация без rotmissingdocs {#log-rotate-without-rotmissing-docs}
Можно ротировать логи самому, для этого их нужно писать не в `/place/db/www/logs`. Обычно пишут в `/db/www/logs/{my_service_name}-{port}/`, туда есть права на запись, туда не смотрит rotmissingdocs, и эта директория будет сохраняться между выкатками сервиса. Этот метод менее предпочтителен и делать это нужно аккуратно, не плодя слишком много логов, т.к. в этом случае можно забить логами всю железную машину, навредив соседям. Если логи необходимо писать на `/ssd`, то их тоже потребуется ротировать (т.е. выбирать момент для ротации и создавать новые файлы) самостоятельно.

##  Ротация логов в изолированной RootFS (docker, sandbox layers) {#custom-rootfs}
При запуске инстанса в собственной файловой системе (с помощью docker-образа или слоёв, собираемых в sandbox), файловая система хоста становится недоступна из контейнера инстанса. При этом перестаёт работать старая схема ротации логов с помощью `rotmissingdocs`, описанная выше. Чтобы настроить ротацию логов в таком изолированном сервисе, можно использовать один из двух вариантов:

1. Встроенный механизм ротации с использованием `logrotate`, повторяющий логику `rotmissingdocs`. [Подробнее](#like-rotmissingdocs).
1. Утилиту `logrotate`. [Подробнее](#logrotate).

###  Ротация логов в изолированной RootFS like rotmissingdocs {#like-rotmissingdocs}

* Ротация логов будет происходить так же, как она происходила в rotmissingdocs (только логов, но не stdout/stderr), подробности [см. выше](#log-rotate-rotmissingdocs);
* Совместима как со [структурированным конфигом instancectl](structured-instancectl-config.md), так и с instancectl.conf/loop.conf;
* Доступна только при наличии изоляции по файловой системе. [Перевод сервиса на отдельный mount namespace](storage/move-to-rootfs.md);
* Доступна и под YP-lite, и под gencfg
* Доступна только при использовании persistent volumes, обязательно наличие volume с точкой монтирования `/logs`. Как его создать под gencfg: [Перевод сервиса на выделенный storage](storage/move-to-volumes.md);
* Данный способ ротации логов совместим только с достаточно свежей версией базового образа, в которой должны существовать:
    * Симлинк `/db -> /place/db`;
    * Симлинк `/usr/local/www -> /place/db/www`;
    * Права на запись от loadbase в директорию `/place/db/www`.
* Перед стартом цикла с `logrotate` будет создана симлинка (при её отсуствии):
    * `/place/db/www/logs -> /logs`
* logrotate-агент запускается в подконтейнере со следующими лимитами:
    * `cpu_limit: 0.1c # 0.1 cores`
    * `memory_limit: 256Mb`
* Будут ротироваться логи, удовлетворяющие одному из шаблонов:
    * `/logs/current-*`
    * `/db/www/logs/current-*`
    * `/place/db/www/logs/current-*`
    * `/usr/local/www/logs/current-*`


* Ротация логов будет запущена, если суммарное место, занимаемое несротированными логами будет превосходить 30% от объёма volume'а `/logs`
* **Замечание: формат ротированного лога отличается от использованного в rotmissingdocs.** Детали доступны в тикете [RTCSUPPORT-510](https://st.yandex-team.ru/RTCSUPPORT-510). 

Пример:

```
# ls -1 /logs/*
/logs/current-application <- текущий лог
/logs/current-application.1 <- отротированный
```
Раньше было так:

```
# ls -1 /logs/*
/logs/current-application <- текущий лог
/logs/application.PREV <- отротированный
```

* Для ротации используется статически собранный бинарь `logrotate v3.13.0`, который приезжает в качестве ресурса сервиса. [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/logrotate).

Используемый конфигурационный файл logrotate:

```
# CURRENT_LOG_PATTERN – паттерн логов для log rotate (например /logs/current-* )
# CURRENT_LOG_SIZE_MAX – суммарный объем логов, при котором надо ротировать в байтах
CURRENT_LOG_PATTERN
{
    create
    rotate 1
    firstaction
        P='CURRENT_LOG_PATTERN'
        USED_BY_LOGS="$(du -bc ${P} --exclude ${P}.1 2>/dev/null | awk '$2 == "total" {print $1}' | tail -1)"
        if [ ${USED_BY_LOGS} -lt CURRENT_LOG_SIZE_MAX ]; then
            msg="Exit. (Used by logs: ${USED_BY_LOGS} B (< CURRENT_LOG_SIZE_MAX B)"
            echo "[`date +"%Y-%m-%d %H:%M:%S"`] INFO ${msg}"
            exit 1
        fi
        msg="Rotating logs (Used by logs: ${USED_BY_LOGS} B (threshold: CURRENT_LOG_SIZE_MAX B)"
        echo "[`date +"%Y-%m-%d %H:%M:%S"`] INFO ${msg}"
    endscript
    prerotate
         /bin/bash -c '[[ ${0} != *.1 ]]' ${1}
    endscript
    lastaction
        FILE_LIST=${1}
        msg="Sending reopenlog signals"
        echo "[`date +"%Y-%m-%d %H:%M:%S"`] INFO ${msg}"
        ./instancectl reopenlog

        msg="Looking for processes still writing to moved files"
        echo "[`date +"%Y-%m-%d %H:%M:%S"`] INFO ${msg}"
        for file in ${FILE_LIST}; do
            _file="${file}.1"
            _mode="[a-z]"
            [ -n "${_file}" -a -f "${_file}" ] || continue
            pids=`lsof "${_file}" | awk '!/PID/ && $4 ~ /'${_mode}'/ {print $2}' | sort -rn`
            [ -n "${pids}" ] || continue

            msg="Kill procs for '${file}' (-KILL ${pids})"
            echo "[`date +"%Y-%m-%d %H:%M:%S"`] WARN ${msg}"
            kill -KILL ${pids} >/dev/null 2>&1
        done
    endscript
}
```

Для включения logrotate-демона нужно:

1. Включить соответствующую опцию в UI:

    ![img](https://jing.yandex-team.ru/files/sshipkov/logrotatedaemon.83f6a6f.png)

1. Обновить базовый слой сервиса как минимум до текущего актуального: [https://rtc.yandex-team.ru/docs/containers/virtual-images](https://rtc.yandex-team.ru/docs/containers/virtual-images)

    ![img](https://jing.yandex-team.ru/files/sshipkov/2017-12-2215-06-03.1bcdf1a.png)

1. Если в сервисе используется instancectl.conf/loop.conf, то описать в нём [reopenlog_script](https://wiki.yandex-team.ru/jandekspoisk/sepe/instancectl/#reopenlogscript).
1. Если в сервисе используется структурированный instancectl, то описать в нём `ReopenLog Action`:

    ![img](https://jing.yandex-team.ru/files/sshipkov/reopenlogaction.2307c83.png)

###  Ротация логов в изолированной RootFS с помощью logrotate {#logrotate}

В этом случае логи можно писать куда угодно, и как угодно, главное правильно написать конфиг для их ротации и запустить `logrotate`. Достаточно:

1. Добавить в конфиг instancectl секцию с запуском `logrotate`;
    Пример секции:
    ```
    [logrotate]
    
    binary = /bin/bash
    arguments = -c 'while true; do sleep 3600 && logrotate -s /logs/logrotate.state logrotate.conf; done'
    ```
2. Добавить конфиг `logrotate.conf`.

    Пример конфига
    
    ```
    /logs/mongo.log {
        daily
        rotate 10
        size 50M
        dateext
        missingok
        notifempty
        sharedscripts
        postrotate
            killall -SIGUSR1 mongod
        endscript
    }
    ```

3. В некоторых версиях logrotate требует, чтобы пользователь, из-под которого он запущен, совпадал с владельцем директории логов. Например, при запуске с DOCKER_LAYERS, где процессы запускаются из-под root, logrotate может отказаться ротировать логи в персистентном вольюме `/logs`, владеет которым loadbase. Чтобы этого избежать, можно использовать один из двух вариантов:

    * Использовать logrotate из arcadia: [https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/logrotate](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/logrotate) где эта проверка выключена;
    * Запускать logrotate из-под того же пользователя, который владеет директорией.

###  Ротация stdout и stderr {#log-rotation-without-rootfs}
Стандартные потоки вывода (stderr, stdout) перенаправляются силами instancectl в файлы `<section>.err, <section>.out` в директории инстанса.

Начиная с версии `instancectl==1.126` ротацией этих файлов занимается instancectl. При этом:

1. Логи ротируются при превышении размера в 1 мегабайт;
1. Проверка необходимости ротации выполняется раз в 30 секунд.
    При этом instancectl подрезает начало этих файлов, не создавая их копии (используется системный вызов `fallocate`).

    {% note info %}

    Если пользовательский процесс запускается в отдельном подконтейнере (например, при кастомных настройках сборки coredumps в сервисе), ротация логов будет выполняться силами porto при достижении размера 8Mb. В общем случае нельзя полагаться на то, что размер файла с логами не будет превышать 1Mb.

    {% endnote %}

    Если необходимо держать на диске более чем 1 мегабайт данных из stdout/stderr, то можно использовать один из двух вариантов:

1. Писать важную информацию в логи, а не stdout/stderr;
1. Перенаправить stdout/stderr, условно сделав `1> /log/log.out 2>/logs/err.log`.

Пример instancectl.conf с перенаправлением стандартных потоков:

```
[test]
binary = /bin/bash
arguments = -c "./my_binary 1>log.out 2>log.err"
```


Для старых версий instancectl ротацией stdout и stderr вне зависимости от того, запущен ли инстанс в изолированной FS (то есть с `chroot`), или нет, занимается `rotmissingdocs`. При этом файлы `<section>.err, <section>.out` ротируются по принципу `copy && truncate` [исходный код)]((https://git.qe-infra.yandex-team.ru/projects/SEARCH_INFRA/repos/rotmissingdocs/browse/rotmissingdocs#292), при этом создаются копии файлов вида `<section>.err.PREV, <section>.out.PREV`. Пользовательские бинарники не должны уметь отпускать эти логи, за неотпущенный лог `<section>.err, <section>.out` из директории инстанса бинарнику не пошлют `SIGKILL`.

rotmissingdocs запускает ротацию stderr/stdout, ориентируясь на объём свободного места на хосте, т.е. независимо от того, упирается ли данный конкретный инстанс в квоту по диску, и это нельзя перенастроить, поэтому при включении в сервисе квотирования диска необходимо переехать на instancectl 1.126.

