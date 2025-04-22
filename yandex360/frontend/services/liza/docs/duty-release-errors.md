# Дежурство по ошибкам после релиза
 
Каждый разработчик после выкатки еженедельного технического релиза должен уделить достаточное время,
чтобы погрепать и починить [ошибки из логов](https://wiki.yandex-team.ru/Pochta/frontend-dev/doc/weberror).

Каждой созданной задаче надо поставить метку [release-logs](https://st.yandex-team.ru/daria/filter?tags=release-logs).
Чтобы не создавать одни и те же задачи, по метке можно смотреть, что разобрано, но еще не исправлено.
 
Что надо исправлять:
 1. Ошибка из браузера `/monitoring_liza.txt` с `&errorType=` из `/var/log/nginx/mail/access.log`
 2. Ошибки серверного JS: любые записи со словами `ERROR` или `EXCEPTION` из `/var/log/wmi/jsintegration.log`
 3. Непойманные (uncaught errors) ошибки серверного JS: все записи из `/var/log/wmi/exception.log`

Найденные ошибки в u2709 исправлеяет тот, кто их нашел.
Если вы нашли большую порцию ошибок, но она не относится к u2709, надо поставить задачу на ответственного за другой кусок. 

## Как грепать

Заходим на [logstore](/Daria/codestyle/blob/master/executer.md) и грепаем ошибки релиза.

Пример грепа:
```
 executer "p_exec %mail_web fgrep 'monitoring_liza' /var/log/nginx/mail/access.log.0 | fgrep '&cv=jane-10.10' | fgrep '&errorType' " > logs-06-24
```

Что тут находится:
 1. `fgrep 'monitoring_liza'` - ошибки из liza
 2. `/var/log/nginx/mail/access.log.0` - ошибка за вчера
 3. `fgrep '&cv=jane-10.10'` - отсекаем нужный релиз или сборку
 4. `fgrep '&errorType'` - фильтру "только ошибки"
 5. `  > logs-06-24` - файл, куда будут записаны логи
 
После этого можно разбить ошибки по типам

```
$ grep -o 'errorType=[^& ]*' logs-06-24 | sort | uniq -c | sort -rn
 190680 errorType=ns.events
 167192 errorType=HandlerError
  80792 errorType=promise.exception
  54095 errorType=handlersjsx.httperror
  23539 errorType=imgError
   6346 errorType=JSError
   4303 errorType=RunFailed
   2013 errorType=compose.save.failed
   1994 errorType=bootstrap.xhr-load-error
   1091 errorType=socialavatars.error.noimg
    588 errorType=VeryLongLoading
    382 errorType=ns.action
    243 errorType=User%20doesn%27t%20have%20email
    213 errorType=UploadFail
    163 errorType=simpleUpload
    154 errorType=yate.run
    153 errorType=bootstrap.loaderror
    149 errorType=compose.http
    131 errorType=FatalError
    123 errorType=no_such_message
    112 errorType=FirstDraw
     82 errorType=simpleUpload.json_parse
     52 errorType=fail-do-attach-file-store
     38 errorType=blob-script-error
     33 errorType=fail-do-attach-file-status
     30 errorType=message-body.error
     21 errorType=upload.disk.xhr_fail
     20 errorType=jane-import
     14 errorType=messages-pager.infinity
     13 errorType=FirstRequest
     12 errorType=noPassportResponse
      6 errorType=ns-model-call
      4 errorType=PROCESS_BODY_ERROR
      4 errorType=bootstrap.invalid-size
      3 errorType=upload.disk.failed
```

## Что чинить

Чинить надо самые массовые ошибки. В каждом `errorType` обычно бывает разбивка по группам.
Например, в `errorType=ns.events` есть разбивка по названию события, а в `errorType=HandlerError` по названию модели.
Конкретные поля зависят от типа ошибки.

Например, `ns.events`

```
$ fgrep 'errorType=ns.events' logs-06-24 | grep -o '&name=[^& ]*' | sort | uniq -c | sort -rn
 126535 &name=daria%3AvToolbarButton%3AdroppableDestroy
  21607 &name=ns-page-before-load
  20481 &name=ns-model-changed.to
   4346 &name=daria%3AvToolbarButton%3AdroppableInit
   4056 &name=daria%3AvToolbarButton%3AupdateName
   3126 &name=ns-view-destroyed
   2364 &name=ns-model-init
   1537 &name=daria%3AvAbookContacts%3AselectionChanged
   1430 &name=ns-model-changed.formIsShown
    965 &name=daria%3AvToolbarSettings%3ApopupClosed
    574 &name=change
    505 &name=ns-model-changed.cc
    393 &name=ns-view-hide
    379 &name=daria%3AvMap%3AinitMap
    350 &name=ns-view-show
    319 &name=ns-page-after-load
    274 &name=ns-model-changed.from_mailbox
    232 &name=ns-model-changed.signature
    177 &name=%23%20sent
    170 &name=pageinit
    168 &name=ns-model%3Adraft-saved
    128 &name=daria%3AvMessageThread%3AfocusEvent
     84 &name=ns-model-changed.bcc
     84 &name=daria%3AvToolbarButtonArchive%3AdoArchive
     80 &name=daria%3AvScrollerMessage%3Ascroll
     63 &name=daria%3AvToolbarSettings%3AbuttonOptionsChanged
     52 &name=daria%3AvMessages%3AmarkImportant
     38 &name=hotkeys.to-search-input
     35 &name=ns-view-htmlinit
     27 &name=pageVisible.change
     24 &name=daria%3AvMessageThreadList%3AcheckVisible
     18 &name=yabs%3Aloaded
     12 &name=daria%3AvMessagesItem%3Achecked
     12 &name=%23%20html
      8 &name=daria%3AvMessages%3Achecked-message-hover
      6 &name=ns-view-touch
      6 &name=closed
      4 &name=daria%3AvMessageThreadList%3AscrollToNextUnread
      2 &name=edit%20%3E%20save
      2 &name=daria%3AvMessages%3AmoveFocusToLastMessage
      1 &name=daria%3AvMessagesItemThread%3AloadMoreMessages
```
