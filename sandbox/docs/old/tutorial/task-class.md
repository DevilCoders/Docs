# Тип { #task_type }

Тип задачи формируется из имени её класса путём преобразования из CamelCase в [SCREAMING_SNAKE_CASE](https://en.wikipedia.org/wiki/Snake_case). Имена типов задач в Sandbox должны быть уникальными.
```
HelloWorld => HELLO_WORLD
TestTask2 => TEST_TASK_2
```

{% note "Совет" %}
Функция `ident` позволяет быстро проверить, в какой тип превратится название класса:

```
$ ya py sandbox/common/format
...
In [1]: from sandbox.common.format import ident
In [2]: ident('UploadFileToS3')
Out[2]: 'UPLOAD_FILE_TO_S_3'
```
{% endnote %}

Docstring класса задачи становится описанием её типа и отображается в интерфейсе. 

# Требования и параметры { #requirements_parameters }

Класс Requirements задаёт условия, требуемые для запуска задачи. В частности, наша задача будет запускаться только на клиентах, на которых есть указанное количество RAM и места на диске:
```python
class Requirements(sdk2.Requirements):
    disk_space = 100  # MiB
    ram = 1024  # MiB
    cores = 1

    class Caches(sdk2.Requirements.Caches):
        """ No caches required """
```

Значения `cores` и `Caches` мы обсудим в разделе *[Окружение исполнения задачи](task-environment.md)*.

Класс Parameters задаёт *общие*, *входные* и *выходные* параметры задачи.

**[Общие](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/task.py?rev=5648356#L216-255) параметры** описывают базовые свойства задачи. Для необходимо лишь задать значения по умолчанию (перед запуском их можно будет поменять):
```python
class Parameters(sdk2.Parameters):
    # Common parameters
    kill_timeout = 5 * 60  # seconds
    description = "Create a greeting for someone"
```
В частности, `kill_timeout` задаёт максимальную длительность выполнения задачи на клиенте. При её превышении задача автоматически завершится в статусе TIMEOUT.

**Входные и выходные параметры** определяются самим разработчиком. Доступные типы параметров и их свойства можно найти в модуле [sandbox.sdk2.parameters](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/parameters.py).
```python
class Parameters(sdk2.Parameters):
    ...
    # Input parameters
    login = sdk2.parameters.String("Login of the person you want to greet")
    create_html = sdk2.parameters.Bool("Make HTML version", default=False)
    # Output parameters
    with sdk2.parameters.Output:
        result = sdk2.parameters.Resource(
            "Resource with the greetings", resource_type=Greeting
        )
```

В интерфейсе задачи они отображаются так:

![task parameters](https://jing.yandex-team.ru/files/mkznts/Screenshot%202019-09-15%20at%2017.00.46.png)

При чтении атрибутов классов Parameters и Requirements из кода задачи в них подставятся их фактические значения:

```python
def on_execute(self):
    # Возвращает введённую строку, а не экземпляр класса `sdk2.parameters.String`
    self.Parameters.login  # -> "mkznts"

    self.Requirements.kill_timeout  # -> 300
```

В некоторых случаях этим атрибутам можно присваивать новые значения, см. ниже.

# Этапы жизненного цикла { #on_something }

Логика задачи определяется в методах с приставкой `on_`. Для лучшего их понимания нам придётся ненадолго отвлечься на архитектуру Sandbox.

В Sandbox есть два вида машин:

* *сервер* — хост, обрабатывающий пользовательские API запросы (как напрямую, так и через UI), хранящий базу данных и очередь задач. Сейчас в Sandbox 15 серверов.
* *клиент* — хост, исполняющий пользовательские задачи. Сейчас в Sandbox ~ 4000 клиентов.

Именно на *клиенте* задача проводит основное время. Но ещё *до* попадания на клиент, некоторые из методов класса задачи вызываются на *сервере*:

* `on_create` — при создании задачи
* `on_save` — при изменении задачи в состоянии DRAFT
* `on_enqueue` — *перед* запуском задачи (точнее: постановкой задачи в очередь)

Эти **серверные методы** — вспомогательные, и выполняются синхронно при вызове соответствующих методов API. Очень важно, чтобы они выполнялись максимально быстро и не требовали обращений к сети.

Основное применение таких методов — изменение или валидация требований и параметров перед её выполнением. В методе `on_enqueue` задачи `HELLO_%LOGIN%` выставляется новое описание, чтобы оно соответствовало входному параметру:

```python
def on_enqueue(self):
    self.Parameters.description = (
        "Create a greeting for {}".format(self.Parameters.login)
    )
```

После ожидания в очереди задача назначается на *клиент*, где начинается её фактическое исполнение. Именно здесь, в **клиентских методах** класса задачи, можно активно использовать вычислительные ресурсы, скачивать данные, создавать файлы и т.д.:

* `on_prepare` — последний этап подготовки задачи к исполнению
* `on_execute` — исполнение задачи

Бегло изучите содержание метода `on_execute` в `HELLO_%LOGIN%`. В процессе выполнения задача:

* проверяет, что не выставлен параметр `create_html`, иначе переводит задачу в статус FAILURE с ошибкой (функциональность для этого параметра мы реализуем позже);
* создаёт ресурс, состоящий из одного Markdown-файла с приветствием;
* сохраняет ресурс в выходной параметр задачи.

Не обязательно прямо сейчас вникать в каждую строчку — по ходу руководства мы разберём все эти действия более подробно.
