# Tasks

> `Task` используется для оформления некоторого действия уровня логики приложения, которое необходимо вынести из `action` и выполнить асинхронно. Поэтому `Task` включена в перечень базовых сущностей (`entities`) приложения.

Важными атрибутами задачи являются:
- тип (`task_type`)
- принимаемые на вход параметры (`task_params`)
- состояние (`task_state`)

*Тип задачи определяет код, который будет выполнен.* Это значит, что за каждым типом задачи закреплен соответствующий WorkerAction, содержащий логику обработки задач заданного типа. За счет этого обеспечивается слабая связанность между постановкой задачи и ее выполнением. С точки зрения высокоуровневой логики постановка задачки &mdash; это создание и сохранение в базе экземпляра `Task` в состоянии PENDING, с соответствующими типом и параметрами. Впоследствии эту задачку обнаружит и подберет обработчик задач соответствующего типа.

Во время создания задачи ее параметры оформляются в виде экземпляра класса, производного от `TaskParams` (либо в виде совместимого по атрибутам словаря). Класс параметров фиксирует интерфейс между постановкой задачи и выполнением задачи. *Тип задачи определяет принимаемые параметры* &mdash; во время выполнения задачи в соответствии с её типом должны ожидаться исключительно те параметры, что описаны в соответствующем классе параметров.
``

# BaseActionWorker

Для упрощения организации асинхронных задачек предлагается использовать следующий подход.
В классе Action определяем вспомогательные атрибуты, позволяющие создавать экземпляры Task на запуск Action.
```python
from dataclasses import dataclass
from payments.core.actions.base.action import BaseAction
from payments.core.exceptions import CoreInteractionError

class StartMerchantModerationAction(BaseAction):
    name = 'some_action'
    async_params = ('merchant_uid',)
    retry_exceptions = (CoreInteractionError,)

    @dataclass
    class Params:
        merchant_uid: int

    async def handle(self):
        ...

```

В приложении воркеров должен быть BaseActionWorker, в список обработки которого следует добавить новый Action:
```python
from payments.taskq.workers.base import ActionWorker

class SomeWorker(ActionWorker):
    actions = (..., StartMerchantModerationAction)

```

При соблюдении данных условий, можно создавать задачи, используя метод на базовом классе `BaseAction`
```python
StartMerchantModerationAction.run_async(
    storage=...,
    action_kwargs={'merchant_uid': 1},
    max_retries=2
)
```
Впоследствии воркер подберет задачу.

Метакласс `ActionMeta` следит за уникальностью атрибута `name` на наследниках `BaseAction` (только на тех, которые определяют такой атрибут как строку, т. е. которые хочется отправлять воркерам). Важно, чтобы для всех воркеров была единая точка запуска (модуль), благодаря чему все используемые определения Actions будут собраны в одном месте и метакласс ActionMeta сможет гарантировать уникальность `name` на уровне приложения.
