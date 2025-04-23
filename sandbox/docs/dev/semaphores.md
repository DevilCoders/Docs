# Семафоры

Как мы уже выяснили [ранее](../semaphores.md), семафоры нужны для ограничения максимального числа параллельно исполняющихся задач. Одна задача может использовать несколько семафоров одновременно. Использование семафора объявляется в [требованиях задачи](requirements.md):

```python
from sandbox import sdk2
import sandbox.common.types.task as ctt

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        semaphores = ctt.Semaphores(
            acquires=[
                ctt.Semaphores.Acquire(name='my_semaphore_name')
            ]
        )
```

По-умолчанию семафор автоматически освобождается (release) при переходе задачи в одно из следующих [состояний](../tasks.md#status):

* EXCEPTION
* EXPIRED
* FAILURE
* NO_RES
* STOPPED
* SUCCESS
* TIMEOUT
* WAIT_*

Можно явно задать **вес задачи** (т.е. насколько увеличить [значение семафора](../semaphores.md#value)) и конкретные состояния, когда семафоры освобождаются:

```python
from sandbox import sdk2
import sandbox.common.types.task as ctt

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        semaphores = ctt.Semaphores(
            acquires=[
                ctt.Semaphores.Acquire(
                    name='my_semaphore_name',
                    weight=5  # Default weight is 1
                )
            ],
            release=(ctt.Status.Group.BREAK, ctt.Status.Group.FINISH)
        )
```

При попытке захватить несуществующий семафор, задача переходит в состояние **EXCEPTION**. Если нужно создавать новый семафор автоматически каждый раз при запуске серии задач, нужно указать параметр `capacity`:

```python
from sandbox import sdk2
import sandbox.common.types.task as ctt

class MyTestTask(sdk2.Task):

    class Requirements(sdk2.Requirements):
        semaphores = ctt.Semaphores(
            acquires=[
                ctt.Semaphores.Acquire(
                    name='my_semaphore_name',
                    weight=2,
                    capacity=10
                )
            ],
            release=(ctt.Status.Group.BREAK, ctt.Status.Group.FINISH)
        )
```

Освободить используемые семафоры из кода задачи явно можно так:

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_execute(self):
        sdk2.Requirements.semaphores.release()
```
