### Что делает сервис
Сервис **notsolitesrv** складывает тела писем в MDS и складывает метаданные через аппхост в базу
### В него ходят:
- NWSMTP. В случае получения ошибки от письмо передается в Postfix (только для асинхронных операций)
- Postfix. Может копить очередь и ретраить запросы
- IMAP. Складывает письма пользователям через APPEND
### Он ходит в:
- Blackbox для резолва уида
- Furita для получения черных/белых списков (bwlist)
- Furita для получения списка правил обработки почты и передачи в tupita
- Tupita для получения резолюции применения пользовательских фильтров
- MDS чтобы положить тело письма
- Postback, отправляет мета-письмо в случае неудачного сохранения
- Forwards/Yaback, пересылка и уведомления
- msearch для получения списка (внешних) рассылок (от которых пользователь отписан или не отписан). В случае, если пользователь отписан - кладем письмо в trash

### Импакт отключения сервиса
- не сможем сохранить черновики на сервере
- не сможем сохранить письма извне в базу и/или сторадж

### Логи сервиса
- /var/log/notsolitesrv/access.tskv
- /var/log/notsolitesrv/attach.tskv
- /var/log/notsolitesrv/notsolitesrv.tskv
- /var/log/notsolitesrv/user_journal.tskv
- /var/log/notsolitesrv/http_client.tskv
- /var/log/notsolitesrv/yplatform.log

### Управление сервисом:
Старт:
supervisorctl start notsolitesrv
Стоп:
supervisorctl stop notsolitesrv