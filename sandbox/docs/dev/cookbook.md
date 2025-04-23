# Книга рецептов

## Теги задач (Tasks tags) { #task-tags }

Теги задач позволяют разделить задачи широкого профиля на группы. По этим тегам существует индекс в БД, поэтому поиск задач по тегам осуществляется намного быстрее, чем, например, по регулярному выражению описания задач.
Также для тегов постоянно вычисляется частота их использования, что позволяет находить наиболее часто используемые теги в саджесте.

Теги являются common-параметром, поэтому узнать теги можно с помощью `self.Parameters.tags`. Можно изменять этот параметр во время исполнения задачи.

Навесить и снять теги задачи можно в любом её состоянии через UI или REST-запросом.

Тэги задачи не должны быть уникальными для каждой задачи — они должны использоваться для кластеризации множества задач.
Для поиска уникальной задачи нужно использовать входные параметры и/или `hints` (см. раздел ниже)

```python
from sandbox import sdk2

class MyTask(sdk2.Task):
    def on_execute(self):
        my_tags = self.server.task[self.id].read()["tags"]
        assert my_tags == self.Parameters.tags

        self.Parameters.tags = my_tags + ["PARENT_TASK_TAG"]
        child_tasks = self.find()
        for task in child_tasks:
            self.server.task[task.id] = {"tags": my_tags + ["CHILD_TASK_TAG"]}
```

## Индексируемые параметры (hints) { #hints }

Каждая задача может иметь список индексируемых значений, которые автоматически проставляются на основании входных или выходных параметров задачи или вручную.
Поиск по таким значениям быстрее чем поиск по параметрам. Чтобы сделать параметр индексируемым, нужно передать ключ `hint=True`. Используйте метод задачи `self.hint(...)`, чтобы добавить один или несколько хинтов.

```python
from sandbox import sdk2

class MyTask(sdk2.Task):
    class Parameters(sdk2.Parameters):
        input_param = sdk2.Parameters.String("Some input parameter", hint=True)
        with sdk2.parameters.Output:
           output_param = sdk2.Parameters.String("Some output parameter", hint=True)

    def on_execute(self):
        self.hint("test2")
        self.Parameter.output_param = "test3"
```

После выполнения этой задачи со входным параметром `input_param="test1"`, её список хинтов будет `["test1", "test2", "test3"]`.

## Генерация параметров { #parameters_generation }

Иногда декларацию похожих параметров можно существенно сократить с помощью генерации, вот весьма показательное изменение:

