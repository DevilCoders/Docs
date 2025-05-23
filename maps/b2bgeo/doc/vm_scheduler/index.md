# Планировщик виртуальных машин (Virtual Machine Scheduler)

Планировщик запускает задачи на динамическом пуле ресурсов. Задача состоит из нескольких джобов. Каждый джоб -- вычислительная задача. Задача задается docker-образом и параметрами для запуска. Каждый джоб также имеет собственные параметры, которые передаются контейнеру в качестве аргументов при запуске, при этом docker-образ одинаков для всех джобов задачи.

Планировщик запускает задачи на виртуальных машинах, которые аллоцирует в облачном провайдере AWS. На аллоцированных машинах запускается агент, который запускает джобы в docker-контейнерах и общается с планировщиком (для получения назначенных задач, отправки статусов запущенных задач).

Планировщик предоставляет gRPC API.

## Зачем нужен Планировщик

[Асинхронный солвер](https://docs.yandex-team.ru/b2bgeo-dev/async_backend/) решает задачу оптимизации планирования маршрутов. Если задача достаточно большая, то в инсталляции солвера в RTC она решается на YT. При переезде во внешние облака понадобилась замена YT (YT использовался не совсем по назначению: просто как планировщик Map-операций). Данный планировщик является такой заменой.

## Архитектура

Планировщик является монолитом, но содержит логические части: аллокатор, gRPC-сервер, детектор отказов, планировщик (назначающий ВМ для джобов).

![Scheduler architecture](_includes/big_picture.png "Архитектура Планировщика")


## Полезные ссылки

* [Код](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/vm_scheduler)
* [README серверной части](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/vm_scheduler/server/readme.md)
* TBD README агента

## Проекты

* [2022 Реализация](https://st.yandex-team.ru/BBGEO-13573)

## Описание основного сценария работы

{% include [Sequence](_includes/sequence.wsd) %}

1. Пользователь добавляет задачу, содержащую несколько джобов, в планировщик. После успешного сохранения информации о новой задачи в БД, пользователь получает ответ с идентификатором задачи и статусом Queued.

2. Запускается итерация планирования джобов. Планировщик забирает из БД текущее состояние системы (все активные джобы и виртуальные машины). Будем называть джоб активным, если его статус не является финальным. ВМ является активной, если она не остановлена или ее завершение еще не запланировано. На этом этапе запускается алгоритм планирования, результатом которого является назначение джобов на виртуальные машины. Виртуальные машины могут быть уже аллоцированы, либо их аллокация будет запланирована. Также какие-то ВМ могут быть отмечены ожидающими завершение. Результат планирования сохраняется в БД.

3. Воркеры-аллокаторы мониторят состояние виртуальных машин в БД. Если есть ВМ, находящиеся в статусе ожидания аллокации или ожидания завершения, аллокатор совершает соответсвующие вызовы API облачного провайдера и записывает в БД статус аллокации. При аллокации ВМ указывается образ с агентом, который будет запущен.

4. Когда виртуальная машина аллоцирована, на ней запускается агент. Агент периодически опрашивает сервис планировщика о назначенных на его ВМ джобах. Агент оперирует только с джобами, не задачами. При получении назначенного джоба агент поллит docker-образ и запускает контейнер. Пока джоб выполняется, агент посылает планировщику heartbeat-ы. При завершении задачи агент сохраняет результат в S3 и сообщает планировщику о статусе выполненного джоба.

5. В течение всего времени выполнения задачи пользователь может поллить ее статус. Когда задача выполнена, пользователь может получить ссылку на результат, лежащий в S3. Также планировщик предоставляет API для отмены задачи.

## Детали реализации

### Устройство сервера на уровне кода

{% include [Classes](_includes/classes.wsd) %}

Планировщик написан на C++. Предоставляет gRPC API. gRPC-сервер реализует API для внешних пользователей (добавляющих задачи для выполнения, на момент написания этого текста таким пользователем является только асинхронный солвер). и для агентов (см. классы в отношении композиции с GrpcServer).

Класс Allocator отвечает за аллокацию виртуальных машин. Cодержит объект интерфейса (чистого абстрактного класса) CloudClient. На данный момент написана только одна реализация интерфейса для облака AWS. (В будущем может появиться поддержка других облаков, нужно лишь реализовать интерфейс CloudClient.) Идемпотентность аллокации виртуальных машин достигается за счет указания уникального токена при вызове метода аллокации AWS SDK.

В данной системе части системы могут отказывать. Под отказом имеется в виду любое некорректное поведение: например, слишком долгий старт агента, прекращение работы агента из-за рестарта сервера (по воли облачного провайдера или из-за проблем с ПО агента, запускаемыми задачами, например, OOM), аллоцированная ВМ, запись о которой отсутствует в БД (такое может произойти из-за неатомарности аллокации и записи в БД). Детектор отказов обнаруживает такие сбои и обрабатывает их.

Класс Scheduler реализует планирование виртуальных машин. Содержит объект интерфейса VmAssigner, который реализует сам алгоритм назначения задач на виртуальные машины. На момент написания этого текста реализован простейший алгоритм планирования (класс SimpleVmAssigner): выделяется новая виртаульная машина на каждый джоб.

Класс TaskRegistry содержит объекты классов GrpcServer, Allocator, Scheduler, FailureDetector.

### Состояния джобов

{% include [Job states](_includes/job_state.wsd) %}

При добавлении задачи в планировщик джобы, которые она содержит, добавляются в статусе Queued. При коммите плана статусы джобов, которым были назначены виртуальные машины, переводятся из Queued в Scheduled. Когда соответсвующая виртуальная машина аллоцирована и на ней запущен агент, агент узнает от планировщика о назначенной задаче (gRPC-вызов getAssignedJobs) и запускает ее. Далее агент делает gRPC-вызов (updateJobState), в котором сообщает, что задача начала выполняться. Планировщик выставляет в БД статус Running. Если задача успешно завершилась, то агент с помощью того же вызова передает ссылку на результат задачи в s3. В этом случае планировщик выставляет джобу статус Completed. Если контейнер завершился с ненулевым кодом возврата, то агент отправляет статус Error, который планировщик записывает в БД.

Задача может быть отменена либо пользователем, либо самим планировщиком (а именно компонентом детектор отказов), если задача не завершается за планируемое время выполнения, переданное пользователем. Отмененный джоб переводится в статус Cancelled.

Остальные переходы (обозначены пунктирными синими стрелками) производятся детектором отказов.

### Состояния виртуальных машин

{% include [VM States](_includes/vm_state.wsd) %}

Когда планировщик коммитит новый план назначений джобов на виртуальные машины, новые виртуальные машины создаются в статусе PendingAllocation. Воркер-аллокатор достает из БД ВМ в этом статусе, в той же транзакции выставляет ей статус Allocating и коммитит транзакцию. Затем аллокатор делает вызовы к API AWS для аллокации физической ВМ и запуска на ней агента. В случае успеха аллокатор переводит виртуальную машину в статус Allocated (изменение значения в соответсвующей колонке в записи в БД). В случае неуспешной аллокации ВМ переводится в статус PendingAllocation и будет обработана на другой итерации аллокации.

Ситуации, когда виртуальная машина была аллоцирована, но запись в БД по какой-то причине (например, сетевая ошибка) завершилась неудачно, или из-за рестарта сервера статус ВМ остался в промежуточном состоянии Allocating, обрабатываются детектором отказов (синие пунктирные переходы).

После аллокации виртуальной машины на ней запускается агент и периодически посылает hearbeat-ы. При получении первого heartbeat-а сервер выставляет статус AgentStarted ВМ в БД.

Когда Планировщик решает завершить ВМ, он выставляет статус PendingTermination в БД. Дальшейшие переходы в Terminating, Terminated аналогичны переходам в Allocating, Allocated.

### Схема БД

{% include [VM States](_includes/db_schema.wsd) %}

### Примеры gRPC-вызовов

#### Публичное API

- Добавить задачу в Планировщик:
```
grpcurl -d '{"limits": {"job_limits": {"memory_mb": 2, "cpu_cores": 1}, "execution_s": 5}, "settings": "{\"a\":\"b\"}", "job_count": 2, "image_version":"img version", "client_id":"yutsareva", "job_options":["{}","[]"]}' -plaintext -import-path <arcadia path> -proto public_api.proto <VM Acheduler address> maps.b2bgeo.vm_scheduler.proto.PublicApiScheduler/addTask

{
  "taskId": {
    "value": "4"
  }
}
```
- Получить статус решения джобов задачи
```
grpcurl -d '{"value":1}' -plaintext -import-path <arcadia path> -proto scheduler.proto <VM Acheduler address> maps.b2bgeo.vm_scheduler.proto.PublicApiScheduler/getTaskResult
{
  "status": "TASK_QUEUED",
  "jobResults": [
    {
      "status": "JOB_QUEUED"
    },
    {
      "status": "JOB_QUEUED"
    }
  ]
}
```
- Получить статус решения джобов задачи. Содержит поле "result_url" с ссылкой на результат в S3 в случае, если джоб успешно завершен.
```
grpcurl -d '{"value":1}' -plaintext -import-path <arcadia path> -proto scheduler.proto <VM Acheduler address> maps.b2bgeo.vm_scheduler.proto.PublicApiScheduler/getTaskState
{
  "status": "TASK_QUEUED",
  "jobStates": [
    {
      "status": "JOB_RUNNING"
    },
    {
      "status": "JOB_COMPLETED",
      "result_utl": "url to result on s3"
    }
  ]
}
```

#### API для агента

- Получить назначенные джобы
```
grpcurl -d '{"value": 18}' -plaintext -import-path <arcadia path> -proto agent_api.proto <VM Acheduler address> maps.b2bgeo.vm_scheduler.proto.AgentApiScheduler/getAssignedJobs
{
  "jobs": [
    {
      "id": {
        "value": "6"
      },
      "status": "JOB_QUEUED"
    }
  ]
}
```
- Получить данные джоба
```
grpcurl -d '{"vm_id": {"value": 18}, "job_id": {"value": 6}}' -plaintext -import-path <arcadia path> -proto agent_api.proto <VM Acheduler address> maps.b2bgeo.vm_scheduler.proto.AgentApiScheduler/getJobToLaunch
{
  "id": {
    "value": "6"
  },
  "imageVersion": "img version",
  "jobLimits": {
    "memoryMb": 2,
    "cpuCores": 1
  },
  "taskSettings": "{\"a\": \"b\"}",
  "jobOptions": "[]"
}
```
- Обновить статус джоба
```
grpcurl -d '{"vm_id": {"value": 18}, "job_id": {"value": 6}, "job_result": {"status": "JOB_RUNNING"}}' -plaintext -import-path <arcadia path> -proto agent_api.proto <VM Acheduler address> maps.b2bgeo.vm_scheduler.proto.AgentApiScheduler/updateJobState
{
}
```
