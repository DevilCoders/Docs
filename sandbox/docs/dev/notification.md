# Уведомления

## Уведомления о статусах
Sandbox умеет сообщать через почту, Telegram, Q и Juggler о том, что задача перешла в некоторый статус.
Для каждой задачи можно настроить несколько правил такого оповещения.

Каждое правило содержит:
* статусы, при переходе в которые необходимо отправить уведомление:
  поддерживаются как отдельные статусы, (например `EXCEPTION`), так и группы статусов (например `BREAK`)
* канал уведомления: `email`, `telegram`, `q` или `juggler`
* список получателей: логины сотрудников, Sandbox-группы, рассылки (рассылки только для email уведомлений) и др.
* статус проверки: `OK`, `WARN` или `CRIT` (только для Juggler уведомлений)


### Настройка правил уведомлений

Настроить правила можно несколькими способами

#### Через Web-интерфейс
В интерфейсе при редактировании полей задачи в секции «Notifications settings»
  можно указать четыре типа нотификаций: Telegram, Q, Email или Juggler
![Пример](img/notification_example.png "Пример уведомления")

#### При создании задачи через API
Через соответствующее поле в [методе создания задачи](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#/task/task_list_post):
```python
from sandbox import common

common.rest.Client().task.create(
    type='TEST_TASK_2',
    notifications=[{
        'recipients': ['yasandbot'],
        'statuses': ['BREAK', 'FAILURE'],
        'transport': 'telegram'
    }]
)
```

#### При создании задачи через SDK2
Через соответствующее поле в конструкторе задачи:
```python
from sandbox import sdk2
from sandbox.common.types import task as ctt
from sandbox.common.types import notification as ctn

task_class = sdk2.Task["TEST_TASK_2"]
task_class(
    None,
    notifications=sdk2.Notification(
        statuses=[ctt.Status.WAIT_TASK, ctt.Status.Group.FINISH],
        recipients=["robot-sandbox"],
        transport=ctn.Transport.EMAIL,
    )
)
```

#### Обновить уведомления у планировщика
Через соответствующее поле в [методе обновления планировщика](http://sandbox.yandex-team.ru/media/swagger-ui/index.html#/scheduler/scheduler_put)

Для статусов задачи:
```python
from sandbox import common

common.rest.Client().scheduler[scheduler_id].update(
    task={
        "notifications": [{
            'recipients': ['yasandbot'],
            'statuses': ['BREAK', 'FAILURE'],
            'transport': 'telegram'
        }]
    }
)
```

Для статусов планировщика:
```python
from sandbox import common

common.rest.Client().scheduler[scheduler_id].update(
    scheduler_notifications=[{
        'recipients': ['yasandbot'],
        'statuses': ['FAILURE', 'STOPPED'],
        'transport': 'telegram'
    }]
)
```

### Управление нотификациями
С точки зрения SDK2, правила уведомлений содержатся в параметре `self.Parameters.notifications`. Через него можно:

* Устанавливать правила по умолчанию
  ```python
  from sandbox import sdk2
  from sandbox.common.types import task as ctt
  from sandbox.common.types import notification as ctn

  class TaskClass(sdk2.Task):
      class Parameters(sdk2.Parameters):
          notifications = [
              sdk2.Notification(
                  [ctt.Status.FAILURE, ctt.Status.Group.BREAK],
                  ["robot-sandbox"],
                  ctn.Transport.EMAIL
              )
          ]
  ```

* Настраивать уведомления динамически при сохранении задачи
  ```python
  from sandbox import sdk2
  from sandbox.common.types import task as ctt
  from sandbox.common.types import notification as ctn

  def on_save(self):
      super(TaskClass, self).on_save()
      already_notified = any(
          n.recipients == ["robot-sandbox"]
          for n in self.Parameters.notifications
      )
      if not already_notified:
          self.Parameters.notifications += [
              sdk2.Notification(
                  [ctt.Status.FAILURE, ctt.Status.Group.BREAK],
                  ["robot-sandbox"],
                  ctn.Transport.EMAIL
              ),
          ]
  ```

По умолчанию, если не настраивать правила явно, автору задачи придут уведомления о переходе задачи
в [один из финальных статусов](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/yasandbox/controller/task.py?rev=4665011#L1882).


## Отслеживание запущенной задачи
Для этого нужно Телеграм-боту [yasandbot@](https://t.me/yasandbot)
или пользователю `robot-sandbox` в MessengerQ отправить сообщение вида `/track task_id status1 status2`,
где `task_id` - id отслеживаемой задачи,
а `status1`, `status2`, ... - статусы, для которых нужно отослать уведомления
(можно не указать ни одного, в этом случае будет применен набор по умолчанию).

***С помощью этой функциональности нельзя отследить переход задачи в релизные статусы.***


## Отправка произвольных уведомлений

Для произвольных уведомлений можно использовать запрос к REST API
[/notification](https://sandbox.yandex-team.ru/media/swagger-ui/#!/notification/notification_create).

В SDK2 задачах для этого используется `self.server.notification`,
в SDK1 вместо `self.server` нужно использовать `sandbox.common.rest.Client()`

### Email

```python
self.server.notification(
    subject="sandbox notification",
    body="notification body",
    recipients=["sandbox-noreply"],
    transport=common.types.notification.Transport.EMAIL,
    urgent=True  # send mail from sandbox-urgent@ instead of sandbox-noreply@
)
```

* В `recipients` можно указывать как логины, так и полные адреса (с `@yandex-team.ru`).
* В случае, если размер письма превысит 10000 килобайт
  (стандартное ограничение `postfix` на размер отправляемых писем), его содержимое будет вырезано

### Telegram
```python
self.server.notification(
    body="notification body",
    recipients=["<telegram-login>"],
    transport=common.types.notification.Transport.TELEGRAM
)
```

* В качестве получателей нужно указать Телеграм-логины сотрудников
* Сообщения придут только тем, кто зарегистрировался в боте [yasandbot@](https://t.me/yasandbot).
  Для регистрации в боте необходимо отправить ему сообщение. Телеграм-логин пользователя должен быть добавлен на staff.
* Для уведомления в чат нужно:
  * Добавить бота [yasandbot@](https://t.me/yasandbot) в чат
  * Убедиться, что в чате есть сиб бот `TashaNaturalBot` с правами админа
  * Указать в настройках sandbox группы через REST API
    [/group](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#/group/group_put)
    в `telegram_chat_id` id телеграм чата
  * Указать в качестве получателя уведомления Sandbox-группу с привязанным id телеграмм чата.
    Если `telegram_chat_id` не привязан к группе, то уведомления будут отправлены каждому члену группы,
    подписанному на бота [yasandbot@](https://t.me/yasandbot), лично
  * Данный способ не работает, если Телеграм-чат является [супергруппой](https://st.yandex-team.ru/DEVTOOLSSUPPORT-7710#60cc787e688ce6439a26acc9).

Получатель при отправке сообщения по Telegram-уведомлению разворачивается в следующем порядке:
  группа, яндекс-логин, телеграм-логин.
1. Если получатель - группа, то уведомление придет в чат группы или лично каждому пользователю из группы.
2. Если группы нет, будет искаться пользователь с таким логином.
3. Если и пользователя нет, бот попробует отправить уведомление, считая, что указан телеграм логин.
   Если при этом получатель ни разу не общался с ботом, уведомление будет проигнорировано.

### Q
```python
self.server.notification(
    body="notification body",
    recipients=["login"],
    transport=common.types.notification.Transport.Q
)
```

При отправке любых сообщений в MessengerQ нужно подписаться на `robot-sandbox` бота.
Для отправки личным сообщением нужно отправить боту сообщение `/sandbox_subscribe_user`.
Для отправки сообщения группе нужно добавить бота в ваш чат
и присвоить группе `messenger_chat_id` равный `chat_id` чата, в которого вы добавили бота.
Пока последнее можно сделать только через [api группы](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#/group/group_put).
Например, так:
```python
import requests
ret = requests.put(
    "https://sandbox.yandex-team.ru/api/v1.0/group/GROUP_NAME",
    json={
        "messenger_chat_id": "CHAT_ID"
    },
    headers={"Authorization": "OAuth XXXX"}
)
```

### Juggler

```python
self.server.notification(
    body="notification body",
    recipients=["host=USER_HOST&service=USER_SERVICE"],
    transport=common.types.notification.Transport.JUGGLER,
    check_status=common.types.notification.JugglerStatus.OK,
    juggler_tags=["tag"],
)
```

* Получателем в juggler может быть проверка `host={user.host}&service={user_service}` или Sandbox-группа:
  * Если получателем является juggler-проверка, то вместо `{user.host}` нужно подставить host проверки,
    а вместо `{user_service}` сервис проверки.
    Формат получателя соответствует формату запроса на поиск проверки в juggler.
  * Если получателем является группа, то для нее нужно сконфигурировать настройки juggler через
    API метод [/group](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#/group/group_put) в `juggler_settings`.
    Поле `сhecks` – JSON, ключом которого может быть
      `task_status_changed` (настройка проверки для изменения статуса задач) или
      `scheduler_status_changed` (настройка проверки для изменения статуса планировщика).
    Каждая проверка является JSON с полями `host` и `service`.
    Если в проверке не указан `host` или `service`,
    то подставляются значения из полей `default_host` и `default_service` соответственно.
    Пример настройки:
    ```json
    {
      "juggler_settings": {
        "checks": {
          "task_status_changed": {
            "host": "test.host1",
            "service": "test_service"
          },
          "scheduler_status_changed": {
            "host": "test.host2",
            "service": "test_service"
          }
        }
      }
    }
    ```
    или то же самое
    ```json
    {
      "juggler_settings": {
        "checks": {
          "task_status_changed": {
            "host": "test.host1"
          },
          "scheduler_status_changed": {
            "host": "test.host2"
          }
        },
        "default_service": "test_service"
      }
    }
    ```
* Поле `check_status` должно иметь одно из трех значений: `OK`, `CRIT` или `WARN`
* Можно передавать произвольные тэги в поле `juggler_tags`: [документация Juggler](https://docs.yandex-team.ru/juggler/raw_events)


{% cut "Пример настройки задачи, для которой при падениях в проверку будут отправляться `CRIT`, а при успешном завершении `OK`" %}

```python
class TaskClass(sdk2.Task):
    class Parameters(sdk2.Parameters):
        notifications = [
            sdk2.Notification(
                [ctt.Status.FAILURE, ctt.Status.Group.BREAK],
                ["host=test.host&service=test_service"],
                ctn.Transport.JUGGLER,
                check_status=ctn.JugglerStatus.CRIT
            ),
            sdk2.Notification(
                [ctt.Status.SUCCESS],
                ["host=test.host&service=test_service"],
                ctn.Transport.JUGGLER,
                check_status=ctn.JugglerStatus.OK
            )
        ]
```

{% endcut %}

## Примеры задач с настроенными уведомлениями

```python
import logging
from sandbox import sdk2
from sandbox.common.types import task as ctt
from sandbox.common.types import notification as ctn

class BaseParameters(sdk2.Task.Parameters):
    notifications = [
        # send messages about workflow events
        sdk2.Notification(
            [
                ctt.Status.ENQUEUED,
                ctt.Status.Group.FINISH,
                ctt.Status.Group.BREAK,
            ],
            ["ИМЯ ВАШЕЙ РАССЫЛКИ"],
            ctn.Transport.EMAIL
        ),
        # send messages about bad events
        sdk2.Notification(
            [
                ctt.Status.NOT_RELEASED,
                ctt.Status.FAILURE,
                ctt.Status.EXCEPTION,
                ctt.Status.NO_RES,
                ctt.Status.TIMEOUT,
                ctt.Status.STOPPED,
                ctt.Status.EXPIRED,
            ],
            ["ДРУГОЕ ИМЯ ВАШЕЙ РАССЫЛКИ"],
            ctn.Transport.EMAIL
        ),
        sdk2.Notification(
            [
                ctt.Status.FAILURE,
                ctt.Status.EXCEPTION,
                ctt.Status.NO_RES,
                ctt.Status.TIMEOUT,
                ctt.Status.EXPIRED,
            ],
            ["ИМЯ ГРУППЫ ИЛИ ПРОВЕРКИ"],
            ctn.Transport.JUGGLER,
            check_status=ctn.JugglerStatus.CRIT
        ),
        sdk2.Notification(
            [
                ctt.Status.SUCCESS
            ],
            ["ИМЯ ГРУППЫ ИЛИ ПРОВЕРКИ"],
            ctn.Transport.JUGGLER,
            check_status=ctn.JugglerStatus.OK
        ),
    ]

class BaseTask(sdk2.Task):
    def on_create(self):
        # remove notification list from children tasks
        if self.parent is not None:
            self.Parameters.notifications = None
```

По умолчанию Sandbox отправляет автору задачи на электронную почту уведомление о переходе задачи в одно из следующих
[состояний](../tasks.md#status): `EXCEPTION`, `EXPIRED`, `FAILURE`, `NO_RES`, `SUCCESS`, `TIMEOUT`.
Это поведение можно переопределить, задав новое значение [стандартного параметра](parameters.md#standard-input-parameters) `notifications`:

```python
from sandbox.common.types import task as ctt
from sandbox.common.types import notification as ctn

from sandbox import sdk2


class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        notifications = [  # Notification settings
            sdk2.Notification(
                statuses=[
                    ctt.Status.FAILURE,
                    ctt.Status.EXCEPTION,
                    ctt.Status.TIMEOUT
                ],
                recipients=["my-email@yandex-team.ru"],
                transport=ctn.Transport.EMAIL
            ),
            sdk2.Notification(
                statuses=[
                    ctt.Status.FAILURE
                ],
                recipients=["awacs-alerts", "prettyboy"],  # Telegram user names list
                transport=ctn.Transport.TELEGRAM
            ),
            sdk2.Notification(
                statuses=[
                    ctt.Status.SUCCESS
                ],
                recipients=["robot-sandbox"],
                transport=ctn.Transport.Q
            )
        ]
```

Если требуется определять настройки уведомлений во время исполнения задачи, то это можно сделать в [методе](task-life.md#server-side) `on_save`:

```python
from sandbox import sdk2
import sandbox.common.types.task as ctt
import sandbox.common.types.notification as ctn

class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        notify = sdk2.parameters.Bool("Send notifications")

    def on_save(self):
        super(MyTestTask, self).on_save()
        if self.Parameters.notify:
            self.Parameters.notifications += [
                sdk2.Notification(
                    statuses=[ctt.Status.FAILURE, ctt.Status.Group.BREAK],
                    recipients=["robot-selenium"],
                    transport=ctn.Transport.EMAIL
                ),
            ]
```

Аналогичным образом можно передавать настройки уведомлений для [вложенных задач](subtask.md):

```python
from sandbox import sdk2
import sandbox.common.types.task as ctt
import sandbox.common.types.notification as ctn

class MyTestSubtask(sdk2.Task):

    def on_execute(self):
        """ Test subtask """

class MyTestTask(sdk2.Task):

    def on_execute(self):
        child = MyTestSubtask(
            self,
            owner=self.owner,
            notifications=[
                sdk2.Notification(
                   statuses=[ctt.Status.FAILURE],
                   recipients=["my-email@yandex-team.ru"],
                   transport=ctn.Transport.EMAIL
               )
            ],
        )
        child.enqueue()
```

Задача может отправлять уведомления с произвольным текстом в произвольный момент времени:

```python
from sandbox import sdk2
import sandbox.common.types.notification as ctn

class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        recipients = sdk2.parameters.List('Notification recipients', required=True)

    def on_execute(self):
        self._email_notification("Email notification text")
        self._telegram_notification("Telegram notification text")
        self._q_notification("Q notification text")
        self._juggler_notification("Juggler notification text")

    def _email_notification(self, text):
        self.server.notification(
            subject='Email notification subject',
            body=text,
            recipients=self.Parameters.recipients,
            transport=ctn.Transport.EMAIL,
            urgent=True, # Send mail from sandbox-urgent@ instead of sandbox-noreply@
        )

    def _telegram_notification(self, text):
        self.server.notification(
            body=text,
            recipients=self.Parameters.recipients,
            transport=ctn.Transport.TELEGRAM,
        )

    def _q_notification(self, text):
        self.server.notification(
            body=text,
            recipients=self.Parameters.recipients,
            transport=ctn.Transport.Q,
        )

    def _juggler_notification(self, text):
        self.server.notification(
            body=text,
            recipients=self.Parameters.recipients,
            transport=ctn.Transport.JUGGLER,
            check_status=ctn.JugglerStatus.OK
        )
```
