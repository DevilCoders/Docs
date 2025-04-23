1. Конфигурация демона syslog-ng для сбора логов из unix socket /var/log.

Все записи в сокете с тегом python-taxidwh фильтруются в файл /var/log/taxidwh/log/python-taxidwh-tskv.log

Пример как отправить запись в сокет из bash:
```logger -t python-taxidwh hello bash```

В python для записи сообщений в сокет надо использовать стандартный модуль logging, а именно SyslogHandler + кастомный format (добавить в начало каждой записи тег с двоеточнием).

2. Конфигурация демона logrotate для удаления старых логов.
