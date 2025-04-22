# Окружение исполнения задачи

В этом разделе приведены сведения о том, в каком окружении исполняется код задач.

## Операционная система { #operating-system }

Задачи Sandbox могут исполняться на одной из трех поддерживаемых [платформ](../agents.md#platforms):

* **Linux** (Ubuntu)
* **MacOS**
* **Windows**

Выбор требуемой платформы производится при помощи [тегов](requirements.md#tags).
Если нет жесткого требования запускаться на MacOS или Windows, рекомендуется использовать Linux везде, где возможно.

## Сеть { #net }

Задачи имеют IPv6 global адрес и не имеют V4 адреса.
Про сетевые доступы изнутри задачи - [см. раздел firewall](../firewall.md).

## Переменные окружения { #env_vars }

При старте процесса задачи Sandbox формирует для нее список переменных окружения:
```(bash)
	EXECUTABLE: # Путь до executable. Путь до python в случае небинарных или путь до бинарника задачи.
	HOME: /home/sandbox # Путь до домашней директории задачи.
	LANG: en_US.UTF8
	LAUNCHER_CONF: # Служебное поле
	LOGNAME: sandbox # Имя пользователя под которым выполняется задача.
	PATH: /usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin:/Berkanavt/bin/scripts
	PYTHONPATH: /skynet:/:/sandbox:/home/zomb-sandbox/tasks
	SANDBOX_CONFIG: /home/zomb-sandbox/client/sandbox/etc/settings.yaml
	SANDBOX_DIR: /opt/sandbox/db-0/key_0/packs/52e338c47621505d92b12c505d66a38d/sandbox
	SSH_AGENT_PID: 798
	SSH_AUTH_SOCK: /tmp/ssh-jAtUt8sghFuR/agent.797
	SSH_OPTIONS: UserKnownHostsFile=/dev/null,StrictHostKeyChecking=no
	TEMP: /tmp/1327400450 # Переменная окружения указывающая на tmp-директорию которую задача может использовать.
	TMP: /tmp/1327400450 # Переменная окружения указывающая на tmp-директорию которую задача может использовать.
	USER: sandbox # Имя пользователя под которым выполняется задача
	USERNAME: sandbox # Имя пользователя под которым выполняется задача
	YA_CACHE_DIR: /place/sandbox-data/build_cache/ya # Путь до директории с кешами сборки, используется ymake
	container: lxc # Тип контейнеризации
```
Помимо переменных окружения, задаче выставляется ```CWD``` до текущей рабочей директории задачи.
Значения переменных окружения задачи можно посмотреть в [debug.log](../tasks.md#logs)

## Контейнеризация { #containers }

На Linux задачи запускаются в контейнере. Если не указано иное, используется одна из версий дистрибутива [Ubuntu](https://en.wikipedia.org/wiki/Ubuntu).
Поддерживаются [LXC](https://linuxcontainers.org/) и [Porto](https://github.com/yandex/porto) контейнеры.

Образ контейнера, в котором будет запущена задача, скачивается из [ресурса](../resources.md).
Понять, какой конкретно ресурс был использован можно из [логов](../tasks.md#logs) задачи - в файле `debug.log` присутствует вот такая строчка:

```
Switching cgroup to /sysdefault/lxc/1033498921.5/sandbox/executor
```

Здесь `1033498921` — идентификатор [ресурса](https://sandbox.yandex-team.ru/resource/1033498921/view) с образом используемого контейнера.
Пользователь имеет возможность [собрать собственный образ контейнера](#custom-environment), установив все необходимые инструменты и библиотеки.

### Как запускаются контейнеры и процессы задач в нем.
#### LXC
Rootfs lxc-контейнера смонтирована из squashfs образа, сверху монтируется overlayfs для каждого экземпляра контейнера.
Контейнеры для задач без привилегий (запуск не от рута) запускаются один раз и работают до остановки, выполняя много задач.
Контейнеры для задач, требующих root собираются под каждую задачу и разбираются после ее завершения.
Внутри контейнера подменяется файл /etc/rc.conf, и маскируются (выключаются) некоторые сервисы (например, cron).

После создания контейнера агент sandbox'а запускает его в режиме full OS (запускается init процесс и все сервисы).
После старта контейнера клиент sandbox'а готовит [окружение](#env_vars) (env) и кладет его в файл внутри контейнера, а затем
запускает процесс задачи так: ```lxc-attach -n container_name -- /path/to/task_executable```.
После старта задача восстанавливает свое окружение из файла внутри контейнера, после чего выполняет пользовательский код.

Важно отметить, что при таком старте не создается сессия пользователя, а значит скрипты из ```/etc/profile```
не запускаются, поэтому образ контейнера никак не может повлиять на environment/limits процесса задачи.
Единственная возможность передать процессу задачи информацию из образа контейнера - через создание файла на файловой
системе при сборке и вычитывании этого файла во время исполнения.

#### PORTOD
В случае выполнения внутри порто контейнера (тэг PORTOD) созданием и запуском контейнеров занимается демон ```portod```.
Структура контейнеров выглядит примерно так:
```
|-- BASE_SB_CONTAINER (Full OS)
|   |-- Sandbox infra processes (client, agentr, skynet, etc)
|   |-- BASE_TASKS_CONTAINER (Meta)
|   |   |-- TASK_CONTAINER_1 (App mode)
|   |   |-- TASK_CONTAINER_2 (App mode)
|   |   |   |-- SUB_CONTAINER_WITH_TASK (via protoctl exec isolation=false)
|   |   |-- TASK_CONTAINER_N (App mode)
```
Иначе говоря, клиент поддерживает некоторое количество предзапущенных контейнеров, а непосредственно процесс задачи
запускается через ```portoctl exec container_name command="/path/to/task_executable"```, без изоляции от ```TASK_CONTAINER```.

{% note warning %}

В случае, если задача требует запуска от имени пользователя ```root```, то контейнер для нее собирается непосредственно
перед стартом и разбирается после завершения. Во время выполнения задаче доступен portod socket на контейнер и все вложенные.

{% endnote %}

Environment процесса задачи формируется так же, как и на lxc - загружается при старте из заранее подготовленного файла.
Файлы ```/etc/profile, /etc/bash.rc``` и прочие игнорируются, поскольку процесс запускается без создания сессии и работы pam.

### Как задать контейнер в требованиях { #container_requirement }
#### Как задать LXC-контейнер в требованиях { #lxc_container_requirement }
В GUI требование `Container` находится в разделе `Advanced` на странице редактирования задачи.

В коде задачи пользовательский образ подключается с помощью требования `container_resource` указанием конкретного ID:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        container_resource = 1293783910
```

Вместо ID возможно описать фильтр для поиска последнего подходящего ресурса:
```python
from sandbox import sdk2
from sandbox.sdk2.service_resources import LxcContainer

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        container_resource = sdk2.parameters.Container(
            resource_type=LxcContainer,  # LxcContainer - тип по умолчанию и в данном случае может быть опущен
            platform="linux_ubuntu_12.04_precise",  # это платформа по умолчанию, она тоже может быть опущена
            owner="MAPS_GARDEN"
        )
```

Также ресурс с контейнером можно определить в методах `on_create`, `on_save`, `on_enqueue`, найдя нужный ресурс и выставив его ID:

```python
import sandbox.common.types.resource as ctr
from sandbox import sdk2
from sandbox.sdk2.service_resources import LxcContainer

class MyTestTask(sdk2.Task):

    def on_save(self):
        self.Requirements.container_resource = LxcContainer.find(
            state=ctr.State.READY,
            attrs={"released": "stable"}
        ).first().id
```

#### Как задать Porto-слои в требованиях { #porto_layers_requirement }
В GUI сейчас невозможно задать кастомный контейнер в случае Porto.

В коде задачи пользовательский образ подключается с помощью требования `porto_layers` указанием списка Porto-слоёв:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        porto_layers = [2463138505]
```

## Сборка пользовательского окружения задачи { #custom-environment }

Рекомендованным способом получения пользовательского окружения является использование [бинарной сборки кода задач](binary-task.md), но в случае зависимостей, выходящих за пределы пакетов Python, для получения произвольного окружения задачи с любым набором зависимостей и утилит является сборка контейнера с нужным окружением.

{% note warning %}

Сборка контейнеров с пользовательским окружением сейчас доступна только под Linux.

{% endnote %}

Пользовательское окружение задачи можно собирать в виде образа [LXC](#build-lxc-image) или [Porto](#build-porto-image) контейнера.

### Cборка образа LXC контейнера { #build-lxc-image }
1. [Создаем задачу](../tasks.md#launch-task) типа [SANDBOX_LXC_IMAGE](https://sandbox.yandex-team.ru/tasks/?type=SANDBOX_LXC_IMAGE).

2. Указываем тип ресурса, куда будет сохранён образ LXC контейнера, его атрибуты и базовый образ, на основе которого будем собирать собственный образ.

    ![Базовые настройки LXC образа](img/environment-lxc-commands.png "Базовые настройки LXC образа")

3. Указываем репозитории с пакетами и команды, устанавливающие дополнительные библиотеки и утилиты.

    ![Команды для сборки LXC образа](img/environment-lxc-settings.png "Команды для сборки LXC образа")

4. Запускаем задачу и дожидаемся её успешного завершения. В списке ресурсов задачи будет ссылка на созданный образ LXC-контейнера. Если требуется, чтобы образ был доступен бесконечное количество времени, то убедитесь, что соответствующему ресурсу выставлен [атрибут](../resources.md#attributes) `ttl = inf`.

    ![Как посмотреть готовый LXC образ](img/environment-lxc-resource.png "Как посмотреть готовый LXC образ")

### Сборка образа Porto контейнера { #build-porto-image }
1. [Создаем задачу](../tasks.md#launch-task) типа [BUILD_PORTO_LAYER](https://sandbox.yandex-team.ru/tasks/?type=BUILD_PORTO_LAYER).

2. Указываем базовый образ, имя нового образа и скрипт, который нужно выполнить. Скрипт может лежать в едином репозитории или его можно положить на [Yandex.Paste](https://paste.yandex-team.ru/).

    ![Настройки Porto образа](img/environment-porto-settings.png "Настройки Porto образа")

3. Запускаем задачу и дожидаемся её успешного завершения. В списке ресурсов задачи будет ссылка на созданный образ Porto контейнера.

## Привилегированное исполнение { #privileged }

По умолчанию задачи запускаются от непривилегированного пользователя `sandbox`.
Если требуется выполнять действия от имени `root` (например, устанавливать дополнительные пакеты в операционную систему),
этого можно добиться с помощью требования:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        privileged = True
```
Это требование недоступно на ```MULTISLOT``` хостах.

На **MacOS** и **Windows** задачи всегда запускаются от непривилегированного пользователя `sandbox`,
а использование контейнеров с пользовательским окружением не поддерживается.

## Файловая система { #file-system }

У каждой задачи есть директория, в которой разрешено создавать пользовательские данные. Путь такой директории задачи имеет вид `/place/sandbox-data/tasks/9/8/123456789`, где `123456789` - числовой идентификатор задачи. Директория задачи установлена как текущая (cwd) в методе `on_execute`. Переменные окружения `TEMP`, `TMP` и `TMPDIR` указывают на директорию внури `/tmp` которая является bind-mount в директорию `tmp` внутри директории задачи (это не работает для osx и windows. Там переменные окружения указывают в `tmp` внутри директории задачи).

```python
import os
import tempfile
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_execute(self):
        os.getcwd()  # -> "/place/sandbox-data/tasks/9/8/123456789"

        self.path()  # -> Path("/place/sandbox-data/tasks/9/8/123456789")

        self.path("foo", "bar")  # -> Path("/place/sandbox-data/tasks/9/8/123456789/foo/bar")

        tempfile.mkdtemp()  # -> "/tmp/123456789/tmpDzvhUT"
```

{% note alert %}

1. [Требование](requirements.md) `disk_space` распространяется только на директорию задачи. Не рекомендуется записывать файлы в другие директории (например, в `/home/sandbox`). Все директории кроме директории задачи смонтированы на другой раздел, где свободное место сильно ограничено. Если вы запускаете сторонние программы, перенастройте их рабочие директории внутрь директории задачи.

2. Не используйте `/tmp` и `/var/tmp` для временных файлов, используйте директорию из переменной окружения $TEMP

{% endnote %}

## Доступные библиотеки { #libraries }

Код задач в Sandbox написан на [Python](https://python.org/) и имеет доступ к ограниченному набору библиотек:

* Интерпретатор [CPython](https://en.wikipedia.org/wiki/CPython) 2.7.8 из поставки [Skynet](https://wiki.yandex-team.ru/skynet/python/);
* [Код задач](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects);
* Библиотеки Sandbox: [SDK v2](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/),
  [SDK v1](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sandboxsdk),
  [Common](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common);
* [Библиотеки Skynet](https://a.yandex-team.ru/arc/trunk/arcadia/skynet/library);
* Внешние библиотеки, список которых зафиксирован в файле [requirements.txt](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/requirements.txt).

Список внешних библиотек, доступных в Sandbox задачах по умолчанию, небольшой и крайне редко пополняется.
Указанный список библиотек доступен для всех [обработчиков событий](task-life.md) задачи.
В следующих разделах описано, каким образом можно получить в свое распоряжение библиотеку или утилиту, которая недоступна по умолчанию.

{% note warning %}

Вышесказанное не относится к [бинарной сборке кода задач](binary-task.md), при использовании бинарной сборки в задаче доступны все библиотеки из Arcadia, в случае их подключения через `PEERDIR` в `ya.make`

{% endnote %}

### Установка python-библиотек в стандартное окружение { #add-python-library }

Если требуется установить библиотеку, которой нет в списке доступных, то можно указать такие библиотеки в списке требований к задаче:

```python
from sandbox import sdk2
import sandbox.projects.common.environments as env  # See https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/common/environments/__init__.py

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        environments = [env.PipEnvironment("commonmark", version="0.9.1")]

    def on_execute(self):
        import commonmark
        # ...
```

Указанные пакеты устанавливаются, когда задача находится в [состоянии](../tasks.md#status) `PREPARING`.

{% note alert %}

1. Импортировать дополнительные пакеты можно только внутри методов. Если вынести импорт на глобальный уровень, то тесты кода задач сломаются.

    ```python
    import commonmark  # Wrong!
    import sandbox.sdk2 as sdk2

    class MyTestTask(sdk2.Task):

        def on_execute(self):
            import commonmark  # Correct
            # ...
    ```

2. Можно установить только новые пакеты. Нельзя обновить версию существующих пакетов. Если попытаться обновить или удалить один из существующих пакетов, произойдет ошибка.
Этот подход можно использовать для небольших пакетов с минимальным количеством зависимостей. При этом рекомендуется явно фиксировать версии пакетов в коде требований к задаче.

{% endnote %}

### Установка NPM и NodeJS в стандартное окружение { #add-npm-nodejs }

Если требуется использовать NodeJS или NPM, то можно указать какую версию требуется привезти в списке требований к задаче:

```python
from sandbox import sdk2
import sandbox.projects.common.environments as env  # See https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/common/environments/__init__.py

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        environments = [env.SandboxNodeNpmEnvironment('14.18.2')]
```

В этом случае будет доступно консольное исполнение файлов `npm` и `nodejs`

Ещё есть вариант привезти NodeJS через другой env, заодно для билда зависимостей node_modules может потребоваться GCC, получить путь к бинарям можно будет через проперти .node и .npm у этих env

```python
from sandbox import sdk2
from sandbox.sandboxsdk import environments

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        environments = [
            environments.NodeJS('10.14.2'),
            environments.GCCEnvironment(version='5.3.0'),
        ]

    def _get_node_path(self):
        """ Returns path to `node` executable of the prepared environment. """
        return self.Requirements.environments[0].node

    def _get_npm_path(self):
        """ Returns path to `npm` executable of the prepared environment. """
        return self.Requirements.environments[0].npm
```
