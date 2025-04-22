# Основные идеи

В предыдущем разделе вы ознакомились с процедурой создания новой задачи в Sandbox с нуля. В этом разделе приведены базовые сведения, связанные с разработкой задач.

## Организация кода { #source-code }

* Исходный код всех задач хранятся в каталоге [sandbox/projects](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects) репозитория.
  Внутри этого каталога каждая команда создает свой подкаталог и уже туда складывает код задач.
* Каждая задача – это отдельный каталог с файлом `__init__.py`, в котором располагается python-класс, наследующий от [sdk2.Task](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/task.py).
  Имя класса задачи автоматически преобразуется в ее тип (`MyTestTask -> MY_TEST_TASK`).
  Описание класса задачи ([docstring](https://www.python.org/dev/peps/pep-0257/)) становится описанием задачи:

    ```python
    from sandbox import sdk2

    class MyTestTask(sdk2.Task):
        """
        This is a task description.
        """
    ```

* Для правильной сборки задачи в каталог также необходимо добавить файл `ya.make`
  с макросом `SANDBOX_PY23_TASK` (бинарная задача на python2),
  `SANDBOX_PY3_TASK` (бинарная задача на python3) или `PY23_LIBRARY`.
  Все промежуточные директории, не содержащие кода задач, помечаются как `PY23_LIBRARY`.
* Для того чтобы задача появилась в Sandbox, ее исходный код должен попасть в trunk Аркадии.
* Если вы попытаетесь запустить задачу, которая не добавлена в общий бандл (т.е. эта задача доступна к запуску только в виде бинарной задачи), получите ошибку вида `Incorrect task type u'TASKLET_CREATE_YA_DEPLOY_RELEASE' (400)`


## Релизы кода задач sandbox/projects { #tasks-releases }

По умолчанию Sandbox всегда использует последнюю версию кода задач из транка Аркадии
(с небольшим отставанием из-за необходимости проведения тестов).
Текущая ревизия кода задач на серверах отображается под буквой `i` в подвале любой страницы Sandbox.

При этом за статусом тестирования влитых в trunk изменений можно следить на странице сборки
[BUILD_SANDBOX_TASKS в CI](https://a.yandex-team.ru/projects/sandbox/ci/actions/launches?dir=sandbox%2Fprojects&id=deploy-build-sandbox-tasks).
Коммиты, ломающие эту сборку, подлежат откатыванию.


## Sandbox SDK { #sdk }

Для разработки задач имеется набор классов с описанием основных типов данных, называемый Sandbox SDK.
Существует две версии этого SDK:

1. **[Sandbox SDK v1](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sandboxsdk)**. Используется в коде некоторых старых задач и объявлен **устаревшим**.

    {% note alert %}

    Запрещено писать новые задачи с использованием Sandbox SDK v1.

    {% endnote %}

2. **[Sandbox SDK v2](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2)**. Текущая версия, на которой следует писать все новые задачи.

## Логирование { #logging }

Для [логирования](../tasks.md#logs) в задачах следует использовать пакет [logging](https://docs.python.org/3/library/logging.html) из стандартной библиотеки Python:

```python
import logging
from sandbox import sdk2

class MyTask(sdk2.Task):
    def on_execute(self):
        logging.info("Boom!")
```

В зависимости от уровня логирования сообщения попадут в `common.log` или `debug.log`.

В `common.log` и `debug.log` попадают не только сообщения вашей задачи, но и другие записи полезные при отладке.

Более подробно о логгировании можно почитать [тут](../tasks.md#logs)


## Метаданные задачи { #task-metadata }

В классе [sdk2.Task](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/task.py) определены некоторые стандартные метаданные задачи, которые можно использовать в ее коде. Пример обращения к метаданным:

```python
import logging
from sandbox import sdk2

class MyTestTask(sdk2.Task):
    def on_execute(self):
        logging.info("My id is %s" % self.id)
```

Список доступных полей приведен в таблице:

Поле | Описание
:--- | :---
author | Автор задачи
container | Метаданные окружения, в котором запущена задача (может быть пустым)
created | Время создания задачи
host | Хост, на котором исполняется задача
hidden | Является ли задача скрытой (не отображается в списке задач)
id | Числовой идентификатор задачи
info | Описание задачи, отображаемое в секции Info
owner | [Группа](../groups.md)-владелец задачи
parent | Указатель на родительскую задачу
ramdrive | Информация о RAM-диске, используемом в задаче
scheduler | Информация о планировщике, запустившем задачу
status | [Состояние](../tasks.md#status) задачи
type | [Тип](../tasks.md#type) задачи
updated | Время последнего обновления задачи
