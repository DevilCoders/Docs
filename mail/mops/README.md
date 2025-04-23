# MOPS
 Сервис **mops** отвечает за выполнение модифицирующих операций над пользовательскими метаданными.

## HTTP API
* Общие методы
  * **/ping** (GET) - pong (тест доступности сервиса)
  * **/stat** (GET) - статистика асинхронных операций конкретного юзера
* Методы операций над письмами (POST)
  * Перемещение
  * Удаление
  * Пометка прочитанным
  * Установка / снятие меток
  * Пометка спамом
  * И т.п.
* Методы редактирование папок (POST)
  * Создание
  * Изменение
  * Удаление
  * Изменение позиции
* Методы редактирование меток (POST)
  * Создание
  * Изменение
  * Удаление

см. [API mops](https://wiki.yandex-team.ru/pochta/backend/mops/http-interface/)

## Архитектура

### Состав
* **mops** - сам сервис
* **mopsdb** - база очереди асинхронных операций

### Где живет
#### mops
* qloud: https://platform.yandex-team.ru/projects/mail/mops

| Кондукторная группа           | суффикс        | число узлов |
| :---------------------------- | :------------- | ----------: |
| mail_mops_production          |                |      **26** |
|                               | _mops          |          25 |
|                               | _mops-canary   |           1 |
| mail_mops_intranet-production |                |       **9** |
|                               | _mops          |           8 |
|                               | _mops-canary   |           1 |

Сервисы живут в отдельных контейнерах. Кроме самого сервиса в контейнере располагаются другие вспомогательные сервисы: **nginx** (проксирует запросы извне, ограничивает rps), **supervisord** (следит за процессом сервиса, перезапускает сервисы), **unistat** (собирает статистику для yasm, отвечает на запрос */unistat*), различные **кроны** (logrotate и т.п.).

#### mopsdb
* yandex-cloud: https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql

Кластеры **mopsdb-***: 1 мастер, 2 реплики, VLA-SAS-MAN

### Цикл работы
#### Запрос
* Потребитель приходит в сервис с запросом.
* *mops* идет в blackbox и проверяет, что юзер не мейлиш.
* *mops* оценивает верхнюю границу количества писем для обработки.
  * Если значение меньще лимита синхронных операций (в данный момент 500), *mops* выполняет операцию сразу.
  * Если значение больше лимита синхронных операций, *mops* ставит операцию в очередь:
    * *mops* добавляет в очередь в *mopsdb* таск на выполнение или на определение mid'ов для обработки.
* Потребителю отдается ответ, который содержит тип выполнения операции (sync или async) и id асинхронной операции.

#### Выполнение асинхронных тасков
* В *mops* есть несколько тредов воркеров, которые пытаются считать свежие таски из *mopsdb*.
* Для найденного таска *mops* пытается взять лок на uid в *mopsdb*. Делается это для предотвращения конфликтов, когда несколько воркеров работают по одному пользователю.
  * Если это таск на определение mid'ов, то:
    * Через *sharpei* определяется шард пользователя.
    * Происходит собственно определение mid'ов.
    * Найденные mid'ы разбиваются на чанки.
    * В очередь в *mopsdb* добавляется новый таск (на выполнение самой операции) с чанками.
  * Если это таск на выполнение операции, то для каждого происходит выполнение операции для каждого чанка.

#### Выполнение операций
* Через *sharpei* определяется шард пользователя.
* Происходит собственно выполнение операций для набора mid'ов.
* *mops* записывает выполнение операции в user_journal.
* После асинхронной обработки чанка *mops* отправляет нотифайку в ксиву (push.yandex.ru).


## Клиенты
Сервис закрыт TVM. Клиенты (согласно конфигу):
* liza
* webapi
* mobile
* lite
* magic
* so
* ml
* xeno (?)

## Зависимости
Корректная работа *mops* зависит от:
* **maildb** - почтовые метабазы, при недоступности мастера работа сервиса невозможна.
* **sharpei** - недоступность сервиса шардирования = недоступность почтовых метабаз.
* **blackbox** - при недоступности не можем определить тип пользователя, работа невозможна.
* **mopsdb** - при недоступности не можем запланировать и выполнить асинхронные операции, начинает расти очередь.
* **puli** - отдельный микросервис для мониторинга и кронов вспомогательных баз, при отключении не происходит ротации таблиц с логами и удаления устаревших тасков, через несколько дней перестают выполняться асинхронные операции, начинает расти очередь (но этого не видно на графиках, так как графики идут с машинки с кронами).
* **push.yandex.ru** - недоступность не влияет на работу сервиса.

## Logs
В контейнере *mops* можно найти следующие логи
* **nginx**:
    * **access** (/var/log/nginx/application/access.tskv)
В yt: [production](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-production-nginx-access-log) [corp](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-corp-nginx-access-log)
* **mops**:
    * **yplatform** (/app/log/yplatform.log)
    * **http_client** (/app/log/http_client.tskv)
В yt: [production](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-production-httpclient-log) [corp](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-corp-httpclient-log)
    * **access** (/app/log/access.tskv)
В yt: [production](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-production-access-log) [corp](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-corp-access-log)
    * **mops** (/app/log/application.tskv.tskv)
В yt: [production](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-production-mops-log) [corp](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-corp-mops-log)
    * **task_master** (/app/log/task_master.tskv)
В yt: [production](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-production-taskmaster-log) [corp](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-corp-taskmaster-log)
    * **worker** (/app/log/worker.tskv)
В yt: [production](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-production-worker-log) [corp](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-mops-corp-worker-log)
    * **tvm_guard** (/app/log/tvm_guard.tskv)
    * **profiler** (/app/log/profiler.log)
* **прочие**:
    * user_journal (/app/log/user_journal.tskv)
    * unistat (/var/log/unistat/unistat.log)
    * supervisord (/var/log/supervisor/supervisord.log)

### Что в логах
* в *nginx* *access* регистрируются поступившие в proxy-сервис запросы и статусы их выполнения (или отклонения, если например превышен рейт).
* в *mops* *access* регистрируются запросы, которые прошли проверку nginx'ом (лимиты rps, наличие ticket'а).
* в *http_client* (*yplatform*) регистрируются http-обращения к внешним сервисам.
* в *mops* попадает более детальная информация о работе сервиса в контексте выполнения запроса.
* в *task_master* попадает информация о работе с очередью задач.
* в *worker* попадает информация о работе воркеров по асинхронной обработке чанков.
* в *tvm_guard* попадают результаты проверки TVM v2 тикетов и причины разрешения/отказа доступа.

