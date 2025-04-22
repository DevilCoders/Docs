# Дочерние задачи и процессы

Sandbox умеет запускать дочерние задачи и процессы.

## Дочерние задачи { #subtasks }

### Создание подзадач { #create }

Sandbox позволяет организовать [иерархию задач](../tasks.md#hierarchy).
При этом задача запускает вложенные задачи и позволяет дождаться их завершения.
Чтобы **создать дочернюю задачу** нужно создать инстанс класса задачи.
Дальше можно либо сразу запустить задачу (метод `enqueue`), либо сохранить её как черновик (метод `save`).
В некоторых случаях может потребоваться остановить вложенную задачу явно. Для этого используется метод `stop`:

```python
import logging
from sandbox import sdk2


class MyTestSubtask(sdk2.Task):

    def on_execute(self):
        logging.info('Hello from subtask')


class MyTestTask(sdk2.Task):

    def on_execute(self):
        child = MyTestSubtask(
            self,
            description="Child of {}".format(self.id),
            owner=self.owner,  # Owner is required
        )
        child.save()  # Only save as DRAFT
        child.enqueue()  # Save and enqueue
        # ...
        child.stop()  # Explicitly stop
```

### Установка системных требований { #set-requirements }

Задавать требования можно передачей требований в виде словаря в конструктор задачи,
или последующей модификацией соответствующих полей класса Requirements.
```python
    sub_task = MyTestSubtask(
        self,
        description="Child of {}".format(self.id),
        owner=self.owner,
        __requirements__={
            "tasks_resource": tasks_resource,
            "client_tags": "WINDOWS",
        },
    )
    sub_task.Requirements.disk_space = 8 << 10  # in MiB, 8 GiB
    sub_task.Requirements.ram = 4 << 10  # in MiB, 4 GiB
    sub_task.save().enqueue()  # it is important to save task after modification of requirements and before calling enqueue().
```

Также задать требования задачи можно с помощью запроса [PUT /task/\<id\>](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#!/task/task_put):
```python
    # set up requirements
    requirements = {
        "disk_space": 8 << 30,  # in bytes, 8 GiB
        "ram": 4 << 30,         # in bytes, 4 GiB
    }
    sdk2.Task.server.task[sub_task.id].update({"requirements": requirements})

    # start task (with class object or via API)
    sub_task.enqueue()
```

### Переход в ожидание { #wait }
Если задача хочет завершить своё исполнение, подождать завершения каких-то задач (возможно, дочерних) и после этого
опять исполнить стадию `on_execute`, то нужно воспользоваться специальным исключением `sdk2.WaitTask`:

```python
from sandbox import sdk2
import sandbox.common.types.task as ctt


class MyTestTask(sdk2.Task):

    def _run_child_tasks(self):
        """ returns list of created sub tasks """

    def on_execute(self):
        sub_tasks = self._run_child_tasks()
        raise sdk2.WaitTask(sub_tasks, ctt.Status.Group.FINISH, wait_all=True)
```

При этом задача может быть настроена на повторный запуск не только после выполнения других задачи, но и после истечения
заданного времени:
```python
    # task is going to wait <wait_time> seconds
    raise sdk2.WaitTime(wait_time)
    # task will be in status WAIT_TASK until any of sub tasks finished
    raise sdk2.WaitTask(subtasks, ctt.Status.Group.FINISH, wait_all=False)
    # task will be in status WAIT_TASK until all of sub tasks finished or 5 minutes are elapsed
    raise sdk2.WaitTask(subtasks, ctt.Status.Group.FINISH, wait_all=True, timeout=300)
```
После того как желаемое событие произойдёт, задача будет переключена в статус ENQUEUED и начнёт своё исполнение заново.
Код задач должен это учитывать, чтобы не выполнить те же самые действия повторно.


Также задача может ожидать установку выходных параметров другой задачи. Для этого используется исключение `sdk2.WaitOutput`.
В это случае задача на время ожидания переходит в специальный статус `WAIT_OUT`.

```python
    targets = {task1_id: "output_field1", task2_id: ("output_field1", "output_field2")}
    raise sdk2.WaitOutput(targets, wait_all=True, timeout=360)
```

### Поиск задач { #find }
Искать задачи можно по-разному.

Поиск по статусу:
```python
    # find all tasks in statuses EXCEPTION, STOPPED of type TEST_TASK ordered by ascending id
    tasks = sdk2.Task.find(TestTask, status=(ctt.Status.EXCEPTION, ctt.Status.STOPPED)).order(sdk2.Task.id).limit(42)

    # find all tasks in statuses EXCEPTION, STOPPED of type TEST_TASK ordered by descending id
    tasks = sdk2.Task.find(TestTask, status=(ctt.Status.EXCEPTION, ctt.Status.STOPPED)).order(-sdk2.Task.id).limit(42)
    # or
    tasks = TestTask.find(status=(ctt.Status.EXCEPTION, ctt.Status.STOPPED)).order(-sdk2.Task.id).limit(42)

    # find first task or None if not exists
    task = TestTask.find(status=(ctt.Status.EXCEPTION, ctt.Status.STOPPED)).order(-sdk2.Task.id).first()
```

Поиск по входным параметрам:
```python
    # find all tasks with param_name1=param_value1 and param_name2=param_value2
    tasks = sdk2.Task.find(TestTask, input_parameters={'param_name1': param_value1, 'param_name2': param_value2}).limit(42)

    # find all tasks with either param_name1=param_value1 or param_name2=param_value2
    tasks = sdk2.Task.find(TestTask, input_parameters={'param_name1': param_value1, 'param_name2': param_value2}, any_params=True).limit(42)
```

Поиск по выходным параметрам задачи:
```python
   sdk2.Task[2464].Parameters.output_parameter
   >> u'something'

   TestTask2.find(output_parameters=dict(output_parameter="something")).first()
   >> TestTask2:2464
```

## Дочерние процессы { #subprocesses }

Для запуска вложенных процессов (т.е. команд) следует использовать встроенные [средства Python](https://docs.python.org/3/library/subprocess.html).
Для того чтобы перенаправить стандартный поток вывода (`stdout`) и ошибок (`stderr`) в файл внутри директории с логами задачи,
можно воспользоваться контекстным менеджером `sdk2.helpers.ProcessLog`:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_execute(self):
        with sdk2.helpers.ProcessLog(self, logger="shell") as pl:
            sdk2.helpers.subprocess.check_call(
                ["echo", "Hello, world!"],
                stdout=pl.stdout, stderr=pl.stderr,
            )
```

В этом коде мы вначале объявляем лог-файл с именем `shell`, а затем перенаправляем вывод команды `echo 'Hello, world!'` в этот файл.
Разовый запуск команды реализован функцией [check_call](https://docs.python.org/3/library/subprocess.html#subprocess.check_call) из стандартной библиотеки Python.

Также логи можно перенаправить и в стандартные логи задачи (`debug.log` и `common.log`):

```python
...
from sandbox.sdk2.helpers import subprocess as sp
...
    with sdk2.helpers.ProcessLog(self, logger=logging.getLogger("du_h")) as pl:
        sp.Popen(["du", "-h"], stdout=pl.stdout, stderr=sp.STDOUT).wait()
```

Запуск подпроцесса с логированием стандартного вывода в отдельный файл и в строковый буфер, с ограничением времени выполнения:
```python
    with sdk2.helpers.ProcessLog(self, logger="synchrophazotron"):
        dependent_resource_path = sdk2.path.Path(sp.check_output(
            [str(self.path("synchrophazotron")), str(resource_id)],
            timeout=3600,
        ))
```

### Сбор корок (coredump) { #coredumps }

Для автоматического сбора coredump процеccа, его нужно запустить в контекстном менеджере `sdk2.helpers.ProcessRegistry`.

```python
    with sdk2.helpers.ProcessRegistry as reg:
        proc1 = sp.Popen(command_line, ...)  # Popen регистрирует процессы автоматически
        reg.register(pid2, command_line2)  # используйте метод register чтобы зарегистрировать произвольный процесс

```

После стадии execute задачи, все coredump-ы, оставшиеся от зарегистрированных процессов, оформляются как ресурсы.
Также для них генерируются gdb-трейсбэки.
