# Методические указания по поиску неисправностей
## RTAPI
### Графики
[Dashboard, rtapi/mysql](https://monitoring.yandex-team.ru/projects/racktables/dashboards)

### rtapi2rr workers  
Критерии проблемности:
* Если worker в работе более 10 минут. 
* Мало workers(меньше 30)
* Очевидные отличия проблемного worker(память или не меняется статус)

**FreeBSD**:  
`rtapi2rr -c /usr/local/etc/rtapi2rr.yml rrtcp:workers -i`  

**Ubuntu**:  
`rtapi2rr -c /etc/rtapi2rr.yml rrtcp:workers -i`  
prestable медленно отвечает, когда мало параллельных запросов - ожидаемое поведение.  

#### Restart workers

{% cut "Если вы уверены, что воркеров не спасти и ясна причина аварии"  %}

**FreeBSD**:  
`sudo -H -u racktables rtapi2rr -c /usr/local/etc/rtapi2rr.yml rrtcp:reset`

**Ubuntu**:  
`sudo -H -u racktables rtapi2rr -c /etc/rtapi2rr.yml rrtcp:reset`

Для серьёзных случаев подойдёт `systemctl restart`, учитывайте, что сервис поднимается обратно пару минут.

{% endcut %}

### Syslog
```
/var/log/rtapi-local-server.log
/var/log/nginx-access.log
/var/log/messages
```
Для ubuntu:
```
sudo journalctl -eu rtapi2rr
/var/log/syslog
```


### MySQL
Процессы 'repl' ожидаемо имеют большое время обработки
```
sudo -H mysql racktables
SELECT * FROM INFORMATION_SCHEMA.PROCESSLIST ORDER by Time;

```
### Cron
`/var/log/cron`  
`sudo crontab -l -u racktables`   


# Шаблоны описания
При описании бага, рекомендуется придерживаться описанных шаблонов.  
Это не саботаж исправления, некоторые баги являются частью действующего дизайна и ожидают его исправления.

{% cut "Шаблон Бага" %} 

**Название/Тикет:**  Заголовок  
**Симптомы:**  Характерные проявления, логи, как опознать.  
**Условие проявления:** Окружение необходимое для воспроизведения.  
**Триггер:** Запрос или действие после которого проявляется баг.   
**Влияние:**  Критичность, на сколько пострадали сервисы и какие.  
**Обходное решение:** Если нельзя исправить, способ обойти или снизить влияние.  
**Восстановление:** Как восстановить и проверить сервисы.   
**Тесты/исправления/тикеты:**

{% endcut %}

