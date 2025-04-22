restarter
=========
Утилита проверяет статус процесса через monrun и, при необходимости, выполянет рестарт.

Пример monrun конфигурации
```
[dns_local]
execution_interval=60
execution_timeout=30
command=/usr/bin/dig @localhost localhost > /dev/null && echo "0;Ok" || echo "2;DNS is down!"
type=common

restart_command=service bind9 restart
restart_attempt=10
restart_window=700
restart_min_interval=60
restart_where_description=DNS is down!
```

restarter запускается по cron-у раз в минуту.

Все интервалы задаются в секундах.

* **restart_command** - команда для рестарта
* **restart_attempt** - максимальное количество попыток рестарта в пределах заданного окна restart_window
* **restart_min_interval** - минимальный интервал между рестартами
* **restart_window** - интервал времени, в пределах которого подсчитываются попытки рестарта (счетчик попыток обнуляется после завершения интервала)
* **restart_where_description** - строка, если не пустая, то сравниваем с description в выводе monrun

Логи находятся здесь: `/var/log/restarter/restarter.log`.

Файлы со списком попыток рестарта сохраняются здесь: `/dev/shm`. Каждая строчка соотвествует одной попытке рестарта. В каждой строке записано unixtime, когда производился рестарт.

Тикет с обсуждением http://st.yandex-team.ru/VSADMIN-172
