# Релизы

## Общее описание { #abstract }

В Sandbox существует возможность релизить задачи и их ресурсы.
По умолчанию в процессе релиза выполняется ряд действий: ответственным людям отправляется письмо с оповещением о релизе,
ресурсы задачи отмечаются как релизнутые (им выставляется атрибут `released=<release-type>`, а также `ttl=inf`),
а также совершаются другие действия, описанные в методе `on_release()` задачи.

Выполняемые при релизе действия описываются в коде задачи, при этом обычно релиз выполняется ради переключения статуса ресурсов,
связанных с задачей.
Например, вы можете создать ресурс, содержащий протестированные версии каких-то программ или образов виртуальных машин,
а затем использовать эти протестированные файлы в других задачах.
В этом случае в тот момент, когда ресурсы будут готовы к использованию повсеместно, а их корректность не будет вызывать опасения,
можно выполнить релиз. Процесс релиза запускается нажатием кнопки **Release** на странице завершившейся задачи:

![Кнопка запуска релиза](img/releases-button.png "Кнопка запуска релиза")

{% note info %}

Предполагается, что запуск релиза на странице задачи — это **ручное действие**, типа постановки штампа "проверено" или "тестируется".
Если какое-то действие требуется выполнять автоматически после успешного или неуспешного завершения задачи, то
правильнее разместить это действие в коде методов `on_success` или `on_failure`.

{% endnote %}

## ACL { #acl }

Релиз может запустить сотрудник или группа, вписанные в [атрибут](../resources.md#attributes) `releasers` класса каждого ресурса,
которые были созданы задачей.

```python
from sandbox import sdk2

class PlainTextData(sdk2.Resource):
    releasers = ["QADEV", "prettyboy"]
    release_subscribers = releasers + ["vania-pooh"]
    releasable = True

```

{% note info %}

Атрибуты `releasers` и `releasable` должны быть выставлен хотя бы у одного типа ресурса из созданных задачей.
Иначе кнопка **Release** будет недоступна.

{% endnote %}

## on_release

Действия, происходящие при нажатии кнопки **Release**, описываются в обработчике `on_release` в коде задачи:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_release(self, parameters):
        """ Executed when task release was submitted """
```

По умолчанию метод `on_release` берёт все ресурсы со свойством `releasable = True` в классе и созданные задачей.
Каждому такому ресурсу выставляется два [атрибута](../resources.md#attributes):

1. **released** (`cancelled`, `prestable`, `testing`, `stable`, `unstable`) - означает стабильность данных, хранящихся в ресурсе.
2. **ttl** - период хранения ресурса.
    По умолчанию ресурсам при релизе выставляется `ttl=inf`, т.е. они хранятся бесконечно.
    Если требуется, чтобы эти ресурсы хранились ограниченное время, а потом автоматически удалялись, можно переопределить `ttl` в методе `on_release`:

    ```python
    from sandbox import sdk2

    class MyTestTask(sdk2.Task):

        def on_release(self, parameters):
            super(MyTestTask, self).on_release(parameters)
            self.mark_released_resources(parameters["release_status"], ttl=15)  # 15 days
    ```

В конце релиза пользователям, указанным в атрибуте `release_subscribers`, отправляется письмо о выполнении релиза.

Суммарно на выполнение метода `on_release` выделяется 5 минут.
В случае успешного завершения метода за это время задача переходит в [состояние](../tasks.md#status) **RELEASED**.
В случае возникновения любой ошибки в процессе выполнения задача переходит в состояние **NOT_RELEASED**.
Задачи можно отправить в релиз повторно. Количество релизов задач не ограничено. Для каждого релиза сохраняются логи выполнения.

![Задача в состоянии RELEASED](img/releases-successful.png "Задача в состоянии RELEASED")

После перехода задачи в состояние **RELEASED** можно использовать созданные ей ресурсы в коде других задач,
находя последний релиз через атрибуты:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_execute(self):
        binary_resource = sdk2.Resource.find(
            type="PLAIN_TEXT_DATA",
            attrs={"released": "stable"}
        ).first()
```

## Управление шаблоном и допустимыми статусами релиза { #release-template }

Sandbox позволяет более тонко настроить поведение при выполнении релиза, переопределив свойство `release_template` задачи:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    @property
    def release_template(self):
        return sdk2.ReleaseTemplate(
            ["qa-dev@yandex-team.ru"],  # Also send release emails to these addresses
            "Task {} has been released.".format(self.id),  # Email subject
            "This is to confirm that task {} has been released.".format(self.id),  # Email body
            ["testing", "prestable", "stable"]  # Allowed release types
        )
```

## Одна задача релизит другую { #external }
Если требуется начать процесс релиза другой задачи, то это можно сделать вызовом API [POST /release](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#/release/release_list_post):

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_execute(self):
        self.server.release(task_id=123456789)
```
