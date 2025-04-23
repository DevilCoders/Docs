Синхронизация тарифов
=====================

В этой папке хранятся скрипты для работы с синхронизованными тарифами.

switch.py
---------

Включение/выключение/проверка статуса.

```
$ ssh ymsh01e.mobile.yandex.net PYTHONPATH=/usr/lib/yandex/taxi-client python switch.py check
Sync is off
$
```

Проверка, идут ли запросы на синхронизацию.

```
echo "p_exec %taxi_cabinet timetail -n30 /var/log/nginx/access.log | grep get_tariffs" | executer | grep -o 'id=[0-9a-z]*' | sort | uniq -c
```

Мониторинг, берутся ли заказы и какая цена.

```
$ ssh ymsh01e.mobile.yandex.net PYTHONPATH=/usr/lib/yandex/taxi-client python monitor.py
```
