
[Документация на comocutor](https://noc-gitlab.yandex-team.ru/nocdev/comocutor/-/blob/master/README.md "Comocutor").
Включить дебаг комокутор можно установив переменную COMOCUTOR_DEBUG.

## Включаем дебаг в коде

Пример скрипта для отладки подключения к хосту используя автоматическое определение параметров подключения: 

```python
import sys
import logging
import os
import asyncssh

# отключение nocauth
os.environ["COMOCUTOR_NO_NOCAUTH"] = "1"

from comocutor.yandex import rt_filter
from comocutor.credentials import Credentials
from comocutor.deploy import async_bulk

logging.basicConfig(level=logging.DEBUG, format="%(asctime)s - %(filename)s:%(lineno)d - %(funcName)s() - %(levelname)s - %(message)s")

# очень подобный дебаг от asynssh
asyncssh.logging.set_log_level(logging.DEBUG)
asyncssh.logging.set_sftp_log_level(logging.DEBUG)
asyncssh.logging.set_debug_level(3)

async def do(conn, hostname, breed):
    print("do", hostname)

# опциональное указание учетки
credentials = Credentials(login="username", password="")
res = async_bulk(rt_filter("{$cn_ololo}"), do, show_report=False, credentials=credentials)
```

Пример с ручным указанием типа подключения и типа CLI. RTAPI не используется.
```python
import sys
import logging
import os
import asyncssh
import asyncio
from functools import partial

os.environ["COMOCUTOR_NO_NOCAUTH"] = "1"

from comocutor.devices import ConnFabric, VrpDevice
from comocutor.streamer import SshStream
from comocutor.credentials import Credentials

logging.basicConfig(level=logging.DEBUG, format="%(asctime)s - %(filename)s:%(lineno)d - %(funcName)s() - %(levelname)s - %(message)s")

asyncssh.logging.set_log_level(logging.DEBUG)
asyncssh.logging.set_sftp_log_level(logging.DEBUG)
asyncssh.logging.set_debug_level(3)


async def do(hostname):
    ssh_partial = partial(SshStream, host=hostname)
    credentials = Credentials()
    fabric = ConnFabric(stream=ssh_partial)
    host_conn = VrpDevice(conn_fabric=[fabric], name=hostname, credential=credentials)
    await host_conn.connect()
    res = await host_conn.cmd("uptime")
    print(res.out)

loop = asyncio.get_event_loop()
loop.run_until_complete(do("ololo"))
```
