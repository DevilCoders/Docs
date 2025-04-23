# Этапы жизни задачи

## Перезапуски задачи { #restarts }

Одна и та же задача может исполняться несколько раз: как из-за инфраструктурных проблем, так и по желанию самой задачи.
Количество любых перезапусков задачи ограничено 640 – это общее ограничение, которое нельзя переопределить для конкретной задачи.
По достижении этого лимита задача переводится в статус `STOPPED`.

### Принудительный перезапуск { #force-restart }

Если вы хотите, чтобы задача была перезапущена, то в коде должно быть выброшено исключение `TemporaryError`.
В таком случае задача перейдет в статус `TEMPORARY` и будет перезапущена.
При этом повторные запуски будут происходить через прогрессивно растущее время, исчисляемое десятками секунд - единицами минут.

Перезапуск невозможен, если у задачи выставлен флаг `fail_on_any_error`. В этом случае задача будет переведена в статус `FAILURE`.


## Релизы { #releases}

Задачи в состоянии `SUCCESS` можно релизить — для этого необходимо нажать на кнопку `Release` на форме задачи.
Эта кнопка активна только для тех пользователей, которые имеют право доступа к задаче (являются автором либо входят в группу, являющуюся `owner`'ом) и кроме этого
входят в список `releasers` ресурсов задачи.

При релизе необходимо указать тип релиза, название и описание. После запуска релиза задача переходит в состояние `RELEASING`
и отправляется на один из хостов для выполнения метода класса задачи `on_release`.
По умолчанию этот метод выполняет следующее:
отправляет письмо-уведомление о релизе, а также на все не-сервисные ресурсы задачи добавляет атрибуты
`ttl=inf` и `released` с выбранным тегом релиза.
Это поведение можно изменить, перегрузив метод `on_release` класса задача.

Подробнее о релизах можно почитать [на отдельной странице документации](releases.md).


## Методы-обработчики событий { #methods }

Минимальная работоспособная задача в Sandbox выглядит так:

```python
import logging
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_execute(self):
        logging.info("Hello, world!")
```

Основные действия, которые выполняет задача, располагаются внутри метода `on_execute`.
Этот метод выполняется при переходе задачи в [состояние](../tasks.md#status) **EXECUTING**
В классе [sdk2.Task](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/task.py)
определены и другие методы-обработчики, которые могут вызываться на разных этапах жизни задачи.
Эти методы можно разделить на те, которые исполняются на агентах ([client-side](#client-side)),
и на те, которые исполняются на web-серверах ([server-side](#server-side))синхронно с обработкой API-запросов.

### Server-side методы { #server-side }

Данные методы запускаются на web-серверах Sandbox синхронно с соответствующими вызовами API.
Поэтому важно, чтобы эти методы исполнялись быстро.

Обработчик | Описание
:--- | :---
on_create | Вызывается при создании задачи
on_save | Вызывается после каждого изменения задачи в статусе `DRAFT`
on_enqueue | Вызывается перед постановкой задачи в очередь

### Client-side методы { #client-side }

Обработчик | Описание
:--- | :---
on_prepare | Вызывается при подготовке задачи к исполнению (статус `PREPARING`)
on_execute | Вызывается в начале исполнения задачи (статус `EXECUTING`). В этом методе содержится основная логика задачи
on_success | Задача завершается успешно
on_failure | Задача завершается неудачно (статус `FAILURE`)
on_break | Задача переходит в состояние из группы `BREAK` (`NO_RES`, `EXCEPTION`, `TIMEOUT`, `EXPIRED`, `STOPPED`)
on_finish | Задача завершается
on_release | Выполняется релиз задачи
on_terminate | Задача остановлена пользователем
on_timeout | Задача остановлена по таймауту (параметр задачи `kill_timeout`)
on_before_timeout | Вызывается перед тем, как задаче будет отправлен сигнал завершения по истечению максимального времени одной итерации исполнения (параметр задачи `kill_timeout`). Может использоваться для корректного завершения дочерних процессов
on_wait | Задача переходит в состояние из группы `WAIT` (`WAIT_RES`, `WAIT_TASK`, `WAIT_OUT`, `WAIT_TIME`)

### Полный список методов задачи в коде { #methods-in-code }
```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def on_create(self):
        """ Called on task creation """

    def on_save(self):
        """ Called when updating task in status DRAFT """

    def on_enqueue(self):
        """ Called before task is enqueued """

    def on_prepare(self):
        """ Called when task is preparing for execution on the host """

    def on_execute(self):
        """ Called when task is executing on the host """

    def on_finish(self, prev_status, status):
        """ Called when task is going to finish """

    def on_success(self, prev_status):
        """ Called when task is switching to status SUCCESS """

    def on_failure(self, prev_status):
        """ Called when task is switching to status FAILURE """

    def on_break(self, prev_status, status):
        """ Called when task going to switch to status from group BREAK """

    def on_timeout(self, prev_status):
        """ Called when task going to switch to status TIMEOUT """

    def on_before_timeout(self, seconds):
        """ Called before task executor is killed by timeout """

    def on_terminate(self):
        """ Called in signal handler when task executing is being stopped forcibly """

    def on_wait(self, prev_status, status):
        """ Called when task going to switch to status from group WAIT """

    def on_release(self, parameters):
        """ Executed when task release was submitted """
```


### Примеры обработчиков событий { #methods-examples }
Некоторые примеры использования обработчиков приведены ниже.

#### Выставление значений параметров в зависимости от других параметров

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    class Parameters(sdk2.Task.Parameters):
        user_name = sdk2.parameters.String("User name")
        greeting = sdk2.parameters.String("User greeting")

    def on_save(self):
        if self.Parameters.user_name:
            self.Parameters.greeting = "Hello, %s!" % self.Parameters.user_name
        else:
            self.Parameters.greeting = "Hello, unknown!"
```

#### Корректное завершение дочерних процессов

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def _start_child_process(self):
        """ Some code to start child process """

    def _stop_child_process(self):
        """ Some code to stop child process """

    def on_execute(self):
        self._start_child_process()

    def on_terminate(self):
        self._stop_child_process()  # Stop when task is manually stopped

    def on_before_timeout(self, seconds):
        self._stop_child_process()  # Stop when task is stopped because of timeout
```

#### Выполнение подготовительных шагов задачи

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def _clone_source_code(self):
        """ Downloads source code from repository """

    def _compile_source_code(self):
        """ Compiles source code """

    def on_prepare(self):
        self._clone_source_code()

    def on_execute(self):
        self._compile_source_code()
```

#### Отправить сигнал во внешний сервис при успешной сборке

```python
from sandbox import sdk2

class MyTestTask(sdk2.Task):

    def _notify_on_success(self):
        """ Send signal on success """

    def on_success(self, prev_status):
        self._notify_on_success()
```

#### Написать комментарий в Стартрек при падении сборки

```python
import sandbox.sdk2 as sdk2

class MyTestTask(sdk2.Task):

    def _post_startrek_comment(self, message):
        """ Post comment to Startrek issue """

    def on_failure(self, prev_status):
        self._post_startrek_comment("Task {} started by {} failed".format(self.id, self.author))
```

#### Предупреждение о таймауте задачи (`on_before_timeout`) { #on_before_timeout }
Когда время исполнения задачи превышает её `kill_timeout`, процесс задачи и все его подпроцессы убиваются по `SIGKILL`.
В некоторых случаях может потребоваться произвести некоторые действия перед тем как это произойдет.
Для этого в отдельном потоке крутится специальный сервис, который запускает метод класса задачи `on_before_timeout` за определенное время до завершения задачи по таймауту.

```python
class MyTask(sdk2.Task):
  ...
  def on_before_timeout(seconds):  # запускается за seconds секунд до таймаута
      if seconds <= 3 * 60:
          # try to kill registered processes by SIGTERM
          for process in sdk2.helpers.ProcessRegistry:
              try:
                 os.kill(process.pid, signal.SIGTERM)
              except OSError:
                 continue

   # переопределите этот метод чтобы установить кастомные промежутки времени (по умолчанию [10, 30, 60, 60 * 3, 60 * 5])
   def timeout_checkpoints(self):
      return [5, 10, 20, 40, 60]
```

#### Обработка исполняющейся задачей собственной остановки (`on-terminate`) { #on-terminate }
Исполняющаяся задача (в статусах **PREPARING** и **EXECUTING**) может быть остановлена извне. Например, нажатием на кнопку `STOP` в web-интерфейсе.
В этом случае процессу задачи будет отправлен сигнал `SIGTERM`.
При этом, если задаче при остановке требуется выполнить какие-то действия, то она может это сделать в методе `on_terminate`. Этот метод автоматически добавляется в обработчик соответствующего сигнала процесса задачи. Он будет запущен в отдельном процессе.

Использование `on_terminate` может быть полезно, например, если задача запускает какую-то работу во внешних системах, а при собственной остановке хочет остановить и запущенную работу.
При этом останавливать подпроцессы таким способом обычно не стоит, так как все подпроцессы и так будут убиты после остановки главного процесса задачи.
```python
def on_terminate(self):
    logging.info("Terminating, aborting activity #{} in third party".format(self.Context.activity_id))
    # Finish sub-jobs
```


## Удаление объектов задач из базы данных { #purge-policy }

Политика удаления объектов задач из нашей базы данных зависит от статуса задачи.
Однако, до тех пор, пока у задачи есть хотя бы один `READY` ресурс, задача не будет удалена.
Таким образом, основным фактором существования объекта задачи является наличие у неё живых ресурсов.

Правила очистки:
1. Задачи переходят в состояние `DELETED`:
    * Из состояния `DRAFT` или `STOPPED` - **через 7 дней после последнего изменения**;
    * Из состояния `EXCEPTION`, `NO_RES` или `TIMEOUT` - **через 14 дней после последнего изменения**;
    * Из состояния `SUCCESS` или `FAILURE`, созданные через API и при отсутствии связанных ресурсов в состоянии `READY` -
        **в момент, когда все ресурсы задачи стали DELETED**.

2. Задачи в состоянии `DELETED` полностью удаляются из базы данных **через 7 дней после последнего изменения**.

3. Для задач старше 30 дней из аудита (истории) удаляются все записи, кроме первых записей о состояниях `DRAFT`, `ENQUEUED`, `EXECUTING` и последней записи.

4. Задачи в статусах `SUCCESS` или `FAILURE` и созданные через Web-интерфейс не удаляются никогда.
