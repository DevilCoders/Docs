# Comocutor

Модуль для работы с CLI различных девайсов (свичей, коммутаторов, обычные сервера, PDU, DWDM).

Ключевые преимущества:
- Няшная аутентификация. Модуль может использовать SSH-ключи, SSH-агента, спросить пароль и даже зашифровать его и использовать в
  дальнейшем. Есть возможность передать учетные данные через env-переменные.
- Обработка ошибок. Модуль всегда выбрасывает исключение, если команду не удалось выполнить. Больше не нужно беспокоиться, что команды будут
  выполнены не в том контексте.
- Вывод команд приводится к ожидаемого виду. Убираются упячки и кракозябры, вставляемые свитчем для управления терминалом.
- Модуль умеет отвечать на вопросы свитча.

Disclaimer: работоспособность и обработка ошибок расширяются по мере возникновения проблем.
Такой подход by design не даёт гарантий для неиспользованного ранее функционала, но иначе проект бы никогда не сошелся.
При наличии проблем/артефактов - сообщайте.

## Примеры

Используется RackTables(в make_connection) для определения типа устройства перед подключением к нему.

```python
import asyncio
from comocutor.yandex import make_connection


async def main():
    host, breed = await make_connection("sas1-s186.yndx.net")
    res = await host.cmd("dis interface 40GE1/0/1:1")
    print(res.out)


loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

Несколько команд в одной строке.

```python
import asyncio
from comocutor.yandex import make_connection


async def main():
    host, breed = await make_connection("sas1-s186.yndx.net")
    res = await host.cmds("""
        dis interface 40GE1/0/1:1
        dis interface 40GE1/0/1:2
        """)
    for cmd, cmd_res in res:
        print(cmd, cmd_res)
    await host.close()
    await asyncio.sleep(0.01)


loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

Пример массового выполнения команды по хостам из RT-фильтра:

```python
from comocutor.deploy import async_bulk
from comocutor.yandex import rt_filter


async def do(conn):
    res = await conn.cmd("dis interface brief | inc 40GE")
    return res.out


res = async_bulk(rt_filter("[некоторые свитчи huawei]"), do)

for host, host_out in res.items():
    if isinstance(host_out, Exception):  # async_bulk() может вернуть исключение
        print("Exception on host %s: %r", host, host_out)
    else:
        print(host, repr(host_out))

```

Выбор команды в зависимости от вендора:

```python
from comocutor.yandex import make_connection, rt_filter
from comocutor.devices import VrpDevice, IosDevice


async def main():
    fqdns = rt_filter("[некоторые свитчи]")
    for fqdn in fqdns:
        host, breed = await make_connection(fqdn)
        if isinstance(host, IosDevice):
            res = await host.cmd("show route 95.108.237.230")
        elif isinstance(host, VrpDevice):
            res = await host.cmd("display ip ro 95.108.237.230")
        else:
            raise Exception("unknown breed %s" % breed)
        print(fqdn, res.out)
```

Можно не использовать RT, а создать подключение руками:

```python
from comocutor.devices import VrpDevice, ConnFabric
from comocutor.streamer import SshStream
from functools import partial


async def main():
    host = "host"
    ssh_partial = partial(SshStream, host=host)
    fabric = ConnFabric(stream=ssh_partial)
    host_conn = VrpDevice(conn_fabric=[fabric], name=host)
    await host_conn.connect(timeout=3)
    res = await host_conn.cmd("show route 95.108.237.230")
    print(res.out)
```

Если нужно ходить на устройства с парольной авторизацией, то есть несколько вариантов:

1. Передать пароль через переменную окружения COMOCUTOR_PASSWORD или несколько паролей через COMOCUTOR_PASSWORDS.
2. Спросить пользователя:

```python
from comocutor.yandex import make_connection
from comocutor.credentials import Credentials, ask_pass

credential_storage = Credentials(prompt_cb=ask_pass)
host, breed = await make_connection(hostname, credential_storage)
```

3. TODO: Использование зашифрованного пароля.

## Аутентификация

Настройки аутентификации по умолчанию отлично работают в большинстве случаев. Но если нужно изменить дефолтное поведение, то нужно
определить объект Credentials. Например:

```python
credentials = Credentials(login="nobody", password="nonono")
await make_connection(hostname, credentials)
```

Порядок определения логина в классе Credentials:

1. login переданный как аргумент
2. переменная окружения COMOCUTOR_LOGIN
3. текущий [пользователь](https://docs.python.org/3.6/library/getpass.html#getpass.getuser)

Порядок определения ключа:

1. переменная окружения COMOCUTOR_IDENTITY
2. ключ пользователя
3. ssh-agent

Порядок определения пароля:

1. password переданный как аргумент
2. переменная окружения COMOCUTOR_PASSWORDS
3. переменная окружения COMOCUTOR_PASSWORD
4. спросить пароль, если передан аргумент prompt_cb

По умолчанию модуль пытается ходить на свитчи через Nocauth. Если устройство не поддерживается, то идёт напрямую. Если нужно сразу идти
напрямую, нужно указать переменную COMOCUTOR_NO_NOCAUTH=1

## Установка или обновление

```bash
python3 -m pip install -i https://pypi.yandex-team.ru/simple/ -U comocutor
```

### Переменные окружения

```COMOCUTOR_ENABLE_SSH_CONF``` - включает использование конфига ~/.ssh/config.\
```COMOCUTOR_SSH_FORWARD_AGENT``` - путь до сокета skotty для проброса агента без указания конфига ssh.\
```COMOCUTOR_IDENTITY``` - путь к приватному ключу для аутентификации по SSH.\
```COMOCUTOR_LOGIN``` - имя пользователя.\
```COMOCUTOR_PASSWORDS``` - пароли разделенные пробелом.\
```COMOCUTOR_PASSWORD``` - пароль.\
```COMOCUTOR_NO_PUBKEY_AUTH``` - не использовать авторизацию по ключу.\
```COMOCUTOR_NO_NOCAUTH``` - ходить напрямую на устройство, без использования Nocauth.\
```NOCAUTH_FORCE``` - аналог `nocssh --force`.\
```NOCAUTH_ONLY``` - не пробовать другие методы, если не вышло с nocauth.\
```COMOCUTOR_DEBUG``` - Включить дебаг comocutor и asyncssh.\
```COMOCUTOR_TUNNEL``` - туннель или "джампхост". Формат ```host1,host2|host1,host3```. Где host в
формате ```[user1@]jumphost1.example.org[:22]```. Через ```|``` указывается альтернативный путь.
