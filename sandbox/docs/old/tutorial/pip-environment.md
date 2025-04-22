*Информация здесь применима только к [классическим задачам](./task-environment.md#python).*

Пакет [commonmark](https://pypi.org/project/commonmark) отсутствует в [sandbox/requirements.txt](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/requirements.txt), а значит в классических Sandbox-задачах он по умолчанию недоступен. Но с помощью класса `PipEnvironment` его можно добавить в виртуальное окружение задачи при её запуске:

```python
import sdk2
from sandbox.sandboxsdk import environments

class Hello%Login%(sdk2.Task):

    class Requirements(sdk2.Task.Requirements):
        environments = [environments.PipEnvironment("commonmark", version="0.9.1")]

    def on_execute(self):
        import commonmark
        ...
```

Пакет установится в статусе PREPARING и будет доступен в коде `on_execute`.

> `PipEnvironment` не имеет никакого эффекта при использовании в [бинарных задачах](./binary-tasks.md).

**Обратите внимание:** импортировать дополнительные пакеты можно только внутри методов. Если вынести его на глобальный уровень, Sandbox не сможет выполнить импорт модуля с задачей в базовом виртуальном окружении, и тесты кода задач сломаются (см. *[Деплой и тестирование задач](./task-deploy.md)*).

```python
import commonmark  # Ошибка! В этой точке пакет ещё не установлен.
from sandbox import sdk2

class TaskClass(sdk2.Task):
    ...
```

**Ограничение:** этот способ допускает только установку новых пакетов, но не изменение существующих. Если ваш пакет, конфликтуя с версиями уже установленных пакетов, попытается обновить или удалить один из них, это приведёт к ошибке. В связи с этим его стоит использовать только лишь для небольших пакетов с минимальными зависимостями (таких как commonmark). Также, крайне рекомендуется фиксировать версии пакетов.

См. подробнее про этот способ в [документации](https://wiki.yandex-team.ru/sandbox/cookbook/#python-libs-task-code).
