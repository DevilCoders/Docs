# ЦК

## Типовые задачи

### Права на запуск сценария

Если у пользователя ЦК нет прав на запуск какого-либо сценария, то:

- он не увидит этого сценария в веб-интерфейсе в форме создания джобы в поле Job type
- он будет получать ошибки "You have no role allowing this operation (or not authenticated)" в cli даже если он
  аутентифицировался

Чтобы права появились, нужно:

- выбрать существующую роль или создать новую в [админке ЦК](https://noc.yandex-team.ru/admin)
- добавить сценарий в эту роль
- добавить пользователя в эту роль

### Доступ в админку ЦК

Для получения доступа в [админку ЦК](https://noc.yandex-team.ru/admin) нужно в IDM запросить роль
[Автоматизация сети -> Superuser](https://idm.yandex-team.ru/system/netauto/roles#rf=1,rf-role=aAenaibI#netauto/superuser,f-role=netauto,rf-expanded=aAenaibI)

### Расширение набора устройств, доступных в веб-интерфейсе

В ЦК есть [страница с устройствами](https://noc.yandex-team.ru/devices), на которой перечислено несколько тысяч
устройств. Запуск джобов в ЦК начинается именно с выбора устройств из этого набора. Иногда случается, что пользователи
ЦК не обнаруживают в этом списке нужных им устройств, и в этом случае может иметь смысл расширить этот набор. Это
расширение делается путём изменения конфига Чекиста (за девайсами ЦК ходит в Чекиста). Для этого нужно:

1.  Посмотреть текущий рэккод в опции `rt_filter`
    [в json-конфиге Чекиста](https://a.yandex-team.ru/arc_vcs/admins/salt-media/noc/roots/units/nocdev-4k/files/etc/checkist/config.json)
2.  Убедиться, что интересующее нас отсутствующее устройство действительно не входит в этот рэккод
3.  Поправить рэккод, сделав Pull Request
4.  Получить одобрение команды netauto
5.  Замержить, выкатить конфиги через salt и перезапустить Чекиста
Обязательно нужно согласовать изменение с командой netauto, потому что изменение набора девайсов повлечён за собой
изменение статистики, которую собирает Чекист, и повлияет на
[дашборды Чекиста](https://datalens.yandex-team.ru/myq3sqesiexog-total-cfg-diff-counts), по которым отслеживается
прогресс снуления диффов

Для [тестинга ЦК](noc-test.yandex-team.ru/) нужно менять тот же
[шаблон конфига Чекиста](https://a.yandex-team.ru/arc_vcs/admins/salt-media/noc/roots/units/nocdev-4k/files/etc/checkist/config.json),
но перезапустить нужно не только прод, но также и тестинг Чекиста

### Добавление пользователя robot-noc-ck на устройство

Может случиться так, что пользователь [robot-noc-ck@](https://staff.yandex-team.ru/robot-noc-ck) отсутствует на
каком-либо устройстве. Добавить пользователя можно:

- в наливке
- в localuser-db
- в обоих этих местах сразу

Для добавления робота robot-noc-ck в localuser-db нужно поправить предикат `[работает ЦК]` в
[Racktables Permissions](https://racktables.yandex-team.ru/index.php?page=perms). По этому предикату и по роли
[в lusettings.php](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/1b28385c5b12483af67f86b6d89d4f9db91505ea/scripts/localuser-db/lusettings.php#L111)
обеспечивается раскатка юзера-робота на устройства

Добавление робота robot-noc-ck в наливку сделано в
[генераторе LocalUsers Аннушки](https://noc-gitlab.yandex-team.ru/nocdev/annushka/-/blob/354bbbb38290c42bec98532d2bda3e0bb49442c6/annushka/generators/local_users.py),
который деплоится как раз при наливке устройства

Для тестинга ЦК используется другой робот [robot-noc-ck-testing](https://staff.yandex-team.ru/robot-noc-ck-testing),
который выкатывается по рэккоду, описанному прямо в
[lusettings.php](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/1b28385c5b12483af67f86b6d89d4f9db91505ea/scripts/localuser-db/lusettings.php#L112),
и расширять набор тестовых устройств нужно расширением этого рэккода. При этом важно учитывать, что тестинг-робот не
должен ходить никуда, кроме лабных устройств (см. [NOCDEV-5091](https://st.yandex-team.ru/NOCDEV-5091))

Тестовый робот robot-noc-ck-testing не добавляется на устройства при наливке

## Методические указания по поиску неисправностей

### Логи

#### Лог общения с устройством

Лог общения с устройством (команды и ответ от устройства через comocutor) находится в "контексте" джобы, который в свою
очередь лежит в базе. Достать этот лог можно через веб-интерфейс:

1. Переходим на [страницу с джобами](https://noc.yandex-team.ru/jobs?state=planned%2Cscheduled%2Crunning&page=1)
2. Выставляем фильтры; удобнее указать имя устройства и сбросить остальные фильтры. Например,
   [так](https://noc.yandex-team.ru/jobs?deviceName=publab-u4&page=1)
3. В списке найденных джобов находим нужную и нажимаем на неё, откроется страница джобы;
   например, страница джобы
   [cisco-sw-upgrade на publab-u4](https://noc.yandex-team.ru/jobs/611bd01a3c6f8dda64949b90)
4. На странице джобы во вкладке "Logs" будет нужный лог общения с устройством

#### Логи ЦК

ЦК запущен на хостах [%nocdev-ck](https://c.yandex-team.ru/groups/nocdev-ck/) и пишет логи в journald для
следующих systemd-сервисов:

- `noc-ck-worker.service` - воркер ЦК, исполняющий джобы и периодические задачи
- `noc-ck-api.service` - веб-сервер ЦК
- `noc-ck-profiler.service` - профайлер воркера ЦК

Соответственно, чтобы понять, как джоба исполнялась, нужно на всех хостах ЦК посмотреть логи воркера:

```bash
sudo journalctl -u noc-ck-worker.service --since "2022-04-05 09:12:00" --until "2022-04-05 09:17:00"
```

Параметры для since/until можно брать со страницы джобы, например, на странице джобы
[checkist на supwh-21u1](https://noc.yandex-team.ru/jobs/624bddb64382f14c0071d950?tab=logs) в правой
панели видим:

- Start time: 05 Apr, 09:17
- End time: 05 Apr, 09:25

Для удобства можно использовать [executer](https://wiki.yandex-team.ru/executer/):

```bash
executer 'p_exec %nocdev-ck sudo journalctl -u noc-ck-worker.service --since "2022-04-05 09:12:00" --until "2022-04-05 09:17:00"' | less
```

Пример конфига executer `~/.executer.conf`:

```ini
qloud_disabled = 1
project_filter = noc
project_filter = nocdev-all
```

### Конфиг ЦК

Используются следующие конфиги:

- `/etc/noc-ck/config.yml` - YAML-конфиг, в котором лежит большая часть настроек
- `/etc/noc-ck/env` - тут указано расположение YAML-конфига и некоторые вещи, которые не удалось перенести в YAML-конфиг
  типа переменных окружения для комокутора

Конфиг рендерится salt-ом из
[Аркадийного шаблона](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/nocdev-ck/files/etc/noc-ck/config.yml).
Информация по работе с конфигом есть в документации [Salt в NOCDev](https://wiki.yandex-team.ru/noc/nocdev/ops/salt/)

### Error reporting

Можно увидеть трейсбэки и error-логи в
[Error Booster](https://error.yandex-team.ru/projects/noc-ck/?filter=environment%20%3D%3D%20production)

### Дашборд с метриками

TODO ([NOCDEV-5273](https://st.yandex-team.ru/NOCDEV-5273))


## Алерты

### noc-ck-elections

Пример:

> **WARN** на [nocdev-ck:noc-ck-elections](https://juggler.yandex-team.ru/check_details?host=nocdev-ck&service=noc-ck-elections)
> в 12:15:32 MSK
>
> Election finish_scenarios has duplicate owners: sas-ck01, Election place has duplicate owners: sas-ck01,
> Election monitoring has duplicate owners: sas-ck01, Election rackcodes_updater has duplicate owners: sas-ck01,
> Election exec has duplicate owners: sas-ck01 (sas-ck01.net.yandex.net, vla-ck01.net.yandex.net)

Воркер ЦК (в примере это sas-ck01) создал больше одного лока в указанных процессах выбора лидера.
Возможные последствия - части логики ЦК залипнут, в частности:

- monitoring - отправка оповещений о статусе джобов в juggler и в startrek-комментарии
- rackcodes_updater - обновление кэша рэккодов для поддержания актуального списка устройств для ролей в
  Админке

Нужно сдать в netauto для поиска причины. Можно также ликвидировать
симптом, удалив самый старый дубликат (в примере ниже старый дубликат имеет счётчик `0000000134`, а
новый - `0000000139`):

```bash
azatkurbanov@sas-zk01:~$ /usr/lib/yandex/zookeeper-nocdev/bin/zkCli.sh

[zk: localhost:2181(CONNECTED) 0] ls -R /ck/production/elections/global/finish_scenarios
/ck/production/elections/global/finish_scenarios
/ck/production/elections/global/finish_scenarios/candidate-49d4337759fe4b52bf2207315340f6f9-0000000139
/ck/production/elections/global/finish_scenarios/candidate-be3b01ef469045df9c314c11b6e2552b-0000000134
/ck/production/elections/global/finish_scenarios/candidate-cc0450f2ba2c4209aff3689e8cec84ee-0000000136
/ck/production/elections/global/finish_scenarios/candidate-fbc24de028d14d22a372093047120dc9-0000000138

[zk: localhost:2181(CONNECTED) 1] get /ck/production/elections/global/finish_scenarios/candidate-49d4337759fe4b52bf2207315340f6f9-0000000139
sas-ck01

[zk: localhost:2181(CONNECTED) 2] get /ck/production/elections/global/finish_scenarios/candidate-be3b01ef469045df9c314c11b6e2552b-0000000134
sas-ck01

[zk: localhost:2181(CONNECTED) 3] get /ck/production/elections/global/finish_scenarios/candidate-cc0450f2ba2c4209aff3689e8cec84ee-0000000136
vla-ck01

[zk: localhost:2181(CONNECTED) 4] get /ck/production/elections/global/finish_scenarios/candidate-fbc24de028d14d22a372093047120dc9-0000000138
myt-ck01

[zk: localhost:2181(CONNECTED) 5] delete /ck/production/elections/global/finish_scenarios/candidate-be3b01ef469045df9c314c11b6e2552b-0000000134
```

### noc-ck-device-lock

> **WARN** на [nocdev-ck:noc-ck-device-lock](https://juggler.yandex-team.ru/check_details?host=nocdev-ck&service=noc-ck-device-lock)
> в 12:15:32 MSK
>
> Finished job left device locks: job_id=61f2735dccbde68cf27cc76c

Джоба с [lock constraint](https://docs.yandex-team.ru/ck/plugins/lock_constraint) завершилась, но не
подчистила за собой список заблоченных устройств. Последствия - другие джобы, работающие с тем же
набором устройств, навечно залипнут; чаще всего лочится весь датацентр.

Нужно сдать в netauto для поиска причины. Можно также ликвидировать симптом, удалив залоченные
устройства из монги

```javascript
rs0:PRIMARY> db.device_lock.distinct("job")
[ ObjectId("61efecb7ccbde68cf27cb98a") ]

rs0:PRIMARY> db.job.find({_id: ObjectId("61efecb7ccbde68cf27cb98a")}, {state: 1})
{ "_id" : ObjectId("61efecb7ccbde68cf27cb98a"), "state" : "canceled" }

rs0:PRIMARY> db.device_lock.deleteMany({job: ObjectId("61efecb7ccbde68cf27cb98a")})
{ "acknowledged" : true, "deletedCount" : 4318 }
```

### Ошибки Job of kind ... is failed

Пример оповещения об ошибке:

> **CRIT** на [man-21d3:CK-jobs](https://juggler.yandex-team.ru/check_details?host=man-21d3&service=CK-jobs)
> в 13:08:07 MSK
>
> Job of kind "huawei-spine-upgrade" is failed due to "TypeError: '<' not supported between
> instances of 'NoneType' and 'NoneType'"

Ошибка говорит о том, что над устройством man-21d3 выполнялся сценарий huawei-spine-upgrade, и в
джобе выполнения сценария случилась ошибка. Приведена последняя строчка python-трейсбэка:

```
"TypeError: '<' not supported between instances of 'NoneType' and 'NoneType'"
```

Почти всегда у таких ошибок есть Startrek-тикет, и почти всегда автор джобы (тот, кто инициировал
выполнение сценария над устройством) уже был призван в Startrek-тикет и оповещён обо всех деталях
ошибки. Чтобы найти этот тикет, можно сделать поиск в веб-интерфейсе ЦК. На примере оповещения выше:

- заходим в [веб-интерфейс ЦК](https://noc.yandex-team.ru)
- переключаемся на
  [страницу с джобами](https://noc.yandex-team.ru/jobs?state=planned%2Cscheduled%2Crunning&page=1)
- справа в форме в поле Device name вводим имя устройства man-21d3
- сбрасываем фильтры по состоянию джобов (по умолчанию, они выставлены в
  `planned,scheduled,running`)
- нажимаем Apply
- в результатах поиска находим последнюю джобу
- у этой джобы в поле Ticket видим [NOCRFCS-8762](https://st.yandex-team.ru/NOCRFCS-8762)
- далее в тикетах видим комментарий ЦК с призывом автора и деталями:
  [комментарий](https://st.yandex-team.ru/NOCRFCS-8762#6114f1fa783fcc1c8075c166)
- в комментарии указан полный traceback и шаг сценария, на котором произошла ошибка

Далее можно дебажить или завести тикет, вооружившись данными

### Ошибки от Error Booster

В ЦК есть error reporting, реализованный через Error Booster, который позволяет оповещать
по любой ошибке, найденной в рантайме (python traceback или запись в log с уровнем ERROR).
Error Booster будет оповещать о проблемах двух типов:

- NewErrors - обнаружена новая не встречавшаяся ранее ошибка
- TrendErrors - встречавшаяся ранее ошибка начала часто проявляться (больше 10 ошибок за 15 минут),
  обычно это говорит о том, что есть какая-то проблема, которую желательно исправить как можно
  скорее

Пример оповещения об ошибке NewErrors:

> **CRIT** на [api.error.yandex-team.ru:alert-540](https://juggler.yandex-team.ru/check_details?host=api.error.yandex-team.ru&service=alert-540)
> в 21:37:58 MSK
>
> Name: NOC CK: new error discovered by Error Booster
>
> Type: NewErrors
>
> Project: noc-ck
>
> Period: 5min
>
> status: CRIT(more than 0)
>
> Top error: rtapi.RtApiRpcException: HTTP Error: Resolving timed out after 5514 milliseconds
> https://error.yandex-team.ru/projects/noc-ck/errors/9845004598906102528
>
>
> [error-booster-service-error . error-booster-type-NewErrors . error-booster-project-noc-ck . noc-ck-production](https://juggler.yandex-team.ru/?query=error-booster-service-error+.+error-booster-type-NewErrors+.+error-booster-project-noc-ck+.+noc-ck-production)

Пример оповещения об ошибке TrendErrors:

> **CRIT** на [api.error.yandex-team.ru:alert-541](https://juggler.yandex-team.ru/check_details?host=api.error.yandex-team.ru&service=alert-541)
> в 10:52:30 MSK
>
> Name: NOC CK: trending error at Error Booster
>
> Type: TrendErrors
>
> Project: noc-ck
>
> Period: 15min
>
> status: CRIT(more than 0)
>
> Top error: aiozk.exc.TimeoutError:  https://error.yandex-team.ru/projects/noc-ck/errors/4453050719400919394
>
>
> [error-booster-service-error . error-booster-type-TrendErrors . error-booster-project-noc-ck . noc-ck-production](https://juggler.yandex-team.ru/?query=error-booster-service-error+.+error-booster-type-TrendErrors+.+error-booster-project-noc-ck+.+noc-ck-production)

Алгоритм действий для ошибок:

1. Получить информацию об ошибке из Error Booster:
   - traceback
   - хосты ЦК
   - компонент ЦК: web-сервер (noc-ck-api) или background worker (noc-ck-worker)
2. Получить логи за этот период
3. Завести тикет в NOCDEV или в NOCDEVDUTY
4. Прилинковать заведённый тикет к ошибке в Error Booster

### Синтаксическая ошибка в рэккоде ролей

> **CRIT** на [api.error.yandex-team.ru:alert-540](https://juggler.yandex-team.ru/check_details?host=api.error.yandex-team.ru&service=alert-540)
> в 23:25:38 MSK
>
> Name: NOC CK: new error discovered by Error Booster
>
> Type: NewErrors
>
> Project: noc-ck
>
> Period: 5min
>
> status: CRIT(more than 0)
>
> Top error: rtapi.RtApiExecException: ('InvalidArgException', 'findObjectsByRackCode', "Argument 'rackcode' of value
> '{юзерский свитч} AND NOT {Не подлежит сня... https://error.yandex-team.ru/projects/noc-ck/errors/7618446646699543859
>
>
> [error-booster-service-error . error-booster-type-NewErrors . error-booster-project-noc-ck . noc-ck-production](https://juggler.yandex-team.ru/?query=error-booster-service-error+.+error-booster-type-NewErrors+.+error-booster-project-noc-ck+.+noc-ck-production)

Ошибка связана с тем, что кто-то в админке ЦК при редактировании роли ввёл невалидный рэккод

Алгоритм действий:

1.  Заходим в [админку ЦК](https://noc.yandex-team.ru/admin)
2.  Смотрим на рэккоды в ролях (находятся в столбце Rackcode) и находим битый рэккод
3.  Нажимаем на роль для редактирования, правим рэккод и сохраняем кнопкой Save
4.  Убеждаемся, что ошибка исчезла в
    [error booster](https://error.yandex-team.ru/projects/noc-ck/?filter=environment%20%3D%3D%20production)

### app.startrek.APIError: Нет доступа к задаче

> **CRIT** на [api.error.yandex-team.ru:alert-541](https://juggler.yandex-team.ru/check_details?host=api.error.yandex-team.ru&service=alert-541)
> в 04:02:25 MSK
>
> Name: NOC CK: trending error at Error Booster
>
> Type: TrendErrors
>
> Project: noc-ck
>
> Period: 15min
>
> status: CRIT(more than 0)
>
> Top error: app.startrek.APIError: Invalid response status code: response=Response(status=403,
> body_json={'errors': {}, 'errorMessages': ['Нет доступа к задаче...
> https://error.yandex-team.ru/projects/noc-ck/errors/3806836565082812874
>
>
> [error-booster-service-error . error-booster-type-TrendErrors . error-booster-project-noc-ck . noc-ck-production](https://juggler.yandex-team.ru/?query=error-booster-service-error+.+error-booster-type-TrendErrors+.+error-booster-project-noc-ck+.+noc-ck-production)

У робота ЦК ([продовый робот](https://staff.yandex-team.ru/robot-noc-ck) или
[тестовый робот](https://staff.yandex-team.ru/robot-noc-ck-testing)) нет доступа к тикету в Startrek. ЦК при создании
джобы сразу проверяет доступ к задаче, и если доступа нет, то не даёт создать задачу (API отвечает ошибкой).
Соответственно, ошибка может возникать, когда:

- пользователь ЦК пытается настойчиво создавать джобу
- у ЦК отобрали доступ к тикету
- тикет перевели в другую очередь

Можно вернуть доступ, добавив робота в наблюдатели

### comocutor.exceptions.ConnectionException: TimeoutError

> **CRIT** на [red1-11u5:CK-jobs](https://juggler.yandex-team.ru/check_details?host=red1-11u5&service=CK-jobs)
> в 00:35:51 MSK
>
> Job of kind "declarative" is failed due to "comocutor.exceptions.ConnectionException: unable to connect to
> [ConnFabric[functools.partial(class comocutor.streamer.SshStream>, host='red1-11u5.yndx.net'), None],
> ConnFabric[functools.partial(class comocutor.streamer.TelnetStream, host='red1-11u5.yndx.net'), None]]:
> [TimeoutError(110, "Connect call failed ('213.180.201.185', 22)"),
> TimeoutError(110, "Connect call failed ('213.180.201.185', 23)")]"

У ЦК таймаут при попытке соединиться с устройством. В данном конкретном случае это вызвано тем, что ЦК не имеет доступа
в management-сеть устройства

Проверить можно через панчер на примере одного из контейнеров ЦК vla-ck01:

- видим отсутствие правил от ЦК до проблемного устройства
  [в панчере](https://puncher.yandex-team.ru/?source=vla-ck01.yndx.net&destination=red1-11u5.yndx.net&rules=exclude_rejected&values=all&sort=source)
  (устройство в [`_WIFIEXTERNALNETS_`](https://racktables.yandex-team.ru/index.php?page=macros&macro_name=_WIFIEXTERNALNETS_))
- для сравнения можно увидеть наличие правил до другого "хорошего" устройства
  [в панчере](https://puncher.yandex-team.ru/?source=vla-ck01.yndx.net&destination=red1-23u7.yndx.net&rules=exclude_rejected&values=all&sort=source)
  (менеджмент в [`_SWITCHMGMTNETS_`](https://racktables.yandex-team.ru/index.php?page=macros&macro_name=_SWITCHMGMTNETS_))
