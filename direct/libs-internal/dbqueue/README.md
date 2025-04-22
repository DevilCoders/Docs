dbqueue
===

Очередь задач в MySQL. Нужна в таком виде, потому что умеет несколько ключевых вещей:

1. хранить задания надёжно и даже иногда обрабатывать их в общей транзакции с чем-нибудь ещё
2. обрабатывать задания повторно, если с первого раза не получилось
3. (когда-нибудь в будущем) обрабатывать задания отложенно
4. (когда-нибудь в будущем) хранить в одной базе задания в нескольких пространствах имён
5. надёжно хранить результаты заданий, чтобы потом можно прямо у очереди спросить, чем же это кончилось

Как с этим работать
----

### Зарегистрировать тип задачи

1. записать some_type в `etc/dbqueue-types.yaml` в перловом коде.
В базу запись справочника попадёт автоматом по скрипту, запускаемому кроном `ppcFillDBQueueJobTypes.pl`.
Но только когда `etc/dbqueue-types.yaml` будет в транке.

2. написать java-кода:
```java
// ru.yandex.direct.core.entity.some.jobs
// оба класса должно быть можно обрабатывать jackson-ом для запаковки/распаковки из json
class SomeJobArgs {
    // какие-то данные и функции, типа JavaBean
    // ...
}
class SomeJobResult {
    // какие-то данные и функции, типа JavaBean
    // ...
    
    public static SomeJobResult error(String strackTrace) {
        // ...
    }
}

// ru.yandex.direct.core.entity.dbqueue
class DbQueueJobTypes {
    public static final DbQueueJobType<SomeJobArgs, SomeJobResult> SOME_JOB_TYPE =
            new DbQueueJobType<>("some_type", SomeJobArgs.class, SomeJobResult.class);
}
```

### Поставить задачу

```java
class WhateverService {
    private final DbQueueRepository dbQueueRepository;
    
    public void doOperation(long clientId, long uid) {
        int shard = 8;
        
        dbQueueRepository.insertJob(shard, SOME_JOB_TYPE, clientId, uid,
                new SomeJobArgs());
    }
}
```

### Сделать задачу

```java
// ru.yandex.direct.jobs.whatever
public class Procrastinator extends DirectShardedJob {
    private final DbQueueService dbQueueService;
    
    @Override
    public void execute() throws JobExecutionException {
        int shard = getShard();
        for (int i = 0; i < MAX_JOBS_PER_RUN; i++) {
            boolean jobProcessed = dbQueueService.grabAndProcessJob(shard, SOME_JOB_TYPE,
                    this::processJob, MAX_ATTEMPTS, SomeJobResult::error);

            if (!jobProcessed) {
                break;
            }

        }
    }

    private SomeJobResult processJob(DbQueueJob<SomeJobArgs, SomeJobResult> job) {
        // сделать это и вернуть результат про успех
    }
}
```

### Не забыть почистить очередь

```java
// ru.yandex.direct.jobs.whatever
public class ProcrastinatorCleanup extends DirectShardedJob {
    private static final Duration TTL = Duration.ofDays(30);
    private static final int LIMIT = 10000;
    private static final Logger LOGGER = LoggerFactory.getLogger(ProcrastinatorCleanup.class);
    
    private DbQueueRepository dbQueueRepository;
    
    @Override
    public void execute() throws JobExecutionException {
        int deletedJobs = dbQueueRepository.cleanup(getShard(), SOME_JOB_TYPE, TTL, LIMIT);
        LOGGER.info("deleted jobs: {}", deletedJobs);
    }
}

```
