# Отладка проблем с сетью

Одной из распространённых проблем при разработке задач является недоступность какого-либо сервиса, расположенного внутри или снаружи Яндекса.

Для отладки таких проблем воспользуйтесь следующим чеклистом:
{# puncher}
1. Наличие дырки в puncher. Подробнее [здесь](../firewall.md).
{ #ipv4 }
2. Обращение к внешним хостам. Проврьте их на IPv4. Подробнее [здесь](../dev/requirements.md#dns).
{ #custom-container }
3. Использование кастомного контейнера. Проверьте настройки сети внутри него: содержимое ```/etc/resolv.conf``` и т.п.
{ #embedded-container }
4. Использование вложенной контейнеризации, docker. Проверьте настройки сети внутри этого контейнера.
{ #base-debug }
5. Попробуйте [shell](web-shell.md) и выполните базовые проверки сетевой доступности
```
host <dst_fqdn>
ping6 <dst_ip>
nc -6vz <dst_fqdn> <dst_port>
```
Подробнее можно посмотреть, какую информацию запрашивает NOC при обращении к ним: [noc/troubleshooting](https://wiki.yandex-team.ru/noc/troubleshooting/).

6. Используйте возможность собрать TCP dump, задав специальный параметр в задаче:
```python
from sandbox.common.types import task as ctt

from sandbox import sdk2


class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        tcpdump_args = "-v 'host foo.yandex.net'"  # Tcpdump arguments that are used for network packets logging.
        suspend_on_status = [ctt.Status.EXCEPTION, ctt.Status.FAILURE]  # Suspend on one of the selected statuses.
```
