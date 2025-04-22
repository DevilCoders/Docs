## Греп с помощью executer

Полезные ссылки:
* [Установка executer](https://wiki.yandex-team.ru/executer/#ustanovka)
* [Про логирование в duffman](https://github.yandex-team.ru/Daria/Duffman/wiki/Логирование)

В ~/.executer.conf нужно добавить:
```
default_user = <login>
project_filter = mail
rtc_disabled = disabled
qloud_disabled = disabled
```

Мы записываем логи duffman в /var/log/duffman/, и логи nginx в /var/log/nginx/

Пример грепа по продакшену корпоративного календаря по логу duffman-access:
```
executer
p_exec %mail_maya-corp_production_maya grep MODEL_REJECTED /var/log/duffman/duffman-access.tskv
```
Где %mail_maya-corp_production_maya - группа машин в qloud. mail - проект, maya-corp - приложение, т.е. корпоративный календарь, production - окружение, maya - компонент.

На машинках логи хранятся в течении трех дней, если нужно более древние логи, то грепать нужно по [YT](YT.md).

## Cookbook

### Топ запросов за моделями

Пример запроса
```
grep -o name=[a-z-]* /var/log/duffman/duffman-access.tskv | sort | uniq -c | sort -rn
```

Пример ответа
```
fresk@iva7-d7a41f534908.qloud-c.yandex.net:   91343 name=auth
fresk@iva7-d7a41f534908.qloud-c.yandex.net:   50175 name=get-modified-event-ids
fresk@iva7-d7a41f534908.qloud-c.yandex.net:   50174 name=get-modified-events
fresk@iva7-d7a41f534908.qloud-c.yandex.net:   49203 name=get-events
fresk@iva7-d7a41f534908.qloud-c.yandex.net:    7562 name=get-availabilities
...
```

### Топ запросов за моделями с таймингом более одной секунды за 2019-02-20, 14 часов по логу nginx

```bash
grep timestamp=2019-02-20T14 /var/log/nginx/access_log.tskv | grep -E "request_time=[1-9]" | grep -o models=[_a-z-]* | sort | uniq -c | sort -rn
```

### Удобный способ смотреть tskv

```
cat tskv | sed -e "s/tskv\t/------------------------------------------------------\n/" | sed -e "s/\t/\n/g"
```
