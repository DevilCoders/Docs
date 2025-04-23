# Общий код тасклетов фронтенда

В данной папке находится общий код, который может быть использован в тасклетах фронтенда:
- [базовые таски](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/ci/tasklets/common/task)
- [миксины](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/ci/tasklets/common/mixins)
- [менеджеры](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/ci/tasklets/common/managers)
- [утилиты](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/ci/tasklets/common/utils)
- [протобуфы](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/ci/tasklets/common/proto)

## Базовые таски

Большинство тасклетов следует наследовать от одной из базовых тасок. На данный момент существует только [BaseTask](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/ci/tasklets/common/task/base.py), в которой большая часть функциональности приезжает за счет менеджеров.

### BaseTask

Базовая задача общего назначения.

## Миксины

Модули с классами для подмешивания дополнительной функциональности в тасклеты. Используются внутри базовой таски [BaseTask](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/ci/tasklets/common/task/base.py).
Доступные миксины:
- `managers` - добавляет в тасклеты специальные классы с общей функциональностью в виде свойств;
- `prepare_working_copy` - отвечает за подготовку рабочей копии.

## Менеджеры

Менеджеры - классы, содержащие какую-то общую функциональность необходимую для большинства тасклетов. Доступны в тасклетах за счет миксина [ManagersMixin](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/ci/tasklets/common/mixins/managers.py), который наследуется в [BaseTask](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/ci/tasklets/common/task/base.py).

Менеджеры должны быть адресованы какой-то общей функциональности для работы с внешними сервисами/подсистемой/cущностью.

## Утилиты

Вспомогательные утилиты.

## Протобуфы

Список общих protobuf-сообщений, должны быть разделены по сервисам/сущностям: `arc.proto`, `environment.proto` и т.д.

# Общие правила

- если в общем коде (базовой таске, миксине или менеджере) нужно достучаться до каких-то данных из тасклета, то необходимо завести абстрактный метод или свойство. Это позволит Python потребовать объявить метод в момент подключения общего кода (IDE умеет замечать такие проблемы и напоминать об отсутсвующем методе). Пример:
```(python)
import six
from abc import ABCMeta, abstractproperty, abstractmethod


@six.add_metaclass(ABCMeta)
class SomeClass():
    @abstractproperty
    def some_prop(self):
        raise NotImplementedError

    @abstractmethod
    def some_method(self):
        raise NotImplementedError
```
