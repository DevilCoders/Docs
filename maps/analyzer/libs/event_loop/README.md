# Обработка событий в потоке на базе libevent

Библиотека образует обработку очередей/событий на базе libevent.

1. [Быстрый старт](#быстрый-старт)
    1. [Очередь с подпиской](#очередь-с-подпиской)
    2. [Pull-очередь](#pull-очередь)
1. [Описание](#описание)
    1. [Событийный поток](#событийный-поток)
    1. [События](#события)
    1. [Очереди](#очереди)
    1. [Pull-очереди](#pull-очереди)

## Быстрый старт

### Очередь с подпиской

Очереди с подпиской постоянно вычитываются в отдельном событийном потоке, вызывая пользовательский callback на каждый прочитанный элемент.

Для быстрого старта нам понадобятся классы:
* `EventLoop`, реализующий поток-читатель; описан в заголовочнике [`event_loop.h`](include/event_loop.h)
* `Queue<T>`, реализующий очередь, которая обрабатывается в потоке-читателе; описан в [`queue.h`](include/queue.h)
* `BatchQueue<T>`, обёртка поверх `Queue<T>`, которая пишет в очередь пакетами; описан в [`batch_queue.h`](include/batch_queue.h)

```cpp
#include <maps/analyzer/libs/event_loop/include/queue.h>
#include <maps/analyzer/libs/event_loop/include/event_loop.h>

using namespace maps::analyzer::event_loop;

int test() {
    // create and start reader thread
    EventLoop loop;
    loop.start();

    // create queue with consume-function
    int result = 0;
    Queue<int> q(loop, [&](int v) {
        result += v;
    });

    // push values to queue, this can be done from several threads
    q.push(10);
    q.push(20);
    q.push(30);

    // close queue and wait for all pending items to be processed
    q.join();
    // stop thread
    loop.stop();

    return result;
}
```

Пакетная очередь отличается тем, что для записи нужно создать объект типа `BatchWriter<T, BatchQueue>`, который содержит буфер неотправленных элементов:

```cpp
    BatchQueue<int> q(loop, [&](int v) {
        result += v;
    });

    auto w = q.writer();
    w.push(10);
    w.push(20);
    w.push(30);
    w.flush(); // called in dtor too
```

См. также примеры в [`examples`](examples):
* [`queue`](examples/queue/main.cpp) — минимальный пример с очередью
* [`sum`](examples/sum/main.cpp) — чуть более сложный пример: N потоков пишут числа, читатель их суммирует
* [`batch_sum`](examples/batch_sum/main.cpp) — многократно более быстрый вариант [`sum`](examples/sum/main.cpp)
* [`timer`](examples/timer/main.cpp) — пример с таймером

### Pull-очередь

В отличие от очередей с подпиской pull-очередь не создаёт дополнительных потоков и читается по запросу в основном потоке.

Для работы с pull-очередью нам понадобятся классы:
* `PullQueue<T>`, позволяющий получить следующий элемент из очереди без создания дополнительного читающего потока; описан в [`pull_queue.h`](include/pull_queue.h)
* `BatchPullQueue<T>`, обёртка поверх `PullQueue<T>`, которая пишет в очередь пакетами; описан в [`batch_pull_queue.h`](include/batch_pull_queue.h)

```cpp
#include <maps/analyzer/libs/event_loop/include/pull_queue.h>

using namespace maps::analyzer::event_loop;

int test() {
    // create queue
    int result = 0;
    PullQueue<int> q;

    // push values to queue
    std::thread ([&](){
        q.push(1);
        q.push(2);

        // join queue
        q.join();
    }).detach();

    // read from queue
    for (auto v = q.pop(); v.has_value(); v = q.pop()) {
        result += v.value();
    }

    return result;
}
```

Для работы с пакетной pull-очередью, как и ранее, требуется создать объект типа `BatchWriter<T, BatchPullQueue>`, который содержит буфер неотправленных элементов:

```cpp
    std::size_t result = 0;
    BatchPullQueue<std::size_t> q;

    std::thread ([&](){
        auto w = q.writer();
        w.push(1);
        w.push(2);
        w.flush();

        q.join();
    }).detach();

    // read elements from queue
    for (auto v = q.pop(); v.has_value(); v = q.pop()) {
        result += v.value();
    }

    return result;
```

## Описание

### Событийный поток

[`EventLoop`](include/event_loop.h) — определяет поток, в котором будут обрабатываться все события и обработки очередей.
* Для обработки событий в отдельном потоке имеет два метода: `start` и `stop`. Поток после остановки можно возобновлять (строго говоря, после перезапуска запустится новый поток, но очередь событий продолжит обрабатываться та же).
* Для обработки одного активного события без создания отдельного потока есть блокирующий метод `step`. Отдельный поток при этом не должен быть запущен (или должен быть остановлен методом `stop`).

### События

События описываются классом [`Event`](include/event.h) с двумя основными функциями:
* `on` — включить обработку событий (возможно указать таймаут)
* `off` — отключить обработку событий

В качестве событий могут выступать события чтения/записи в какой-либо файловый дескриптор. В частном случае можно не указывать дескриптор и получить таким образом таймер. В [`event.h`](include/event.h) для создания таймера — события без дескриптора — есть функция `timer`.

### Очереди

[`Queue<T>`](include/queue.h) — многопоточная очередь (много писателей, один читатель), привязана к событийному потоку и обрабатывает все элементы в его контексте, пока он работает:
* `push` — положить элемент в очередь; возвращает `false`, если очередь уже закрыта на запись; блокируется, если очередь переполнена
* `close` — закрывает очередь и возвращает `std::future<void>` на то, что очередь обработана целиком
* `join` — закрывает очередь и ждёт обработки

Реализована на базе pipe'ов, создаёт пару дескрипторов (на чтение и на запись) с помощью функции `pipe2`; в пишущий дескриптор идёт запись, а на читающий дескриптор подписывается обработчик событий в рамках соответствующего потока.

**NOTE**: Атомарные (`std::is_trivially_copyable_v`, и при этом меньшие `PIPE_BUF`) значения в очередь кладутся как есть, остальные же типы перемещаются во временный объект в куче и удаляются после обработки их в читателе. Таким образом во избежание утечки памяти необходимо дождаться обработки очередью всех сообщений.

### Pull-очереди

[`PullQueue<T>`](include/pull_queue.h) — объединяет многопоточную очередь (`Queue`) и событийный поток (`EventLoop`), но обрабатывает все элементы в контексте основного потока по запросу, не порождая дополнительный фоновый поток:
* `push` — аналогично `Queue<T>::push`
* `close` — аналогично `Queue<T>::close`
* `join` — аналогично `Queue<T>::join`
* `pop` — возвращает следующий элемент из очереди или `std::nullopt`, если очередь пуста и закрыта; блокируется, если очередь пуста, но не закрыта.
