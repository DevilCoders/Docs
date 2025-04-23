### Метрики
Dashboard:
<iframe height="800" width="100%" frameborder="0" src="https://monitoring.yandex-team.ru/embed/gfglister/dash/monm6ts2h94f5e7h5qoh?from=now-120m&to=now"></iframe>

[Срез статусов по всем хостам](https://nda.ya.ru/t/aeEhUtGQ5FHw2D).
**error_total** - ошибки получения конфига или сохранение.\
**inflight_total** - в процессе получения конфига.\
**success_total** - успешно полученный конфиг.\
**success_diff_total** - успешно полученный конфиг, но с диффом. \
**success_diff_period_total** - успешно полученный конфиг, но с диффом и процесс получения конфига был вызван внутренним таймером.
Говорит о том, что не получили сигнал о сохранении конфига.\
**unknown_total** - Нет состояния так как сервер запустился недавно или новых хост.

### Отладка

Вызов ручки для обновления конфига конкретного хоста:
```shell
curl -s --data '{"hostname":"sas1-s10.yndx.net"}' 'http://localhost:80/update_config'
```
Или для всех хостов:
```shell
curl -s 'http://localhost:80/update_config_all'
```

Можно послать трап с whitebox
```shell
etckeeper sendtrap
```

Эмуляция вебхука:
```shell
curl -s --data '{
		  "data": {
			"fqdn": "sas1-s348.yndx.net",
			"ip": "2a02:6b8:0:c011:0:210:c:9f",
			"timestamp": 1655474844,
			"committer": ""
		  },
		  "format": "post_fn_config",
		  "uuid": "b2f51ade-7935-4d6c-afa6-94d9718169bd",
		  "hostname": "vla-snmptrap1.net.yandex.net"}' 'http://localhost:80/config'
```

Получения статусов хостов:
```shell
curl -s 'http://localhost:80/get_status' | python3 -m json.tool
```

Получение хостов с ошибкой:
```shell
curl -s 'http://localhost:80/get_status' | jq '.data | .[] | select(.status == 2)'
```
```json
{
    "code": 200,
    "response": "OK",
    "data": {
        "sas1-s10.yndx.net": "lastSuccessfulUpdateTime=0001-01-01T00:00:00Z lastErrorTime=2022-06-27T17:50:31+03:00 lastError=max amount of retries reached, last error: get_config from sas1-s10.yndx.net error fork/exec /usr/bin/get_config: no such file or directory stderr= locked=false"
    }
}
```

Проверка получения конфигурации:
```shell
NOCAUTH_ONLY=1 COMOCUTOR_LOGIN=robot-gfglister COMOCUTOR_IDENTITY=/etc/gfglister/robot-gfglister /usr/bin/get_config -d lab-vla-i01.yndx.net < /dev/null
```

Статус мастера из zk
```shell
zk get /gfglister_dev/master -s iva-zk01.net.yandex.net
```

Логи в journald:
```shell
июл 22 21:47:00 vla-gfglister1.net.yandex.net gfglister[61517]: 2022-07-22T21:47:00.733+0300        DEBUG        gfglister/gfglister.go:664        callConfigChange        {"hostname": "ben-42u2.yndx.net", "comment": "from [::1]:51704 at 2022-07-22T21:47:00+03:00", "source": "confChangeSourceWeb"}
июл 22 21:48:33 vla-gfglister1.net.yandex.net gfglister[61517]: 2022-07-22T21:48:33.191+0300        DEBUG        xretry/retry.go:77        starting callback with retry        {"callback": "confGetter_ben-42u2.yndx.net"}
июл 22 21:48:33 vla-gfglister1.net.yandex.net gfglister[61517]: 2022-07-22T21:48:33.191+0300        DEBUG        comocutorConfigGetter        gfglister/configgetter_comocutor.go:52        get config        {"hostname": "ben-42u2.yndx.net"}
июл 22 21:48:33 vla-gfglister1.net.yandex.net gfglister[61517]: 2022-07-22T21:48:33.191+0300        DEBUG        comocutorConfigGetter        gfglister/configgetter_comocutor.go:133        get config using conf_get        {"hostname": "ben-42u2.yndx.net"}
июл 22 21:48:33 vla-gfglister1.net.yandex.net gfglister[61517]: 2022-07-22T21:48:33.191+0300        DEBUG        comocutorConfigGetter        gfglister/configgetter_comocutor.go:154        exec        {"cmd": "/usr/bin/get_config ben-42u2.yndx.net", "stdout": ""}
```