## Dashboards
https://yasm.yandex-team.ru/template/panel/mops_panel

https://yasm.yandex-team.ru/template/panel/mops_by_request_panel

https://yasm.yandex-team.ru/template/panel/mopsdb_panel

Подробнее тут https://wiki.yandex-team.ru/pochta/backend/mops/graphs/

## Troubleshooting
### Рост ошибок 401 на графике nginx
#### Проблемы с TVM

Посмотреть ошибки можно в логах *mops*
```
executer "p_exec %mail_mops_production timetail -t tskv -n 600 /app/log/tvm_guard.tskv | fgrep 'action=reject'" 2>/dev/null
```

Частых известных проблем нет - нужно призывать ответственного за сервис.

### Рост ошибок 500, 504, 499 на графике nginx
#### Проблемы с базами

<img src='https://yasm.yandex-team.ru/img/a906aacefea8f4d6194ddd7d7b1a6071.png' width=800><br/>

Посмотреть топ ошибок на шардах можно в логах *mops*
```
executer "p_exec %mail_mops_production timetail -t tskv -n 600 /app/log/application.tskv.tskv | fgrep -e 'db.yandex.net' -e 'xdb'" 2>/dev/null | grep -oP '(?<=host=)[^\s]+' | sort | uniq -c | sort -nr | head
```
Написать дежурным по базам.

#### Проблемы с dns

Фон ошибок будет в одном ДЦ:
<img src='https://yasm.yandex-team.ru/img/c4aac47c914227fcc96d83224cf28a93.png' width=800/><br/>

Разложить сигнал по засветившемуся ДЦ в топ по хостам. Найти контейнер по хосту:
```(bash)
executer "p_exec %mail_mops_production env | grep PORTO_HOST=hostname"
```
Проверить, что в контейнере таймаутится резолвинг:
```(bash)
# cat /etc/resolv.conf
search search.yandex.net yandex.ru
nameserver fd53::1
nameserver 2a02:6b8::1:1
# fgrep "sharpei" /etc/hound2/hound2.yml
                sharpei:
                    host: http://sharpei-production.mail.yandex.net
# dig @fd53::1 sharpei-production.mail.yandex.net
; <<>> DiG 9.9.5-3ubuntu0.18-Ubuntu <<>> @fd53::1 sharpei-production.mail.yandex.net
; (1 server found)
;; global options: +cmd
;; connection timed out; no servers could be reached
```

Закрыть контейнер от нагрузки (гасить нужно вместе с сервисом из-за воркеров):
```(bash)
supervisorctl stop nginx cron mops
```

#### Проблемы с blackbox или sharpei
Будет видно на соответствующих графиках на панели *mops_panel*.

Написать дежурным паспорта или шарпея.

### Проблемы с асинхронными операциями
#### Рост очереди
Перестали выполняться асинхронные операции.

Можно посмотреть на потребление ресурсов mopsdb - могли упереться в cpu, память или диск.

В текущих реалиях причину разобрать непросто - нужно призывать ответственного за сервис.

#### Пропал сигнал по размеру очереди
Потеряли кроны - нужно призывать ответственного за сервис.