[https://a.yandex-team.ru/arc/commit/6152948](https://a.yandex-team.ru/arc/commit/6152948)

Для этого в SDK2 было реализовано несколько нововведений:

* [опциональный параметр при включении внешних параметров `label_substs`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/tests/task.py?rev=6148679#L1152): ожидается `dict`  с подстановками для шаблона в описаниях параметров (используется str.format )
* [вспомогательная функция для динамического определения параметров](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/helpers/misc.py?rev=6148679#L307): определенные таким образом параметры в UI будут всегда находится после статически определенных, но с сохранением порядка в котором определялись. Если хочется их вставить в произвольное место, то можно определить их как внешние и включить в нужное место

## Постановка задачи в очередь { #enqueue_task }

### Приоритет задачи внутри квоты

Для приоритетного выбора сервера для конкретной задачи (не типа, а именно экземпляра задачи) рекомендуется использовать параметр `score`.

Выставить данный параметр можно также, как и любой другой параметр: через API, в декларации параметров или в серверном хуке. Например:

API:

```json
{"type": "TEST_TASK_2", "description": "__", "owner": "MY_GROUP", "score": 5}
```

В параметрах задачи:

```python
import sdk2

class Parameters(sdk2.Parameters):
    score = 5
```

В серверном хуке:

```python
def on_enqueue(self):
    self.Parameters.score = 5
```

Ранжирование с помощью веса, определенного в `score`, происходит после ранжирования по остатку квоты пользователя и базовому приоритету задачи (`SERVICE:HIGH` и другие).
Это означает, что все задачи всех типов одного пользователя с одинаковым базовым приоритетом для заданного хоста будут отсортированы по значению из `score`. По умолчанию значение равно 0.
Так что, если задача имеет в `score` достаточно большой отрицательный вес (-100, например), то она фактически выполнится последней среди всех задач этого пользователя с идентичным базовым приоритетом.

## Выполнение задачи { #task_execution }

### Идентификатор выполняемой задачи { #task_id }

* Если объект задачи доступен в функции, например, это `task`, то идентификатор задачи можно получит как `task.id`
* Если объект задачи не доступен, то можно использовать `sdk2.Task.current.id` (работает для всех типов sdk, но только в клиентских хуках)

### Сохранение состояния задачи { #save_task_state }
Сохранить данные задачи можно в ее контексте – в словаре `self.Context` в SDK2 или `ctx` в SDK1. Данные, записанные в контекст, сохраняются после завершения работы задачи и доступны в веб-интерфейсе на вкладке “Context”. Не рекомендуется сохранять в контекст большие объемы данных (больше единиц мегабайт), так как при сохранении задачи с большим контекстом в базу данных может возникнуть ошибка превышения максимального размера документа. В качестве ключей контекста можно использовать: `int` и `str`. В качестве значений – все базовые типы (`int`, `str`, `list`, `dict`): в sdk2 контекст сохраняется через JSON, из-за чего `tuple` будет сконвертирован в `list`.

Никакие объекты (даже datetime) не могут быть сохранены в контекст, в противном случае будет вызвано исключение и задача перейдет в состояние `EXCEPTION`. Валидация контекста достаточно тривиальная — python-структура, которая сохраняется в контекст, должна сериализоваться без ошибок в `JSON` (вызов `json.dumps`).

### Сохранение в контексте задачи произвольных объектов { #save_objects_in_context }

Как сказано выше, в контекст нельзя сохранить произвольный объект.

Тем не менее это поведение можно имитировать с помощью класса, умеющего хранить состояние в JSON.

{% cut "Пример" %}

```python
import json

from sandbox import sdk2
from sandbox import common


class AttributeDict(common.collections.AttrDict):
  pass


class Serializable(object):
  def __init__(self, **kws):
    for k, v in kws.iteritems():
      setattr(self, k, v)

  def to_json(self):
    return json.dumps(self.__dict__)

  @classmethod
  def from_json(cls, payload):
    return cls(**json.loads(payload))


class Task(sdk2.Task):
  class Context(sdk2.Context):
    serializable = json.dumps(dict(a=1, b=2))
    attrdict = common.collections.AttrDict(c=3, d=4)

  def on_prepare(self):
    self.serializable = Serializable.from_json(self.Context.serializable)

  def on_execute(self):
    assert self.serializable.a == 1 and self.serializable.b == 2
    assert self.Context.attrdict.c == 3 and self.Context.attrdict.d == 4
```

{% endcut %}

### Принудительное завершение задачи с ошибкой { #switch_task_to_exception }

При разных обстоятельствах требуется, чтобы задача завершилась с ошибкой и перешла в правильный статус.

```python
from sandbox import common
# Перевод в статус EXCEPTION
raise common.errors.TaskError("I can't live any longer")
# или просто — при любом необработанном исключении
raise Exception("Something went really wrong")
# альтернатива — перевод в статус FAILURE, из которого задачу не получится перезапустить
raise common.errors.TaskFailure("Go bother someone else")
```

### Использование ssh ключа в задаче { #ssh_key_in_task }

Для использования своего SSH-ключа, например, для доступа к `arcadia.yandex.ru` от имени своего пользователя (робота) нужно сделать следующее:
1. Сгенерировать пару ssh ключей с пустым паролем (passphrase).
2. Приватный ключ положить в [Секретницу](https://yav.yandex-team.ru): нажать на кнопку "создать секрет", в поле "ключ" ввести имя ключа, в поле "значение" скопировать содержимое приватного ключа.
  Публичную часть ключа пользователя (робота) положить на Стафф. Так же поддерживается использование ключей из [Sandbox Vault](https://sandbox.yandex-team.ru/admin/vault), но рекомендуемым сервисом хранения секретов является Секретница.
3. В коде задачи получить приватный ключ из секрета по [этой инструкции](secret.md) и передать его в менеджер контекста [sandbox.sdk2.ssh.Key](https://sandbox.yandex-team.ru/docs/html/sdk2.html#sdk2.ssh.Key) в параметр _private_part_.
  Внутри контекстного менеджера команды смогут использовать новый ssh-ключ.

```python
from sandbox import sdk2

class TaskClass(sdk2.Task):
    class Parameters(sdk2.Parameters):
        private_ssh_key = sdk2.parameters.YavSecret("Yav secret with private ssh key")
    <...>

// использование менеджера контекста
with sdk2.ssh.Key(private_part=private_ssh_key.data()["<имя_ключа_из_секретницы>"]):
    <...>
```

В качестве примера использования с Sandbox Vault можно использовать [задачу TestTask2](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox/test_task_2/__init__.py).


### Монтирование overlay { #mount-overlay }

Монтирование и последующее размонтирование `overlay` можно осуществить с помощью функции из модуля [sandbox.sdk2.os](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/os.py).

Монтирование overlay работает только на linux-серверах при исполнении в контейнерах, в том числе при непривилегированном исполнении (не от имени root).

```python
from sandbox import sdk2
...
        sdk2.os.mount_overlay(mount_point, lower_dirs, upper_dir=upper_dir, work_dir=work_dir)
        # work with mounted directory
        sdk2.os.umount(mount_point)
```

Смонтировать `overlay` можно и без `upper_dir` и `work_dir`. Однако, если определён `upper_dir`, то должен быть определён и `work_dir`.
Аргументы функций соответствуют аргументам команд `mount` и `umount`.


### Монтирование/размонтирование overlayfs из подпроцесса задачи { #mount-overlay-from-subprocess }

Для того чтобы смонтировать overlayfs из подпроцесса задачи, нужно запустить синхрофазатрон с аргументом `mount_overlay`
и передать в stdin json с полями, аналогичными аргументам метода `sdk2.os.mount_overlay`
([пример использования в задаче TEST_TASK_2](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox/test_task_2/__init__.py?rev=7152590#L1119-1124)).

Для размонтирования overlayfs нужно запустить синхрофазатрон с параметрами `umount_overlay {mount_point}`
([пример использования](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox/test_task_2/__init__.py?rev=7152590#L1136-1140)).

Для монтирования squashfs нужно запустить синхрофазатрон с параметрами `mount_image {image_path} {dirname(опционально)}`
([пример использования](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox/test_task_2/__init__.py?rev=7249820#L1002-1008)).

### Создание (регистрация) ресурса из подпроцесса задачи { #resource-registration-from-subprocess }

Новые ресурсы можно создавать из подпроцесса задачи с помощью синхрофазатрона. Путь до него можно найти в `self.synchrophazotron`.
Для этого необходимо запустить скрипт с параметром `-` и передать ему на STDIN метаданные ресурса в следующем формате:
```json
{
    "path": "mydata", // путь до данных ресурса
    "type": "MY_RESOURCE", // тип ресурса
    "description": "abcdefg", // описание ресурса
    "arch": "x86_64", // архитектура процессора или any (опционально)
    "attributes": {"key": "value"} // атрибуты ресурса в виде `key=value` (опционально)
}
```

В случае успешного завершения, код завершения программы будет `0`, на STDOUT будет выведен числовой идентификатор ресурса,
в ином случае код возврата будет отличен от ноля, а вывод программы можно рассматривать как текст ошибки.


### Получить файл по rbtorrent

Чтобы скачать файл скайнетом, можно воспользоваться функцией ([skynet_get](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/share/__init__.py?rev=r8224552#L221))
Пример использования:
```python
import api.copier.errors as copier_errors
import sandbox.common.share as common_share

...
    try:
        common_share.skynet_get(rbtorrent_id, download_path)
    except copier_errors.CopierError as e:
        logging.exception("Cannot download resource with id %s. Exception %s", rbtorrent_id, e)
        raise
```

### Создание существующих ресуров при перезапуске задачи { #creating_resources_on_task_restart }

Если необходимо создавать ресурс на каждый запуск/перезапуск задачи, то создавать ресурсы нужно в методе класса задачи `on_execute`.

Если задача выполняется ещё раз (переходит из статуса **WAIT_TASK**, например),
то при перезапуске метод `on_execute` будет вызван второй раз, и будет создан ещё один ресурс.
Здесь следует помнить о том, чтобы в каждом из ресурсов задачи было зарегистрировано уникальное для задачи имя файла.

Если нужен уникальный ресурс, создаваемый в задаче один раз независимо от количества перезапусков задачи,
то такой ресурс необходимо создавать при помощи контекстного менеджера `memoize_stage`, позволяющего запомнить этап выполнения задачи в методе `on_execute`.


### Номер итерации выполнения задачи { #execution_iteration_number }

Номер итерации выполнения задачи использовав из метода объекта задачи свойство

```python
self.agentr.iteration
```

При первом запуске данной значение равно `0`.

### FQDN хоста и дата-центр клиента, на котором исполняется задача { #task_host_information }

Данная информация записывается в конфигурационный файл клиента в момент его деплоя, получить ее можно следующим образом:

```python
from sandbox import common

dc = common.config.Registry().this.dc
fqdn = common.config.Registry().this.fqdn
```

Дополнительно стоит отметить, что во всех контейнерах хоста конфигурационный файл используется с хост-системы, соответственно, значения будут одинаковы для всех контейнеров.

### Подключение по сети к процессу, запущенному в задаче { #connect_subprocess_from_net }

Для подключения по сети к процессу, запущенному в Sandbox-задаче, необходимо передать подключающейся стороне IP адрес хоста (или, чаще всего, контейнера), где выполняется эта задача. Самый простой способ получить собственный IP-адрес такой:

```python
from sandbox.projects.common import network
addr = network.get_my_ipv6()
```

Так как Sandbox создает контейнеры для задач динамически, у них нет индивидуальных DNS-записей, и, соответственно, подключение к контейнерам по hostname не возможно.

### Выполнение задачи в несколько этапов { #task_execution_by_steps }

В SDK есть контекстный менеджер
  [memoize_stage](https://sandbox.yandex-team.ru/docs/html/sdk2.html?highlight=memoize_stage#sdk2.Task.memoize_stage),
  позволяющий заполнить этап выполнения задачи.
Поскольку при выходе из состояний **WAIT** метод `on_execute()` вызывается повторно, такая функциональность будет полезной,
  когда нужно выполнить разные действия при разных запусках.

Менеджеру можно передать:
* `max_runs` - максимальное количество перезапусков (по умолчанию, `1`)
* `commit_on_entrance` - отметить секцию пройденной при входе в неё (по умолчанию, `True`)
    Использование `commit_on_entrance=False` позволяет считать секцию выполненной только в случае её успешного прохождения
* `commit_on_wait` - отметить секцию пройденной, если она прервалась исключением `sdk2.task.Wait` (по умолчанию, `True`)
    Параметр не влияет на выполнение, если `commit_on_entrance=True`

Пример
```python
 class MyTask(sdk2.Task):
    def on_execute(self):
        with self.memoize_stage.first_step(commit_on_entrance=False):
            logging.info("This is my first run")
            logging.debug("%r", sandboxsdk.svn.Arcadia.info("arcadia:/arc/trunk/arcadia/")))  # this line may raise an exception

        with self.memoize_stage.second_step[:1] as no:
            logging.info("This is my #%d run", no)
            raise sdk2.WaitTime(1)

        with self.memoize_stage["last-step"]:
            logging.info("The last step")
```

Ещё пример

```python
class MyTask(sdk2.Task):
    def on_execute(self):
        with self.memoize_stage.important_action as st:  # executed only once
            assert st.runs == 1

        with self.memoize_stage.important_action(3) as st:  # executed three times
            assert 1 <= st.runs <= 3

        with self.memoize_stage.action2 as st:
            assert st.runs == 1

        with self.memoize_stage['action2'] as st:
            assert st.runs == 1
```

### Монтирование ramdisk в задаче { #ramdrive }

Sandbox поддерживает монтирование дисков в оперативной памяти на базе `tmpfs`. Для этого в коде задачи нужно задекларировать требуемый размер `ramdisk` при помощи следующего кода:
```python
import sandbox.common.types.misc as ctm
from sandbox import sdk2

class MyTask(sdk2.Task):
    class Requirements(sdk2.Requirements):
        ramdrive = ctm.RamDrive(ctm.RamDriveType.TMPFS, 1024, None)  # Декларация ramdisk объемом 1024 Mb
    ...
    def on_execute(self):
        ...
        self.ramdrive.path  # Путь до смонтированного диска
```

В случае, если требуемый размер `ramdisk` зависит от входных параметров задачи, то его можно задекларировать в методе `on_enqueue` класса задачи.
В качестве примера можно использовать [задачу TEST_TASK_2](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox/test_task_2/__init__.py).

Использование ramdisk неявно влияет на список клиентов, где задача может исполняться.
При постановке задачи в очередь будут выбраны только linux-клиенты, у которых объем оперативной памяти больше, чем задекларированный размер `ramdisk + 1 Gb`.

### Управление Turbo boost на хосте { #turbo-boost }

По умолчанию turbo boost включен на всех хостах, где поддерживается.
Однако, у задачи есть возможность выключить его и включить обратно, если необходимо --
для этого надо воспользоваться функциями `disable_turbo_boost` и `enable_turbo_boost` из модуля [sandbox.sdk2.os](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/os.py).

### Использование библиотек из Аркадии в задачах { #arcadia_libraries }

При использовании бинарной сборки задач библиотеки можно подключать по `PEERDIR` к задаче.

### Использование python пакетов в задачах { #use_python_packages_in_task }

По умолчанию код задачи исполняется под Python 2.7.8 (из поставки [Skynet](https://wiki.yandex-team.ru/skynet/)) в [стандартном виртуальном окружении](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/requirements.txt) Sandbox. Если вашей задаче не хватает установленных в нём пакетов, их можно доустановить, либо создать отдельное виртуальное окружение.

#### Для кода задач { #use_python_packages_in_task_for_code }

Чтобы использовать дополнительные пакеты прямо из кода задач, нужно указать их в `Requirements.environments`:

```python
import sdk2
from sandbox.sandboxsdk import environments

class TaskClass(sdk2.Task):

    class Requirements(sdk2.Task.Requirements):
        environments = [
            # List of required packages
            environments.PipEnvironment("yandex-yt", version="0.9.9"),
        ]

    def on_execute(self):
        from yt.wrapper import YtClient
        # ...
```

{% cut "SDK1" %}

```python
from sandbox.sandboxsdk import task, environments

class TaskClass(task.SandboxTask):
    environments = [
        # List of required packages
        environments.PipEnvironment("yandex-yt", version="0.9.9"),
    ]

    def on_execute(self):
        from yt.wrapper import YtClient
        # ...
```

{% endcut %}

По умолчанию пакет будет установлен через pip из внутреннего репозитория [pypi.yandex-team.ru](https://pypi.yandex-team.ru/dashboard/repositories/default/). Можно указать и другие репозитории через параметр `index_url`.

Кроме PyPI, Sandbox умеет устанавливать пакеты из ресурсов с типом `PYTHON_WHEEL`. Можете поискать нужный вам пакет среди [существующих ресурсов](https://sandbox.yandex-team.ru/resources?type=PYTHON_WHEEL). Обращайте внимание на версию и платформу ресурса (атрибуты `version` и `platform`). Если нужный ресурс найден, укажите название пакета и его версию вместе с параметром `use_wheel`, напимер:

```python
PipEnvironment("yandex-yt", version="0.8.46a1", use_wheel=True)
```

Можете также собрать собственный ресурс используя задачу [BUILD_PY_PACKAGE](https://sandbox.yandex-team.ru/tasks?type=BUILD_PY_PACKAGE).

**Важные ограничения**:
* Этот способ допускает только установку //новых// пакетов, но не изменение существующих. Если ваш пакет, конфликтуя с версиями уже установленных пакетов, попытается обновить или удалить один из них, это приведёт к ошибке.
* В этом режиме пакеты устанавливаются непосредственно перед `on_prepare` и доступны только внутри методов `on_prepare` и `on_execute`. Импорт пакетов также необходимо делать только внутри этих методов (как в примере выше), а не на глобальном уровне.

```python
import sdk2
from sandbox.sandboxsdk import environments
from yt.wrapper import YtClient  # Ошибка! `yandex-yt` ещё не установлен

class TaskClass(sdk2.Task):
    class Requirements(sdk2.Task.Requirements):
        environments = [environments.PipEnvironment("yandex-yt")]
```

#### Для внешних скриптов { #use_python_packages_in_task_for_scripts }

Если вы не хотите иметь дело с ограничениями выше, или не хотите завязываться на нашу версию Python, вынесите код, использующий сторонние пакеты, в отдельный скрипт.

Предположим, директория вашей задачи имеет структуру:
```
.
..
__init__.py
script.py
requirements.txt
ya.make
```

Используя класс `VirtualEnvironment`, можно подготовить виртуальное окружения для скрипта прямо из задачи:

```python
import os
import subprocess
from sandbox import sdk2
from sandbox.sandboxsdk import environments

class TaskClass(sdk2.Task):
    def on_execute(self):
        src_dir = os.path.dirname(os.path.realpath(__file__))
        req_path = os.path.join(src_dir, "requirements.txt")
        script_path = os.path.join(src_dir, "script.py")

        with environments.VirtualEnvironment() as venv:
            # Вам *скорее всего* придётся это сделать: почти все пакеты требуют свежих версий
            venv.pip("pip==19.1 setuptools==41.0.1")
            # Установить пакеты из requirements.txt
            venv.pip("-r {}".format(req_path))
            # Запустить скрипт
            with sdk2.helpers.ProcessLog(self, logger="script-log") as pl:
                subprocess.check_call([venv.executable, script_path], stdout=pl.stdout, stderr=pl.stdout)
```

Если же вы не хотите чтобы задача каждый раз тратила время на установку, либо хотите использовать другую версию Python, соберите собственный LXC-контейнер, в котором необходимое окружение уже будет подготовлено.

### Предупреждение о таймауте задачи { #on_before_timeout }
[Раздел переехал](task-life.md#on_before_timeout)

### Обработка исполняющейся задачей собственной остановки { #on_terminate }
[Раздел переехал](task-life.md#on-terminate)

### Ограничение на время исполнения в любом статусе { #task-expiration }

Можно поставить ограничение на время исполнения задачи в любом статусе (включая очередь и WAIT-ы). Для этого существует sdk2 параметр `expires`. Его можно установить либо в определении класса задачи, либо в хуках `on_enqueue`, `on_execute` и т.п.

```python
import datetime as dt
from sandbox import sdk2

class MyTask(sdk2.Task):
    class Parameters(sdk2.Parameters):
        ...
        expires = dt.timedelta(minutes=30)   # можно также использовать int, равный числу секунд

   def on_execute(self):
      # увеличить время ожидания до 60 минут от текущего момента
      self.Parameters.expires = dt.timedelta(minutes=60)  # так же можно присвоить dt.datetime объект
      ...
```

При истечении времени задача переходит в статус `EXPIRED`. Из него задачу можно перезапустить. После перезапуска момент истечения времени устанавливается (текущее_время + последняя дельта, которая была ранее установлена).

### Авторизация в Sandbox API при его использовании в подпроцессах задачи { #task_authorization }

Для авторизации в Sandbox API из подпроцессов задачи можно воспользоваться сессионным токеном задачи, его можно получить следующим образом (для SDK2):
```python
token = self.server.task_token
```

В HTTP-запросе токен необходимо передавать как обычный OAuth-токен, в заголовке `Authorization: OAuth {token}`.

## Работа с подзадачами { #subtasks }
### Ожидание выполнение подзадач { #wait_subtasks }

Пример:
```python
def on_execute(self):
    with self.memoize_stage.create_children:
        subtask_ids = self._create_child_tasks()  # task objects or task ids
        # Save ids to context to process them after waking up
        self.Context.subtask_ids = subtask_ids

        raise sdk2.WaitTask(subtask_ids, ctt.Status.Group.FINISH, wait_all=True)

    self.check_satuses(self.Context.subtask_ids)
```

После того как подзадачи перейдут в ожидаемые статусы, задача будет снова запущена и будет заново выполнен метод `on_execute`.

Внимание: родительская задача может навечно остаться в статусе **WAIT_TASK** если подзадача перейдёт в статус, который не ожидается
(например, для вышеприведённого примера это **EXCEPTION** или **TIMEOUT**).


## Работа с ресурсами { #resources }
### Получение более 3000 ресурсов или задач { #resource-iteration }

В `API` Sandbox существует ограничение на получение списков из более чем `3000` элементов.
Если вам необходимо получить список из большего количества, в первую очередь, подумайте, действительно ли вам это необходимо,
и нельзя ли сократить выборку, задав более строгое условие поиска.
Если это **действительно** так, то нужно воспользоваться страничной адресацией примерно так:
```python
offset = 0
chunk_sz = 1000
while True:
    logging.debug("Requesting items %d-%d...", offset, offset + chunk_sz - 1)
    chunk = list(MY_RESOURCE.find().limit(chunk_sz).offset(offset))
    logging.info("Got items %d-%d...", offset, offset + len(chunk))
    offset += len(chunk)
    if len(chunk) < chunk_sz:
        break
```

### Подготовка дочерней задачей ресурса для родительской задачи { #parent_resource }

Иногда возникает необходимость данные, которые подготавливает дочерняя задача, регистрировать как ресурс родительской задачи,
например, чтобы можно было их удобно зарелизить одним кликом на форме родительской задачи.
Технически это реализуется тем, что родительская задача должна зарегистрировать **NOT_READY** ресурс и передать его ID дочерней задаче,
которая подготовит данные для него и отметит ресурс как **READY**.
Для этого на стороне дочерней задачи надо сконструировать [ResourceData](resources.md#create) для родительского ресурса,
как это делается для обычного ресурса.
Для удобства передачи метаинформации о родительском ресурсе, существует тип входного параметра [ParentResource](https://a.yandex-team.ru/arc_vcs/sandbox/sdk2/parameters.py?rev=r9018502#L270).

Стоит отметить, что для ресурса **NOT_READY** создаются только метаданные. То есть в родительской задаче директория для ресурса сама не создается.


## Post-execution and hooks { #task_hooks }

### Изменение `ttl` ресурса при релизе { #resource-ttl-on-release }

Для того чтобы изменить `ttl` ресурса при релизе, нужно в хуке `on_release` вызвать метод `mark_released_resources`.
Например:

```python
def on_release(self, params):
    super(MyTask, self).on_release(params)
    # Для всех релизящихся ресурсов ставим ttl в 15 дней.
    self.mark_released_resources(params["release_status"], ttl=15)
    # Если надо только для некоторых ресурсов:
    # for resource in resources: ## вместо resources подставить требуемый набор ресурсов
    #    resource.ttl = 15
```

### Автоматический релиз задачи { #auto-release }

Задача не может автоматически себя зарелизить. Для этого нужно использовать либо другую задачу, которая запустит нужную задачу как подзадачу, дождется её выполнения и зарелизит ее,
либо стороннюю систему.
Для автоматизации релизных процессов, можете воспользоваться релизной машиной и использовать готовую функциональность.

Если вам нужна автоматически создавать тикет в Няне при успешном завершении задачи, то можно просто вызвать соответствующий метод,
как это сделано в коде задачи типа [RTC_SLA_TENTACLES_RESOURCE_TGZ_GENERATOR](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/rtc/RtcSlaTentaclesResourceTgzGenerator/__init__.py).

```python
import time
import logging

import sandbox.common.types.task as ctt

from sandbox import sdk2
from sandbox.sdk2.helpers import subprocess as sp

from sandbox.projects.common.nanny import nanny


class RtcSlaTentaclesResourceTgz(sdk2.Resource):
    """ Tar file with current unixtime inside """
    any_arch = True
    auto_backup = False
    executable = False
    releasable = True
    ttl = 3


class RtcSlaTentaclesResourceTgzGenerator(nanny.ReleaseToNannyTask2, sdk2.Task):
    """ Generates tar file with current unixtime inside """

    def on_execute(self):
        # Write current unixtime to file
        with open("sandbox_unixtime.txt", mode='a') as file:
            file.write('%s' % int(time.time()))

        # Archive file
        with sdk2.helpers.ProcessLog(self, logger=logging.getLogger("tar")) as pl:
            sp.Popen("tar -cf RtcSlaTentaclesResourceTgz.tgz sandbox_unixtime.txt", shell=True, stdout=pl.stdout, stderr=sp.STDOUT).wait()

        # Create resource
        sdk2.ResourceData(RtcSlaTentaclesResourceTgz(
            self, "Output file", "RtcSlaTentaclesResourceTgz.tgz"
        ))

    def on_success(self, prev_status):
        sdk2.Task.on_success(self, prev_status)
        nanny.ReleaseToNannyTask2.on_release(self, dict(
            releaser=self.author,
            release_status=ctt.ReleaseStatus.STABLE,
            release_subject="RTC SLA Tentacles unixtime",
            email_notifications=dict(to=[], cc=[]),
            release_comments="RTC SLA Tentacles unixtime",
        ))
```

## Тестирование и коммиты изменений { #tests_and_commits }

### Выполнение задачи с патчем из Аркадии без комита { #tasks_execution_with_arcadia_patch }
#### Ручная сборка архива задач { #build_by_hand }

1. Создайте задачу [BUILD_SANDBOX_TASKS](https://sandbox.yandex-team.ru/tasks?type=BUILD_SANDBOX_TASKS) и предоставьте ей патч. Получится ресурс типа [SANDBOX_TASKS_ARCHIVE](https://sandbox.yandex-team.ru/resources/?type=SANDBOX_TASKS_ARCHIVE), запомните его ID.
2. Создайте свою задачу в статусе **DRAFT**.
3. Укажите ресурс в параметрах `Advanced->Tasks resource`.
4. Запустите свою задачу на выполнение.

## Запуск (выполнение) задачи { #task_starting }
### Запуск задачи по расписанию { #scheduling }

В Sandbox есть [планировщики](https://sandbox.yandex-team.ru/schedulers), для которых можно настроить [регулярный запуск](/sandbox/templates/).

Получить идентификатор планировщика в рантайме можно с помощью атрибута задачи `self.scheduler`. Он принимает отрицательное значение при ручном и положительное при регулярном запуске:
```python
if self.scheduler:
    logging.info(
        "This is a %s run under scheduler #%d",
        "scheduled" if self.scheduler > 0 else "manual",
        abs(self.scheduler)
    )
```

### Профилирование использования процессора задачей { #cpu-profiling }

В Sandbox [можно использовать Google Performance Tools](https://beta.wiki.yandex-team.ru/SergejjGorelov/Profiling/#podderzhkagperftoolsvsandbox)
и входящий туда [CPU Profiler](http://google-perftools.googlecode.com/svn/trunk/doc/cpuprofile.html).

Кроме этого, в Sandbox автоматически собирается статистика использования системных ресурсов при помощи Solomon agent и atop.
Результаты первого можно увидеть в UI на вкладке "Hardware".
Лог atop сохранятся в директории логов задачи под именем `atop.out`.

## Результаты запуска (выполнения) задачи { #tasks_results }
### Дополнительный отчёт в веб-интерфейсе { #tasks_report }

С помощью декоратора `sdk2.report()` на странице задачи можно показать дополнительный отчёт (например, времена исполнения этапов задачи). Он попадёт в отдельную вкладку, либо, если использованы `sdk2.footer()` или `sdk2.header()`, окажется снизу или сверху на странице. Все подробности о работе с декораторам и отчётами можно прочитать на [отдельной странице](https://wiki.yandex-team.ru/sandbox/tasks/report).

### Профилирование использования диска задачей { #disk_profiling }

В Sandbox есть возможность узнать, сколько дисковых ресурсов использовала задач в процессе исполнения, —  поле "Used disk space" на странице задачи. Пока что нет возможности узнать, на что именно было потрачено место, но в целом у задачи есть три источника данных:

– кэши: `arcadia` и прочие `vcs`, `arcadia_tests_data`, программы из `environments`;
– синхронизируемые (скачанные на клиент) ресурсы при помощи метода `channel.sync_resource()` или `sdk2.ResourceData()`;
– созданные объекты в локальной директории задачи на клиенте.

Расчет значения поля "Used disk space" именно так и происходит: каждые 30 секунд запускается df и считает, на сколько уменьшилось свободное место. Если задача запускалась несколько раз, то берется максимальное значение для всех запусков.
При завершении задачи подробная информация об использованном месте на диске сохраняется в лог задачи под именем `disk_usage.yaml`

Для облегчения профилирования на задачу можно навешивать [пользовательские теги](https://wiki.yandex-team.ru/sandbox/cookbook/#user-tags-on-clients) и затем использовать их для фильтрации (см. ниже)

## Дедупликация при создании задач { #deduplication }

Если возникает необходимость исключить создание задач определенного типа и с одинаковыми параметрами (либо с внешним определением эквивалентности), то можно воспользоваться функциональностью дедупликации задач. Для этого достаточно при [создании задачи](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#!/task/task_list_post) передать в параметре uniqueness словарь с двумя ключами:
* **key** (обязательный) - ключ уникальности; если передать пустую строку, то ключ посчитается автоматически на основе всех параметров задачи
* **excluded_statuses** (необязательный) - список статусов (групп статусов); задачи в этих статусах не будут учитываться при проверке уникальности, значение по-умолчанию ["DELETE"]

Примеры:

**REST API**:
```python
from sandbox import common
api = common.rest.Client()

# external unique key
task1_1 = api.task(type="TEST_TASK_2", uniqueness=dict(key="1234567890"))
task1_2 = api.task(type="TEST_TASK_2", uniqueness=dict(key="1234567890", excluded_statuses=["DELETE"]))
task1_3 = api.task(type="TEST_TASK_2", uniqueness=dict(key="1234567890", excluded_statuses=["DELETE", "DRAFT"]))
task1_4 = api.task(type="TEST_TASK_2", description="Different description", uniqueness=dict(key="1234567890"))
assert task1_1["id"] == task1_2["id"]
assert task1_3["id"] != task1_2["id"]
assert task1_4["id"] == task1_3["id"]

# auto unique key
task2_1 = api.task(type="TEST_TASK_2", uniqueness=dict(key=""))
task2_2 = api.task(type="TEST_TASK_2", uniqueness=dict(key="", excluded_statuses=["DELETE"]))
task2_3 = api.task(type="TEST_TASK_2", uniqueness=dict(key="", excluded_statuses=["DELETE", "DRAFT"]))
task2_4 = api.task(type="TEST_TASK_2", description="Different description", uniqueness=dict(key=""))
assert task2_1["id"] != task1_2["id"]
assert task2_1["id"] != task1_3["id"]
assert task2_1["id"] == task2_2["id"]
assert task2_3["id"] != task2_2["id"]
assert task2_4["id"] != task2_1["id"]
assert task2_4["id"] != task2_2["id"]
assert task2_4["id"] != task2_3["id"]
```

Также, можно использовать уже настроенный (авторизованный сессией задачи, выставлены таймауты и т.д.) `rest.Client` из задачи, который доступен как `self.server`. Например:
```python
task1_1 = self.server.task(type="TEST_TASK_2", uniqueness=dict(key="1234567890"))
```


**SDK2**:
```python
import sandbox.common.types.task as ctt
from sandbox import sdk2

T = sdk2.Task["TEST_TASK_2"]

# external unique key
task1_1 = T(None, uniqueness=dict(key="1234567890"))
task1_2 = T(None, uniqueness=dict(key="1234567890", excluded_statuses=[ctt.Status.Group.DELETE]))
task1_3 = T(None, uniqueness=dict(key="1234567890", excluded_statuses=[ctt.Status.Group.DELETE, ctt.Status.DRAFT]))
task1_4 = T(None, description="Different description", uniqueness=dict(key="1234567890"))
assert task1_1 is task1_2
assert task1_3 is not task1_2
assert task1_4 is task1_3

# auto unique key
task2_1 = T(None, uniqueness=dict(key=""))
task2_2 = T(None, uniqueness=dict(key="", excluded_statuses=[ctt.Status.Group.DELETE]))
task2_3 = T(None, uniqueness=dict(key="", excluded_statuses=[ctt.Status.Group.DELETE, ctt.Status.DRAFT]))
task2_4 = T(None, description="Different description", uniqueness=dict(key=""))
assert task2_1 is not task1_2
assert task2_1 is not task1_3
assert task2_1 is task2_2
assert task2_3 is not task2_2
assert task2_4 is not task2_1
assert task2_4 is not task2_2
assert task2_4 is not task2_3
```

## Разное { #misc }
### Сборка цели в Аркадии { #buildi_arcadia_target }

1. Использовать задачу `YA_MAKE_2` с флагом `Use arcadia-api fuse`.
2. Воспользоваться ArcadiaAPI внутри задачи:

```python
from sandbox import sdk2

from sandbox.projects.common.arcadia import sdk as arcadiasdk
from sandbox.projects.common.constants import constants as sdk_constants

def build(target, revision, output_directory, patch=None):
    with arcadiasdk.mount_arc_path("@".join((sdk2.svn.Arcadia.ARCADIA_TRUNK_URL, revision))) as aarcadia:
        if patch:
            path_to_patch = sdk2.svn.Arcadia.apply_patch(aarcadia, patch, task.path())
            if patch.startswith("arc:"):
                # When applying (arc:review-id) use zipatch  downloaded from Arcanum
                patch = path_to_patch
        arcadiasdk.do_build(
            build_system=sdk_constants.DISTBUILD_BUILD_SYSTEM,
            source_root=aarcadia,
            targets=[target],
            results_dir=output_directory,
            patch=patch
            clear_build=False,
        )
```

### Использование GCC/GDB/PIP/venv/etc в задаче { #environments_in_task }

В Sandbox нас есть некоторое количество описанных окружений, которые можно использовать в задачах:
  * pip
  * gcc
  * gdb
  * clang
  * virtualenv
  * svn
  * dolbilka
  * yandex.tank

Полный список можно найти [в документации](https://sandbox.yandex-team.ru/docs/html/sandboxsdk.html#module-sandboxsdk.environments)
(окружения, написанные авторами задач, [расположены отдельно](https://sandbox.yandex-team.ru/docs/html/projects.common.html#module-projects.common.environments)).
Если какого-то окружения не хватает, то можно добавить его самому или запросить реализацию у команды разработчиков Sandbox.
Прежде чем начать полезную работу клиент смотрит на требования задачи, подготавливает соответствующее окружение и только после этого начинает выполнение непосредственно полезной работы.

### Запуск Yandex.Tank внутри задачи в Sandbox { #tank }

Основная информация (в какую сторону копать) – в посте [«Про танки в Sandbox»](https://clubs.at.yandex-team.ru/tanks/965).
По вопросам использования Танка в Sandbox можно общаться с разработчиками  `Yandex.Tank` (рассылка load@).

Поскольку Sandbox может стать плохо, если много людей будет стрелять по сети, генерируя сотни тысяч RPS,
мы поощряем стрельбы в локальные инстансы ваших приложений и строго не рекомендуем стрелять с хостов Sandbox по сети.

### Сборка контейнера с окружением, в котором будет исполняться задача { #task_container }
Чтобы использовать собственный образа контейнера, нужно:
1. [Собрать контейнер](environment.md#custom-environment)
2. [Использовать его в требованиях к задаче](environment.md#container_requirement)

### Добавить кастомные логи в список логов на странице задачи { #custom_logs }

В шапке страницы задачи в виде ссылок отображаются все ресурсы задачи типов `TASK_LOGS` и `TASK_CUSTOM_LOGS`.
Первый тип ресурсов регистрируются автоматически системой, второй можно зарегистрировать из кода задачи.

### Доступ к IPv4 адресам и DNS64/NAT64 { #dns }
[Раздел переехал](requirements.md#dns)

### Получение диапазона гарантированно свободных портов { #free_ports }

Попробуйте использовать диапазон `15000..25000`, он не занят нашими сервисами и должен быть свободным.
Для получения случайного свободного порта используйте метод `get_free_port` из py23-модуля `sandbox.projects.common.network`.

Очень грубо для истории:
```
10000 - 15000  - Скайнет/Копир и наши сервисы
30000 +/- 100 - Самогон
32000 - 65000 - ОС для исходящих подключений
```
