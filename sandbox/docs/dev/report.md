# Отчёты

{% note warning %}

Отчёты можно создавать только в задачах, использующих SDK v2.

{% endnote %}

Sandbox предоставляет возможности добавления на страницу задачи произвольного HTML.
Например, можно добавить отчёт о прохождении тестов, информацию о покрытии кода, ссылку на внешнюю систему и так далее.

## Отчёт наверху страницы задачи { #header }

Будет расположен под заголовком `Custom header`:
![Размещение отчёта наверху страницы](img/reports-header.png "Размещение отчёта наверху страницы")


Такой отчёт создаётся с помощью декоратора **@sdk2.header()**:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        name = sdk2.parameters.String("Your name", default="")

    @sdk2.header(title="Greeting")  # Title will be printed instead of "Custom header"
    def header(self):
        if self.Parameters.name:
            return "<h1>Hello, {}!</h1>".format(self.Parameters.name)
        else:
            return "<h1>Hello!</h1>"
```

## Отчеты в теле задачи

При выполнении задачи можно отправлять кастомные отчеты, которые будут показываться на странице задачи в ее теле. Для этого используется метод задачи `self.set_info`, принимающий параметры:
1. `info` - сообщение, которое нужно добавить в отчет. Может быть в html стиле.
2. `do_escape` - экранирует символы сообщения. По умолчанию `True`. Если вам нужно сделать именно html отчет, то передайте в этот параметр значение `False`.


## Отчёт внизу страницы задачи { #footer }

Будет расположен под заголовком `Custom footer`:
![Размещение отчёта внизу страницы](img/reports-footer.png "Размещение отчёта внизу страницы")

Создаётся с помощью декоратора **@sdk2.footer()**:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    @sdk2.footer(title="Report URL")  # Title will be printed instead of "Custom footer"
    def on_execute(self): # It's allowed to decorate event handlers too
        return '<a href="https://report.yandex-team.ru/{}">'.format(self.id)
```

## Отчёт на отдельной странице { #separate-page }

![Размещение отчёта на отдельной странице](img/reports-report.png "Размещение отчёта на отдельной странице")

Создаётся с помощью декоратора **@sdk2.report()**:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    @sdk2.report(title="First report", label="first")  # Title field is used a tab name on task page
    def first_report(self):
        return "<b>One</b>"

    @sdk2.report(title="Second report", label="second")
    def second_report(self):
        return "<b>One</b>"
```

## Особенности работы { #restrictions }

### Server-side исполнение { #server-side }

Вызовы методов создания отчётов, происходят на сервере Sandbox каждый раз при загрузке соответствующей страницы.
Важно, чтобы все подобные методы отрабатывали быстро. Любая задержка в работе подобных методов может привести к замедлению загрузки страницы задачи.
Это же означает, что можно отображать разные данные в зависимости от значений полей задачи.

### Использование шаблонов { #templates }

Для отображения сложного HTML можно использовать шаблонизатор [Jinja](https://jinja.palletsprojects.com/) (доступен в [окружении задач](environment.md)):

```python
from jinja2 import Environment, BaseLoader
from sandbox import sdk2

template_string = """<h3>Numbers</h3>
{% if numbers is defined %}
<ul>
{% for item in numbers %}
  <li>{‎{ item }‎}</li>
{% endfor %}
</ul>
{% else %}
List is empty
{% endif %}"""

class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        numbers = sdk2.parameters.List("Selected numbers", required=True)

    @sdk2.footer()
    def footer(self):
        template = Environment(loader=BaseLoader).from_string(template_string)
        return template.render({
            "numbers": self.Parameters.numbers,
        })
```


### Ограничения на теги { #xss }

Отчёты – это данные, которые создаются нашими пользователями.
По этой причине все отчёты, а также описание (description) задачи, фильтруются в нашем UI.
В отчёте нельзя использовать внешний HTML в теге **iframe**, а также скрипты. Подобные конструкции автоматически удаляются на стороне UI с целью борьбы с XSS-атаками.
