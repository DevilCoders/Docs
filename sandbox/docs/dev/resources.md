# Использование ресурсов

Ранее мы уже подробно [останавливались](../resources.md) на том, что такое ресурс. В этом разделе мы разберёмся с особенностями работы с ресурсами из кода задач.

## Объявление нового типа ресурса в коде { #new-type }

Задача может использовать ресурсы уже существующих типов или объявить собственный тип.
Чтобы объявить новый тип ресурса, нужно создать и добавить в репозиторий его класс:

```python
from sandbox import sdk2

class SignedData(sdk2.Resource):
    """ A directory with signature """
```

Этот класс можно [положить в файл с кодом задачи](basics.md#source-code) или в отдельный каталог.
Для того чтобы новый тип ресурса стал известен API-серверам, требуется чтобы класс ресурса был объявлен или проимпортирован **в каком-нибудь из `__init__.py` модулей** одной из библиотек,
подключенной при помощи PEERDIR (возможно, транзитивно) к корневой библиотеке `sandbox/projects`.
После вливания изменений в trunk Аркадии и прохождения всех тестов новый тип ресурса станет доступен в Sandbox.

Аналогично задачам, имя типа ресурса получается преобразованием имени класса: `SignedData -> SIGNED_DATA`.


## Метаданные ресурса { #metadata }

У каждого ресурса, как и у задачи, есть набор полей, содержащих метаданные.
Некоторые из доступных полей приведен в таблице:

Поле | Описание
:--- | :---
accessed | Время последнего доступа к ресурсу
arch | Архитектура данных, хранящихся в ресурсе
created | Время создания ресурса
description | Описание ресурса
expires | Время, когда ресурс будет удален
http_proxy | HTTP-ссылка на скачивание данных ресурса
id | Числовой идентификатор ресурса
md5 | [MD5](https://en.wikipedia.org/wiki/MD5) сумма данных ресурса
owner | Владелец ресурса
path | Путь, по которому хранятся данные
rights | Права доступа текущего пользователя на обновление ресурса
size | Полный размер данных ресурса
skynet_id | Идентификатор ресурса в системе Skynet (rbtorrent)
state | [Состояние](../resources.md#status) ресурса
task | Объект задачи, создавшей ресурс (содержит её метаданные)
task_id | Числовой идентификатор задачи, создавшей ресурс
type | Тип ресурса
updated | Время последнего обновления ресурса
url | URL для просмотра ресурса в графическом интерфейсе Sandbox

Полный список полей можно посмотреть в описании базового класса – [sandbox.sdk2.resource.Resource](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/resource.py?rev=r8249147#L62).

## Атрибуты ресурсов { #attributes }

У ресурса есть набор [стандартных атрибутов](../resources.md#attributes), определяющих как долго он хранится, происходит ли создание резервной копии и так далее. Аналогично тому, как у задачи можно определить [пользовательские входные и выходные параметры](parameters.md), у любого ресурса можно определить пользовательские атрибуты:

```python
from sandbox import sdk2

class SignedData(sdk2.Resource):

    signature = sdk2.resource.Attributes.String("Data signature")
```

В отличие от параметров задач атрибуты ресурсов могут быть только одного из четырёх скалярных типов: `String`, `Bool`, `Integer` и `Float`.

## Поиск и чтение данных ресурса { #search-and-download }

Существует несколько способов прочитать данные из ресурса.

**Способ 1. Получение ресурса по его идентификатору.**

```python
import logging
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_execute(self):
        resource_id = 1110614779
        resource = sdk2.Resource[resource_id]
        data = sdk2.ResourceData(resource)
        path = data.path  # See https://docs.python.org/dev/library/pathlib.html
        logging.info("Resource %d downloaded to %s", resource_id, path)
```

При обращении к ресурсу он автоматически скачивается и сохраняется в кэше на хосте исполняющем задачу.
В поле `path` содержится абсолютный путь до файла или корневого каталога, сохраненного в ресурсе.
Прочитать содержимое файла или список файлов в каталоге можно стандартными средствами Python.

**Способ 2. Поиск ресурса по его типу.**

Использование числовых идентификаторов ресурса прямо в коде не рекомендуется, т.к. любое изменение ресурса потребует изменения кода задачи.
Более правильным считается поиск ресурса по типу и атрибутам:

```python
import logging
from sandbox.common import errors
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_execute(self):
        binary_resource = sdk2.Resource.find(
            type="SOME_BINARY",
            attrs={"released": "stable"}
        ).first()

        if not binary_resource:
            raise errors.TaskFailure("Could not find binary")

        data = sdk2.ResourceData(binary_resource)
        path = data.path
        logging.info("Using binary %s from resource = %s created by %s", path, binary_resource.id, binary_resource.task_id)
```

Вместо указания типа ресурса в виде строки можно использовать его класс:

```python
from sandbox import sdk2

class PlainTextData(sdk2.Resource):
    """ Plain text data """

class MyTestTask(sdk2.Task):

    def on_execute(self):
        resource = PlainTextData.find(
            attrs={"released": "stable"}
        ).first()
```

**Способ 3. Использование ресурса из параметра задачи.**

Sandbox позволяет указывать ресурс в качестве параметра задачи.
В этом случае при запуске задачи можно явно переопределить какой ресурс следует использовать в конкретном запуске.

```python
import json
import logging
from sandbox import sdk2

class JSONData(sdk2.Resource):
    """ JSON data """

class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        json_data_resource = sdk2.parameters.Resource('JSON data', resource_type=JSONData, required=True)

    def on_execute(self):
        if not self.Parameters.json_data_resource:
            data_path = str(sdk2.ResourceData(self.Parameters.json_data_resource).path / "data.json")
            with open(data_path) as json_config_data:
                json_config = json.load(json_config_data)
                logging.info("Loaded JSON from %s: %s", data_path, json_config)
```

Если требуется загрузить последний [релиз](releases.md) ресурса:

```python
from sandbox import sdk2

class JSONData(sdk2.Resource):
    """ JSON data """

class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        json_data_resource = sdk2.parameters.LastReleasedResource('JSON data', resource_type=JSONData, required=True)
```

## Создание ресурса с данными { #create }

Для того чтобы записать данные в ресурс, нужно создать экземпляр класса ресурса в коде задачи.
В конструкторе класса указывается описание ресурса, а также название файла или корневого каталога.

```python
from sandbox import sdk2

class PlainTextData(sdk2.Resource):
    """ Plain text data """

class MyTestTask(sdk2.Task):

    def on_execute(self):
        resource = PlainTextData(self, "Resource description", "filename.txt")
        resource.path.write_bytes("Hello world!")
```

Можно записать в ресурс каталог с файлами и выставить его атрибуты:

```python
from sandbox import sdk2

class SignedData(sdk2.Resource):

    signature = sdk2.resource.Attributes.String("Data signature")

class MyTestTask(sdk2.Task):

    def on_execute(self):
        resource = SignedData(self, "A directory with signature", "root_dir")
        resource.signature = "ba1f2511fc30423bdbb183fe33f3dd0f"

        data = sdk2.ResourceData(resource)
        data.path.mkdir(0o755, parents=True, exist_ok=True)
        data.path.joinpath("filename.txt").write_bytes("Hello, world!")

        data.ready()  # Set resource status to READY
```
