# Объявление параметров

У каждого класса задачи может быть два типа [входных параметров](../tasks.md#input-parameters) (стандартные и пользовательские),
а также **[выходные параметры](../tasks.md#output-parameters)**.
Все параметры задаются в классе **Parameters** внутри класса задачи.

## Стандартные входные параметры { #standard-input-parameters }

Стандартные параметры уже [объявлены](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/task.py?rev=r8821078#L224) в Sandbox SDK.
В коде задачи вы можете переопределить значения для некоторых из них:

```python
from sandbox.common.types import task as ctt
from sandbox.common.types import notification as ctn

from sandbox import sdk2


class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        description = "This is my test task description"  # Task description
        max_restarts = 2  # Maximum task restarts
        kill_timeout = 5 * 60  # Task timeout in seconds
        notifications = [  # Notification settings
            sdk2.Notification(
                statuses=[
                    ctt.Status.FAILURE,
                    ctt.Status.EXCEPTION,
                    ctt.Status.TIMEOUT
                ],
                recipients=["my-email@yandex-team.ru"],
                transport=ctn.Transport.EMAIL
            )
        ]
        owner = "QADEV"  # Task owner
        tags = ["adfox", "engine", "rm-main-ticket"]  # Task tags.
        suspend_on_status = [ctt.Status.EXCEPTION]  # Suspend on one of the selected statuses.
```

Ниже – сценарии использования некоторых из них.

### fail_on_any_error { #fail_on_any_error }
```python
fail_on_any_error = True
```
Позволяет переводить задачу в статус FAILURE при любой (даже инфраструктурной) ошибке.
Может быть полезно, чтобы запретить перезапуск задачи.
В таком случае на вкладке History вы увидите сообщение вида `Switched to FAILURE instead of TEMPORARY.` 

### dump_disk_usage { #dump_disk_usage }
```python
dump_disk_usage = False
```
Позволяет отключить сбор статистики использования диска `disk_usage.yaml`, `peak_disk_usage.yaml`.
Может быть полезно, если задача создаёт много файлов (более 100K).

### tcpdump_args { #tcpdump_args }
```python
tcpdump_args = "-v 'host foo.yandex.net'"
```
Позволяет собрать tcp dump.
Может быть полезно для отладки проблем с сетью.

## Пользовательские входные параметры { #custom-input-parameters }

Кроме стандартных входных параметров каждая задача может объявить неограниченное количество пользовательских входных параметров.
Набор входных параметров обычно определяется предметной областью. Примеры того, что может передаваться через такие параметры:

* Ветка, ревизия или версия исходного кода;
* Путь до конфигурационного файла;
* Значение секрета (пароля, секретного ключа или сертификата) из [Секретницы](https://yav.yandex-team.ru/);
* Содержимое файла или каталога, сохраненное в виде [ресурса](../resources.md);

Пример объявления и использования пользовательского входного параметра:

```python
class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        configuration = sdk2.parameters.String("Task configuration", default="", multiline=True)

    def on_execute(self):
        logging.info("Task configuration is %s", self.Parameters.configuration)
```

Полный список возможных типов параметров можно посмотреть [в модуле sandbox.sdk2.parameters](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/parameters.py).

## Выходные параметры { #output-parameters }

Выходные параметры могут быть только пользовательскими и используются следующим образом:

```python
class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        with sdk2.parameters.Output():
            some_result = sdk2.parameters.Float("Task execution result")

    def on_execute(self):
        self.Parameters.some_result = 2.718281828
```

Значение выходного параметра можно менять только один раз за время жизни задачи.
Это обусловлено тем, что на output-параметры могут подписываться и ждать их инициализации другие задачи.

### Сброс значения параметра при перезапуске задачи { #reset-on-restart }

Любая задача может быть перезапущена: например, из-за проблем с физическим сервером и переключения через статус `TEMPORARY` или из-за ручной остановки и последующего повторного запуска. В этом случае output-параметры сохранят свои значения, что может привести к ошибке, если задача попытается выставить значения повторно.

Если в случае перезапуска задачи важно иметь возможность выставить output-параметры повторно, то группу таких параметров надо отметить флагом `reset_on_restart`:
```python
class TaskWithOutputParameters(sdk2.Task):
    class Parameters(sdk2.Parameters):
        with sdk2.parameters.Output:  # same as reset_on_restart=False
            output1 = sdk2.parameters.Integer("Output 1")
        with sdk2.parameters.Output(reset_on_restart=False):
            output2 = sdk2.parameters.Integer("Output 2")
        with sdk2.parameters.Output(reset_on_restart=True):
            output3 = sdk2.parameters.Integer("Output 3")
```


## Управление параметрами

### Числовые и строковые параметры
```python
class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        string_parameter = sdk2.parameters.String("A string parameter", default="default value")
        date = sdk2.parameters.StrictString( # String with regular expression checking
            "Date YYYY-MM-DD",
            regexp="\d{4}-\d{2}-\d{2}",
            required=True,
        )
        integer_parameter = sdk2.parameters.Integer("An integer parameter", default=50)
        float_parameter = sdk2.parameters.Float("A float parameter")
```

### Списки и словари { #lists-and-dicts }

Динамические списковые и словарные параметры (`List`, `Dict`) определяются следующим образом:
```python
...
    class Parameters(sdk2.Task.Parameters):
        list_of_strings = sdk2.parameters.List("Dynamic parameter of type 'List'")
        dict_of_strings = sdk2.parameters.Dict("Dynamic parameter of type 'Dict'")
        with sdk2.parameters.Dict("Dynamic parameter of type 'Dict' with choices") as dict_of_strings_choices:
            dict_of_strings_choices.values[""] = ""  # в этом месте нельзя определять значения по умолчанию
            dict_of_strings_choices.values.SUCCESS = "success"
            dict_of_strings_choices.values.TEMPORARY = "temporary"
            dict_of_strings_choices.values.EXCEPTION = "exception"
            dict_of_strings_choices.values.FAILURE = "failure"
...
```

### Флажки, радио-группы и условное отображение параметров
```python
import logging
from sandbox import sdk2


class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        checkbox = sdk2.parameters.Bool("A checkbox", default=True)

        with sdk2.parameters.RadioGroup("Deployment mode") as mode:
            mode.values["auto"] = mode.Value("Automatic mode")
            mode.values["manual"] = mode.Value("Manual mode", default=True)

        with mode.value["manual"]:  # Show some parameters depending on radio group
            issue = sdk2.parameters.Url("Release issue", required=True)

    def on_execute(self):
        if self.Parameters.checkbox:
            logging.debug("Checkbox enabled")

        if self.Parameters.mode == "manual":
            logging.info("Manual mode")
        else:
            logging.info("Automatic mode")
```

### Скрытие поля в зависимости от значения другого поля { #subfields }

Параметры могут показываться и скрываться в зависимости от значения любого другого параметра.
Для этого не обязательно использовать параметр типа `RadioGroup`.

```python
parameter_selector = sdk2.parameters.String("Subfieldable parameter")
with parameter_selector.value["test"]:
    hidden_parameter_1 = sdk2.parameters.String("Hidden parameter 1")
    hidden_parameter_2 = sdk2.parameters.String("Hidden parameter 2")
```

Внутри кода задачи можно получить список под-параметров для данного параметра в атрибуте sub_fields класса параметра

```python
# вместо self.type можно использовать класс произвольной задачи
assert self.type.Parameters.parameter_selector.sub_fields == {'test': ('hidden_parameter_1', 'hidden_parameter_2')}
```

### Группировка параметров { #groups }

```python
class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):

        with sdk2.parameters.Group("Specific settings", collapse=True) as specific_settings_block:
            release = sdk2.parameters.Bool("Release build", default=False)
            use_robot = sdk2.parameters.Bool("Run with robot", default=True)
```

### Наследование параметров { #inheritance }

Можно добавить еще один параметр в группу параметров, объявленную в другой задаче (**TestTask2** в примере):
```python
class TestTask3(TestTask2):
    class Parameters(TestTask2.Parameters):
        with TestTask2.Parameters.life_block() as life_block:
            new_param = sdk2.parameters.String("New parameter")
            new_param2 = sdk2.parameters.String("New parameter 2")
```

### Доступ к meta-информации о параметрах { #meta }

Пользовательские параметры, адресуемые через класс задачи (`cls.Parameters.my_param`), представляют собой объекты параметров,
со всей мета-информацией: у этого объекта, например, есть поля `default` и `description`.
При обращении к параметрам через экземпляр задачи (`self.Parameters.my_param`) возвращается уже конкретное значение
соответствующего типа (`int`, `str`, `sdk2.Resource` и других).


### Обязательные параметры { #required }

Для того чтобы сделать параметр обязательным, нужно добавить ему атрибут `required`:

```python
class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        required_parameter = sdk2.parameters.String("A string parameter", required=True)
```

{% note warning %}

Свойство required не имеет смысла применять для списковых параметров. (Например, CheckGroup). Поскольку нельзя точно понять какое состояние списка является "не заполненным", поскольку пустой список может быть валидным выбором.

{% endnote %}

### Копирование параметров задачи { #copy-policy }

По умолчанию при копировании задачи все поля, заполненные пользователем, будут скопированы в новую задачу.
Однако, это поведение можно переопределить, установив параметр `do_not_copy=True`:

```python
class Task(sdk2.Task):
    class Parameters(sdk2.Parameters):
        my_param = sdk2.parameters.String("My parameter", do_not_copy=True)
```

### Авто-дополнение строковых параметров в UI { #autocomplete }

При большом количестве вариантов значений параметр `sdk2.parameters.String` принимает форму текстового поля с авто-дополнением:

![Авто-дополнение строкового параметра](img/string_parameter_autocomplete.png "Авто-дополнение строкового параметра")

Если нужно, чтобы данный параметр отображался в виде выпадающего списка без авто-дополнения,
то необходимо принудительно указать ему использовать для отображения элемент интерфейса select:

```python
class Parameters(sdk2.Parameters):
    with sdk2.parameters.String("Yet another name", ui=sdk2.parameters.String.UI("select")) as parameter:
        ...
```

### Переиспользование параметров между sdk2 и sdk1 задачами. { #use-sdk2-params-in-sdk1 }

Переиспользование параметров sdk1 задачи в sdk2 задаче невозможно.
Возможный выход из ситуации - перенести все общие параметры в sdk2 задачу, и сконвертировать их в sdk1 задаче в input_parameters.

Пример переиспользования sdk2-параметров в sdk1 задаче:

```python
from sandbox.sandboxsdk import task
from sandbox.projects.sandbox import test_task_2 # sdk2 task

# some sdk2 parameters are not supported in sdk1
EXCLUDE_PARAMETERS = ["client_tags", "json_parameter"]

class TestTask21(task.SandboxTask):
    Parameters = test_task_2.TestTask2.Parameters
    input_parameters = list(p for p in Parameters if p.name not in EXCLUDE_PARAMETERS)
    def on_execute(self):
        sleep = self.ctx[self.Parameters.live_time.name]
```
