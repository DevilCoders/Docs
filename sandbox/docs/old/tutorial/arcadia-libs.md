*Информация здесь применима только к [бинарным задачам](./binary-tasks.md).*

В бинарных задачах можно использовать любые библиотеки из Аркадии совместимые с Python 2. Для этого их нужно перечислить в секции PEERDIR файла `ya.make` модуля с задачей:

```plain
# sandbox/projects/hello_%login%/ya.make

SANDBOX_PY23_TASK(hello)
OWNER(%login%)

PEERDIR(
    contrib/python/commonmark  # новая зависимость
    sandbox/projects/tutorial/common
)
```

Пересоберите задачу, запустите её командой `run`, и убедитесь, что `commonmark` в коде задачи импортируется и работает:

```
def on_execute(self):
    import commonmark
    ...
```

**Обратите внимание:** даже модули бинарных задач должно быть импортируемы в [базовом виртуальном окружении](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/requirements.txt). Все внешние зависимости (всё кроме `sandbox.*`) следует импортировать внутри методов, иначе есть риск сломать тесты кода задач (см. *[Деплой и тестирование задач](./task-deploy.md)*).

```python
import commonmark  # Ошибка!
from sandbox import sdk2

class TaskClass(sdk2.Task):
    ...
```

{% note "Примечание" %}
Строго говоря, вы можете выносить на глобальный уровень импорты пакетов из базового виртуального окружения. Но перенос *всех* внешних импортов в методы повышает консистентность кода и уменьшает вероятность ошибиться в том, какие именно пакеты можно импортировать.
{% endnote %}

Подробнее про Python-сборку и библиотеки в Аркадии читайте в [документации](https://wiki.yandex-team.ru/arcadia/python/pysrcs/).
