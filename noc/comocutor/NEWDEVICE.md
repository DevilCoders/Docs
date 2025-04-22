Создадим заготовку:
```python
import sys
import asyncio
import logging

from functools import partial

from comocutor.devices import BasicDevice, ConnFabric
from comocutor.streamer import SshStream

logging.basicConfig(level=logging.DEBUG,
                    format="%(asctime)s - %(filename)s:%(lineno)d - %(funcName)s() - %(levelname)s - %(message)s")


class BlankDevice(BasicDevice):
    pass


async def main(host, cmd):
    ssh_partial = partial(SshStream, host=host)
    fabric = ConnFabric(stream=ssh_partial)
    host_conn = BlankDevice(conn_fabric=[fabric], name=host)
    await host_conn.connect(timeout=5)
    res = await host_conn.cmd(cmd)
    print(res.out)


host = sys.argv[1]
cmd = sys.argv[2]

asyncio.get_event_loop().run_until_complete(main(host, cmd))
```
Такой класс уже можно натравить на устройство, он, конечно, будет выдавать ошибки чтения, но таким образом удобно получать сырые данные от устройства.

Для нового устройства нужно сделать тесты в comocutor/tests/data/$new_device_cls.py. По аналогии с другими классами.

Промпты. Задаётся в COMMAND_PROMPT. В тесте переменная PROMPT_VARIANTS.
Нужно собрать несколько промптов. Обычный и в режиме конфигурации. Если они меняются в зависимости от контекста, то добавить примеров и с контекстом.


Ошибки. Задаётся в COMMAND_ERROR. В тесте переменная COMMAND_ERROR_VARIANTS.
Нужны примеры когда команда неизвестна, команда неполная или неправильный аргумент, нет прав


Вопрос. Задаётся в QUESTION. В тесте переменная QUESTION_VARIANTS.
Например при сохранении и ребуте бывает вопрос.


Вопрос при входе. Задаётся в CLI_INIT_QUESTION.
Бывает ли вопрос при входе на устройство. Смена пароля например.
