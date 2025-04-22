# Требования к агенту

При необходимости каждая задача может объявить [требования к агентам](../tasks.md#requirements), на которых она должна запускаться.
Все параметры задаются в классе **Requirements** внутри класса задачи.
Требования могут быть изменены в [server-side методах задачи](task-life.md#server-side).

```python
from sandbox import sdk2
import sandbox.common.types.client as ctc
import sandbox.common.types.misc as ctm
import sandbox.common.types.task as ctt

from sandbox.projects.common.environments import SandboxJavaJdkEnvironment
from sandbox.projects.common.environments import SandboxMavenEnvironment

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        cores = 1  # Require 1 CPU core
        ram = 1024  # Require 1024 Mib RAM
        disk_space = 100  # Require at least 100 Mib of disk space
        host = "sandbox042.search.yandex.net"  # Execute on specific agent
        privileged = True  # Require root permissions (container in privileged mode)
        client_tags = ctc.Tag.SSD & (ctc.Tag.LINUX_TRUSTY | ctc.Tag.LINUX_XENIAL) & ~ctc.Tag.MAN  # Require SSD disks, Ubuntu Trusty or Xenial and not MAN datacenter
        ramdrive = ctm.RamDrive(ctm.RamDriveType.TMPFS, 30 * 1024, None)  # Mount /tmpfs into memory
        dns = ctm.DnsType.DNS64  # Enable NAT64 to access to IPv4-only hosts
        environments = [SandboxJavaJdkEnvironment("1.8.0"), SandboxMavenEnvironment("3.2.2")]  # Require JDK 1.8.0 and Maven 3.2.2 installed
        semaphores = ctt.Semaphores(  # Acquire a semaphore before running and release it when finished or interrupted
            acquires=[
                ctt.Semaphores.Acquire(name="my_semaphore_name")
            ],
            release=(ctt.Status.Group.BREAK, ctt.Status.Group.FINISH)
        )
        porto_layers = [2463138505]  # Require porto layers stored in specified resources
        tasks_resource = 1826744342  # Override default archive with tasks source code
        container_resource = 1718293390  # Run everything using LXC image stored in specified resource
        resources = [2463138505, 1718293390]  # Download specific resources to task
```

На мультислотовых агентах количество открытых файловых дескрипторов ограничивается значением 300000.

## Фильтрация агентов по тегам { #tags }

Наиболее гибким способом выбора агента является фильтрация [по тегам](../agents.md#tags).
Теговое требование к агентам задаётся при помощи поля `client_tags`.
Самый простой способ фильтрации – это передать в поле один тег:

```python
import sandbox.common.types.client as ctc

client_tags = ctc.Tag.SSD
```

При помощи [побитовых операций](https://docs.python.org/3.9/reference/expressions.html#binary-bitwise-operations) можно требовать наличия или отсутствия нескольких тегов:

```python
import sandbox.common.types.client as ctc

client_tags = (ctc.Tag.LINUX_TRUSTY | ctc.Tag.LINUX_XENIAL)  # Ubuntu Trusty or Ubuntu Xenial
client_tags = ~ctc.Tag.MAN  # Not MAN datacenter
client_tags = ctc.Tag.INTEL_E5_2650 & ctc.Tag.LINUX_PRECISE  # Intel E5 2650 CPU and Ubuntu Precise
```

Если вы определяете пользовательские теги, их также можно передавать аналогичным образом:

```python
import sandbox.common.types.client as ctc

client_tags = ctc.Tag.Group.LINUX & ctc.Tag.USER_MONOREPO
```

Полный список тегов можно посмотреть [в коде](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/types/client.py).
Основные группы тегов приведены в таблице:

Группа | Теги
:--- | :---
Модель CPU | `INTEL` - любой Intel, `INTEL_E5_2683`, `INTEL_E5_2683V4`, `INTEL_E5_2650`, `INTEL_E5_2650V2`, `INTEL_E5_2660`, `INTEL_E5_2660V1`, `INTEL_E5_2660V4`, `INTEL_E5_2667`, `INTEL_E5_2667V2`, `INTEL_E5_2667V4`, `INTEL_X5675`, `INTEL_GOLD_6230`, `INTEL_GOLD_6230R`, `INTEL_GOLD_6338`, `INTEL_E5645`, `INTEL_E312XX`, `INTEL_3720QM`, `INTEL_4278U`, `INTEL_4578U`, `INTEL_8700B`, `AMD` - любой AMD, `AMD6176`, `ARM`, `KVM`
Операционная система `OS` | `LINUX` - любой Linux <br/> `LINUX_PRECISE` - Ubuntu 12.04 <br/> `LINUX_TRUSTY` - Ubuntu 14.04 <br/> `LINUX_XENIAL` - Ubuntu 16.04 <br/> `LINUX_BIONIC` - Ubuntu 18.04 <br/> `LINUX_FOCAL` - Ubuntu 20.04 <br/> `OSX` - любая версия MacOS <br/> `OSX_SIERRA` - MacOS 10.12 <br/> `OSX_HIGH_SIERRA` - MacOS 10.13 <br/> `OSX_MOJAVE` - MacOS 10.14 <br/> `OSX_CATALINA` - MacOS 10.15 <br/> `WINDOWS` - свежая версия Windows 10 с поддержкой [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
Тип диска `DISK` | `HDD` - жесткий диск <br/> `SSD` - твердотельный диск
IP-адрес `NET` | `IPv4` - у агента есть IPv4-адрес <br/> `IPv6` - у агента есть IPv6-адрес
Датацентр `DC` | `IVA` - Ивантеевка <br/> `SAS` - Сасово <br/> `MYT` - Мытищи <br/> `VLA` - Владимир <br/> `MAN` - Мянтсяля (Финляндия)
Назначение хоста `PURPOSE` | `GENERIC` - обычный Sandbox агент (назначается по-умолчанию) <br/> `SERVER` - хосты `sandbox-server*` <br/> `STORAGE` - хосты `sandbox-storage*` <br/> `BROWSER` - хосты Яндекс.Браузера <br/> `MARKET` - хосты Маркета и т.д.
Технология изоляции процессов `VIRTUAL` | `LXC` - используются Linux Containers <br/> `PORTOD` - используется [Porto](https://github.com/yandex/porto)

## Тип подключения к Интернету { #dns }

Известно, что в Яндексе подавляющее количество хостов не имеет [IPv4](https://en.wikipedia.org/wiki/IPv4)-адреса и являются [IPv6](https://en.wikipedia.org/wiki/IPv6)-only хостами.
Тем не менее в Интернете множество хостов (например, `github.com`) продолжают работать исключительно по IPv4.
Для того чтобы получить доступ к IPv4-сетям, в Яндексе используется технология трансляции IPv4-адресов в IPv6: [NAT64](https://wiki.yandex-team.ru/infrasearch/dns64/).
В Sandbox использование NAT64 настраивается с помощью параметра `dns`:

```python
from sandbox.common.types import misc as ctm
from sandbox import sdk2


class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        dns = ctm.DnsType.DNS64
```

Возможные значения этой настройки:

* `DEFAULT` - Настройки по умолчанию, доступ в Интернет по IPv4 невозможен.
* `DNS64` - Доступ в Интернет по IPv4 возможен, весь резолвинг имён происходит через ферму `ns64-cache.yandex.net`.
* `LOCAL` - Используются настройки из файла `/etc/resolv.conf.local`. Имеет смысл только для кастомных контейнеров, в которых этот файл существует.

Пример ошибки при попытке доступа к IPv4-only хосту без указания требования DNS64:
```
Caused by NewConnectionError('<urllib3.connection.VerifiedHTTPSConnection object at 0x7f9c0cf8bcd0>: Failed to establish a new connection: [Errno 101] Network is unreachable',)
```

Не стоит забывать, что объявленные в коде значения являются значениями по умолчанию.
Если склонировать задачу или запустить задачу на основе планировщика, то требования будут взяты у этого объекта, а не из кода.

Если свойство `dns` должно изменяться, например, в зависимости от входных параметров задачи, то это рекомендуется делать в методе `on_enqueue`.
Для SDK2 модификацию можно делать ещё и в `on_save`.

{% cut "SDK2 on_save" %}
SDK2:
```python
    def on_enqueue(self):
        if self.Parameters.create_ui_resource:
            self.Requirements.dns = ctm.DnsType.DNS64
```
{% endcut %}

[Анонс в Этушке](https://clubs.at.yandex-team.ru/sandbox/2000)

## Запуск на мультислотовых агентах { #multislot }

Для того чтобы задача исполнялась [на мультислотовых агентах](../agents.md#slots), в требованиях необходимо указать ограничения
на количество ядер (`cores`), памяти (`ram`) и добавить блок `Caches`:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        cores = 8
        ram = 8072

        class Caches(sdk2.Requirements.Caches):
            pass  # Do not use any shared caches (required for running on multislot agent)
```

## Привилегированное исполнение { #privileged }

Для запуска задачи [в привилегированном режиме](environment.md#privileged) (пользователем `root`) надо указать требование `privileged = True`.
