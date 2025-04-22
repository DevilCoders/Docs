TaskSemaphore
=============

Полезен в ситуациях, когда мы хотим, чтобы дальше прошла только часть тасок: например, мы хотим выдавать в Янг/Толоку только первые 1000 тасок по приоритету.

Решение - по сути дела персистентный семафор на Postgresql:
- можно "вставать" в очередь, указывая свой приоритет
- семафор знает количество активных заданий и рассылает событие активации тем, кто дождался
- может также рассылать просьбы деактивироваться, если надо освободить место более приоритетным заданиям

Характеристики предлагаемого:
- должен довольно хорошо работать с умеренным количеством семафоров (<100)
- и с не очень большой глубиной "активных" заданий
- при этом размер очереди неактивных не должен никак влиять на скорость

Реализация
----------

Схема данных:
```sql
create table markup.semaphore (
    id serial primary key,
    key text not null,
    active int not null default 1000, -- количество активных заданий
    try_release int not null default 900 -- какое количество активных с хвоста можно убирать, чтобы засунуть более приоритетные
);

create unique index ix_semaphore on markup.semaphore(key);

create type markup.semaphore_status as enum ('WAIT', 'ACQUIRED', 'TRY_RELEASE');

create table markup.semaphore_task (
    semaphore_id int not null references markup.semaphore(id),
    task_id bigint not null references markup.task(id),
    priority double precision not null,
    status markup.semaphore_status not null default 'WAIT',
    enqueued timestamptz not null default now(),
    primary key (semaphore_id, task_id)
);

create index ix_semaphore_task_wait on markup.semaphore_task(semaphore_id, priority);
create index ix_semaphore_task_active on markup.semaphore_task(semaphore_id, priority) where status in ('ACQUIRED', 'TRY_RELEASE');
```

API:
```kotlin
interface TaskSemaphoreManager {
    fun getOrCreate(key: String): TaskSemaphore
    fun update(key: String, active: Int, tryRelease: Int)
}

interface TaskSemaphore {
    /**
     * Можно вызывать повторно, будет изменять приоритет.
     */
    fun enqueue(taskId: TaskId, priority: Double)
    fun release(taskId: TaskId)
}

sealed class TaskSemaphoreEvent : Event() {
    data class Acquired(val semaphoreKey: String): TaskSemaphoreEvent()
    data class TryRelease(val semaphoreKey: String): TaskSemaphoreEvent()
}
```

Управление - просто tms-ка, которая раз в минуту для каждого семафора:
1. выбирает limit active тасков в порядке приоритета
2. выбирает все работающие таски (ACTIVE, TRY_RELEASE)
3. в свободные места засовывает новые таски из п. 3 - шлёт им `Acquired` (а они в ответ уже там делают, что надо - идут в Янг и т.п.)
4. если у нас появились более приоритетные таски, то пытается освободить самые неприоритетные из работающих (количество в конфиге - грубо говоря, размер хвоста, который можно трогать, например, не освобождать первые 100 из тех, что сейчас активны - их могут взять). Тут надо додумывать, сейчас так себе гарантии.

Риски:
- плохо будет работать для 1000+ семафоров, т.к. каждый требует индивидуальной обработки - будет увеличиваться время полного обхода => выдачи новых заданий, т.к. им надо получить "ок"
- хорошо работает для маленьких количеств тасков, т.к. для переприоритезации надо выбрать из БД N активных записей
- может плохо работать (как и вся система), если очередь событий будет забиваться, т.к. нужно довольно быстро "выдавать" и "освобождать" слоты, из-за этого, возможно, потребуется добавить всё же приоритетов событиям
- т.к. мы будем держать в Янге/Толоке маленький объём данных, постоянно (по сути раз в минуту) подбрасывая новые, то есть большой риск "остановки"

Вопрос глубины очереди:
- текущий объём 150К - это оценка сверху 300 оферов/минуту
- если держать выданными 1К заданий - это от 1К до 10К оферов, т.е. объём на 3-30 минут



