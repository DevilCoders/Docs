#Библиотека мониторинга Sandbox задач

## Описание
Библиотека позволяет добавить к sandbox задачам логику мониторинга выполнения и отправки результатов в Solomon

## Применение
Решение сделано в виде миксина, от которого наследуются ваши задачи sandbox, либо ваша базовая задача.
Для корректной работы миксин должен стоять первым среди базовых классов, так как он переопределяет методы on_* базовой задачи.
Также необходимо переопределить метод fill_task_tracker_config(), где вы зададите свою логику формирования параметров Solomon-а:\
разделение на окружения (prod | test), наследование параметров от родительских задач и пр.

Пример базового класса:
````
class YourBaseTask(CommonTaskTrackerMixin, sdk2.Task):
    class BaseParameters(BaseParameters):

    def fill_task_tracker_config(self):
        enable_solomon = True
        self.task_tracker_config.enable_solomon = enable_solomon
        self.task_tracker_config.solomon_track_start = True
        if enable_solomon:
            self.task_tracker_config.solomon_secret_token = 'sec-topsecrettoken'
            self.task_tracker_config.solomon_secret_key = 'solomon-token'
            self.task_tracker_config.solomon_secret_version = ''
            self.task_tracker_config.solomon_project = 'your_service'
            self.task_tracker_config.solomon_cluster = 'your_cluster'
            self.task_tracker_config.solomon_service = 'sandbox'
            self.task_tracker_config.solomon_common_labels = {}

        task_name = self.type.__name__
        self.task_tracker_config.source = '.'.join([self._solomon_prefix, task_name])
        self.task_tracker_config.host = task_name
````

В миксине есть возможность включить отслеживание запуска, в этом случае миксин дополнительно отправит статус 'RUNNING' при подготовке задачи и при завершении,\
а также проставит метки результата в начале выполнения, в этом случае визуально можно оценивать длительность выполнения.

Важно! Не забудьте делегировать секрет в sandbox для возможности хождения в секретницу.

Именования по умолчанию:
source = sandbox.{service-name}
host = {SandboxTaskName}
description - error description
status = {OK|CRIT}
Можете переопределить как вам необхоимо в fill_task_tracker_config()


