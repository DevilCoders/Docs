# Многопоточная обертка для мапперов и редьюсеров

Библиотека образует обертку для мапперов/редьюсеров с возможностью их исполнения в несколько потоков.

1. [Быстрый старт](#быстрый-старт)
    1. [Многопоточный маппер](#многопоточный-маппер)
    1. [Многопоточный редьюсер](#многопоточный-редьюсер)
1. [Статистика операций](#статистика-операций)
1. [Описание](#описание)
    1. [MTJob](#mtjob)
    1. [MTMapper](#mtmapper)
    1. [MTReducer](#mtreducer)
    1. [QReader](#qreader)
    1. [QWriter](#qwriter)
    1. [Worker](#worker)
    1. [WriterWorker](#writerworker)
    1. [Job](#job)

## Быстрый старт

### Многопоточный маппер

Класс `MTMapper` оборачивает переданный в качестве параметра шаблона маппер и запускает его на заданном числе потоков.

Чтобы перевести свой маппер на многопоточный вариант, нужно:

1) поменять базовый класс на `mt_jobs::Job`;

2) обернуть создание класса в `MTMapper` с передачей необходимого количества потоков и функции, создающей экземпляр исходного маппера.

```cpp
#include <maps/analyzer/libs/mt_jobs/include/mt_mapper.h>

using namespace maps::analyzer::mt_jobs;

// custom mapper (single thread)
class SquareMapper: public Job {
public:
    // необходимые методы
    void Do(TReader* reader, TWriter* writer) override
    {
        for (auto& cursor: *reader) {
            auto row = cursor.MoveRow();
            auto tableIndex = cursor.GetTableIndex();

            Row outRow;
            const auto num = row["number"].AsInt64();
            outRow["number"] = num;
            outRow["squared"] = num * num;
            outRow["table_index"] = tableIndex;

            writer->AddRow(outRow, tableIndex);
        }
    }
    //
};

int test() {
    std::size_t threads = 2;
    std::size_t batchSize = 4, outputBatchSize = 4;
    // create MTMapper
    MTMapper<SquareMapper> mtMapper(
        [&]() { return std::make_unique<SquareMapper>(); },
        // optional; {.threads = 1, worker.batchSize = 1024, output.batchSize = 1024} by default
        {.threads = threads, .worker = {.batchSize = batchSize}, .output = {.batchSize = outputBatchSize}}
    );

    mtMapper->Start(TWriter* /*writer*/);
    mtMapper->Do(TReader* /*reader*/, TWriter* /*writer*/);
    mtMapper->Finish(TWriter* /*writer*/);
}

```

### Многопоточный редьюсер

Класс `MTReducer` оборачивает переданный в качестве параметра шаблона редьюсер и запускает его на заданном числе потоков.

Чтобы перевести свой редьюсер на многопоточный вариант, нужно:

1) поменять базовый класс на `mt_jobs::Job`;

2) обернуть создание класса в `MTReducer` с передачей необходимого количества потоков и функции, создающей экземпляр исходного редьюсера.

```cpp
#include <maps/analyzer/libs/mt_jobs/include/mt_reducer.h>

using namespace maps::analyzer::mt_jobs;

// custom reducer (single thread)
class GreatestEven: public Job {
public:
    // необходимые методы
    void Do(TReader* reader, TWriter* writer) override
    {
        Row outRow;
        outRow["number"] = -1;
        for (auto& cursor: *reader) {
            auto row = cursor.GetRow();

            const auto num = row["number"].AsInt64();

            if (num % 2 == 0 && num > outRow["number"].AsInt64()) {
                outRow = row;
            }   
        }
        if (outRow["number"].AsInt64() != -1) {
            writer->AddRow(outRow);
        }   
    }
    //
};

int test() {
    std::size_t threads = 2;
    std::size_t batchSize = 4, outputBatchSize = 4;
    // create MTReducer
    MTReducer<GreatestEven> mtReducer(
        threads,
        [&]() { return std::make_unique<GreatestEven>(); },
        // optional; {.threads = 1, worker.batchSize = 1024, output.batchSize = 1024} by default
        {.threads = threads, .worker = {.batchSize = batchSize}, .output = {.batchSize = outputBatchSize}}
    );

    mtReducer->Start(TWriter* /*writer*/);
    mtReducer->Do(TReader* /*reader*/, TWriter* /*writer*/);
    mtReducer->Finish(TWriter* /*writer*/);
}

```

## Статистика операций

Пользовательские статистики пишутся в YT-операции (секция `custom`):
* `init_time` — время загрузки; это время должно быть относительно небольшим по сравнению с `total_time`. Если это не так, возможно, стоит увеличить `data_size_per_job`, чтобы увеличить долю выполнения непосредственно операции. Слишком большой `data_size_per_job`, однако, повышает риск потери большого кол-ва работы из-за абортов джоб
* `total_time` — общее время работы джобы
* `reading` — секция касательно чтения входных таблиц
  * `time_ms` — общее время чтения; включает в себя ожидание свободных воркеров
  * `wait_time_ms` — время ожидания свободных воркеров; если число большое, это значит, что воркеры обрабатывают данные медленнее, чем читается вход; в целом это нормально
  * `blocking_time_ms` — время блокирования из-за переполнения очереди текущего воркера; говорит о слишком больших ключах, также об этом будет предупреждение в `stderr`
  * `rows_per_sec` — строки в секунду с учётом ожидания
  * `wait_time_percent` - процент времени ожидания свободного воркера от общего времени чтения
  * `blocking_time_percent` - процент времени блокирования из-за переполнения очереди текущего воркера от общего времени чтения
* `job` — секция касательно операции
  * `time_ms` — общее время операции
  * `rows_per_sec` — общая скорость выполнения операции всеми воркерами с учётом ожидания писателя
  * `wait_time_ms` — общее (суммарное по потокам) время ожидания писателя воркерами; большое число означает, что писатель не успевает записывать результат и, возможно, имеет смысл снизить кол-во потоков
  * `avg_wait_time_percent` - средний процент времени ожидания писателя одним воркером
* `writing` — секция касательно писателя
  * `time_ms` — общее время работы писателя
  * `rows_per_sec` — строки в секунду

Дополнительно `MTReducer` пишет статистику `keys` — общее кол-во обработанных ключей; желательно, чтобы даже минимальное значение превосходило кол-во потоков.

## Описание

### MTJob

[`MTJob<T>`](impl/mt_job.h) — базовый класс для `MTMapper`, `MTReducer`. Реализует все необходимые методы, кроме `Do` (определяется в `MTMapper`, `MTReducer`), и поля для многопоточных джоб. Поддерживает логирование статистики операций. Параметры многопоточной джобы задаются структурой `MtJobConfig`:
* `threads` - количество worker'ов
* `worker` - кофигурация (`QueueConfig`) очередей worker'ов
* `output` - кофигурация (`QueueConfig`) очереди потока-писателя

Структура [`QueueConfig`](impl/worker.h) состоит из:
* `batchSize` - количество строк, помещаемых в очередь в рамках одного пакета
* `bufferLimit` - максимальное количество строк, которое может обрабатываться очередью в данный момент времени

Данные между читателем, worker'ами и писателем передаются пакетами, хранение которых занимает память. 
* максимальное потребление между читателем и воркерами = `(worker.bufferLimit + worker.batchSize) * threads`
* максимальное потребление между вокерами и писателем = `output.bufferLimit + output.batchSize * threads`
* `worker.bufferLimit` должен быть больше типичного размера ключа в редьюсе, иначе есть риск упереться в одного воркера на тяжёлом ключе, это отразится в статистике `job/wait_time_ms` (`NOTE: поправим в рамках [MAPSJAMS-4332]`)
* чем тяжелее строки, тем больше это требует памяти, по необходимости понижайте `batchSize`


### MTMapper

[`MTMapper<M>`](include/mt_mapper.h) — создает необходимое количество (аргумент `threads`) потоков `Worker` и один поток-писатель `WriterWorker`; наполняет пакетные очереди (размер пакета регулируется параметром `batch_size`) worker-ов и ждет, пока они обработают свои очереди и запишут результат в очередь потока-писателя, который заполнит данными таблицу. Переключается между worker'ами после записи очередной строки.

* Для инициализации маппера внутри каждого `Worker'а` необходимо передать в конструктор `MTMapper'а` функцию, которая создает экземпляр маппера `M` и возвращает уникальный указатель на него.

### MTReducer

[`MTReducer<R>`](include/mt_reducer.h) — работает аналогично `MTMapper`. За исключением того, что заполняет очередь активного worker'а непрерывно строками с одинаковым ключом, после чего переключается на следующего активного worker'а.

### QReader

Фейковый `TReader`, который читает строки из пакетной очереди кокретного потока.
Имеет аналогичные методы `IsValid, Next, MoveRow, GetRow, GetTableIndex`, но работающие с внутренней пакетной очередью.

Для работы с `QReader'ом` внутри `Worker'а` используются методы:

* `emitRow` - записи строк в очередь ридера;
* `emitKeySwitch` - для обозначения смены текущего ключа (редьюс задачи);
* `getNextKey` - для перехода к следующему ключу (редьюс задачи); если какие-то строки текущего ключа не были прочитаны внутри `Do`, поток их дочитает.

### QWriter

Фейковый `TWriter`, который пишет обработанные worker-ом строки в очередь `WriterWorker'а`.
Имеет аналогичный метод `AddRow` для записи элементов в очередь.

### Worker

[`Worker<M>`](impl/worker.h) — владеет собственной пакетной очередью для чтения из потока (`QReader`) и писателем (`QWriter`) для заполнения очереди `WriterWorker'а`. Внутри потока работает собственный маппер/редьюсер `M`.

* `push` — пишет значения для обработки в очередь `Worker'а`;
* `done` — сигнализирует `Worker'у`, что текущий ключ обработан.

### WriterWorker

[`WriterWorker`](impl/worker.h) — отдельный поток для записи данных в таблицу; содержит очередь, которую заполняют worker-ы, и вычитывающий ее event_loop.

### Job

[`Job`](include/job.h) — абстрактный класс для работы с многопоточным маппером/редьюсером.

Содержит методы:

* `Start, Finish`, которые по дефолту ничего не делают; не нуждаются в перегрузке;
* чисто виртуальный метод `Do`.
