<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Preliminaries](#preliminaries)
- [Инструменты](#%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B)
  - [Работа с C++ потоками в ads_pytorch](#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-c-%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%B0%D0%BC%D0%B8-%D0%B2-ads_pytorch)
    - [Интерфейс](#%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81)
    - [Как программировать свои функторы](#%D0%BA%D0%B0%D0%BA-%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D1%82%D1%8C-%D1%81%D0%B2%D0%BE%D0%B8-%D1%84%D1%83%D0%BD%D0%BA%D1%82%D0%BE%D1%80%D1%8B)
  - [StringHandle: работа с байтами между python/C++](#stringhandle-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%B1%D0%B0%D0%B9%D1%82%D0%B0%D0%BC%D0%B8-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-pythonc)
    - [StringHandle](#stringhandle)
    - [BufferProtocol/memoryview](#bufferprotocolmemoryview)
  - [TensorPipe](#tensorpipe)
    - [CPU: SharedMemory](#cpu-sharedmemory)
    - [GPU: CudaSharedMemory](#gpu-cudasharedmemory)
    - [NestedTensorStructure](#nestedtensorstructure)
    - [Эффективность передачи nested_tensor_structure между процессами](#%D1%8D%D1%84%D1%84%D0%B5%D0%BA%D1%82%D0%B8%D0%B2%D0%BD%D0%BE%D1%81%D1%82%D1%8C-%D0%BF%D0%B5%D1%80%D0%B5%D0%B4%D0%B0%D1%87%D0%B8-nested_tensor_structure-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-%D0%BF%D1%80%D0%BE%D1%86%D0%B5%D1%81%D1%81%D0%B0%D0%BC%D0%B8)
    - [Часто возникающие проблемы](#%D1%87%D0%B0%D1%81%D1%82%D0%BE-%D0%B2%D0%BE%D0%B7%D0%BD%D0%B8%D0%BA%D0%B0%D1%8E%D1%89%D0%B8%D0%B5-%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D1%8B)
      - [Чтение CUDA тензоров из очереди в посылающем процессе](#%D1%87%D1%82%D0%B5%D0%BD%D0%B8%D0%B5-cuda-%D1%82%D0%B5%D0%BD%D0%B7%D0%BE%D1%80%D0%BE%D0%B2-%D0%B8%D0%B7-%D0%BE%D1%87%D0%B5%D1%80%D0%B5%D0%B4%D0%B8-%D0%B2-%D0%BF%D0%BE%D1%81%D1%8B%D0%BB%D0%B0%D1%8E%D1%89%D0%B5%D0%BC-%D0%BF%D1%80%D0%BE%D1%86%D0%B5%D1%81%D1%81%D0%B5)
  - [BaseAsyncWorkerPool](#baseasyncworkerpool)
  - [ExtendableStream](#extendablestream)
    - [Пример](#%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

Данная документация - техническое описание основных объектов в обучалке с перечислением неочевидных особенностей, оптимизаций и т.д.

# Preliminaries
Предполагается, что читатель знаком с:
1. asyncio
2. I/O multiplexing: poll/epoll
3. Unix Domain Socket, STREAM/DGRAM сокеты, блокирующая/неблокирующая запись/чтение
4. Unix shared memory ```//dev/shm```
5. PyTorch
6. [Асинхронная работа с CUDA](https://pytorch.org/docs/stable/notes/cuda.html), [CUDA Stream](https://docs.nvidia.com/cuda/cuda-runtime-api/group__CUDART__STREAM.html), cudaStreamSynchronize
7. Аллокации на GPU. [CUDACachingAllocator](https://github.com/pytorch/pytorch/blob/master/c10/cuda/CUDACachingAllocator.cpp)
8. [OnlineLearning](https://clubs.at.yandex-team.ru/machinelearning/2177)

# Инструменты
Базовые "строительные блоки", на которых мы строим все остальное

## Работа с C++ потоками в ads_pytorch
Long-long time ago, мы использовали python потоки для запуска C++ функций. Делали по классике:
1. Запускали python поток в ```loop.run_in_executor```
2. Отпускали GIL
3. Ждали поток через asyncio.future

Такой метод обладает целым рядом недостатков:
1. Нужно следить за тем, чтобы в python потоках не было ничего лишнего-питоновского, иначе все тормозит из-за GIL
2. Поскольку C++ код запускается из питона, flamegraph от perf выглядит хрен пойми как. По нему невозможно было что-то нормально понять.
3. Если где-то в недрах C++ лок не будет отпущен, такой код перестанет отвечать на сигналы (к примеру, не будет ctrl+c работать, питон просто не будет вызвать свой обработчик сигналов) и в целом там 100500 способов намертво подвесить код
4. Код плохо масштабируется на большое число потоков из-за того же GIL
5. Использовать CProfile для поиска боттлнеков в многопоточном питоне + C++ тоже дело крайне непростое

В какой-то момент нам это надоело и мы поставили следующую задачу: вообще всю многопоточность целиком нужно унести в C++, потому что от python потоков одни проблемы. Чтобы понять, как это провернуть, для начала разберемся, как asyncio работает с потоками. В uvloop это делается **примерно** так:
1. Мы пушим нашу python функцию в функцию ```loop.run_in_executor(py_thread_pool, our_func, *args)```
2. ```out_func``` оборачивается примерно вот так. sock - некоторый UNIX stream сокет (или другой IPC интерфейс, я уже не помню), сидящий внутри самого event_loop
```(python)
def _run_in_executor_wrapper(sock, our_func, *args):
    try:
        return our_func(*args)
    except:
        sock.send('failure_bytes')
        raise
    else:
        sock.send('success_bytes')
```
3. Пушим джобу в тредпул ```py_thread_pool.submit(_run_in_executor_wrapper, sock, our_func, *args))```
4. Создаем asyncio.Future в недрах эвент лупа. Когда эвент луп прочтет из сокета нужные байтики, он запушит в эту фьючу результат или исключение
5. Возвращаем пользователю эту фьючу

Таким образом, на самом деле, asyncio в работе с потоками просто эксплуатирует свои же механизмы I/O multiplexing. Легко видеть, что можно ровно всю ту же логику написать целиком на C++, избавившись от всех недостатков кровосмешения:
1. Регистрируем некий "системный" unix domain socket в нашем event loop'e и запускаем background корутину, которая будет разгребать данные из него.
2. py_thread_pool -> C++ thread pool
3. Python функция out_func -> C++ функтор, который мы создаем в питоне с помощью pybind11
4. Оборачивать в функцию, пишущую в сокет, тоже будем уже в C++. Запись в сокет будет производиться из C++ кода, надо только передать нужный нам файловый дескриптор
5. Когда запушим функтор в C++ тредпул, на стороне питона зарегистрируем фьючу, ждущую из сокета определенный набор байтиков, и отщелкнем ее в python-side, когда джоба выполнится

Такая схема лечит все вышеперечисленные проблемы: легко профилировать C++ и python код, нет проблем с GIL, нормальная многопоточность.

### Интерфейс
Python-side интерфейс - это [cpp_threaded_worker](/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/tools/cpp_async_threaded.py). В конструктор мы передаем Python handler с C++ тредпулом. Метод ```__call__``` принимает C++ функтор, проделывает все шаги выше и возвращает нужную нам фьючу.
Детали реализации под капотом:
1. [signal_socket_bus](/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/tools/signal_socket_bus.py) - синглтон, держащий нужный нам сокет и регистрирующий обернутые фьючи
2. [cpp_thread_bridge](/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/cpp_lib/threading) - C++-side код в pybind, позволяющий передавать функторы в тредпул и оборачивающий их в запись в сокет

### Как программировать свои функторы
Самая главная особенность - в тредпул пушится **shared_ptr на функтор**. Никакой move/reference семантики тут нет. Причина заключается в том, что наш функтор, по сути, должен жить в двух рантаймах, питоновском и C++. Если что-то где-то пойдет не так, эти рантаймы могут начать независимую подчистку за собой

## StringHandle: работа с байтами между python/C++
Один из важнейших кусков стриминга с/на YT. Работать с сырыми байтиками при потоках в гигабайт в секунду в основном потоке уничтожает производительность всей системы. Более того, хочется, чтобы данные из C++ можно было использовать в python без копирований/созданий py::bytes, который опять-таки блокирующий.

### StringHandle
Обертка над различными классами-хэндлерами строк. Сейчас там под капотом variant из:
1. ```(cpp)py::bytes``` - питон строка
2. ```(cpp)std::shared_ptr<std::string>``` - C++ строка
3. ```(cpp)torch::tensor[uint8_t]``` - PyTorch тензор
**ВАЖНО**: предполагается, что StringHandle содержит shared/intrusive pointer'ы на внутренние строки. Он, как и функторы, передается by value между py/c++, чтобы разделить владение ресурсом.

Тензор здесь нужен затем, что в PyTorch из коробки работает shared_memory. Чтобы избежать передачи толстых данных по сокетам из процесса в процесс, можно класть их в shared_memory тензор. Далее можно просто в разных процессах делать на него view из StringHandle'ов.

### BufferProtocol/memoryview
[pybind11 buffer protocol](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/cpp_lib/yt/libtorch_yt_tools.cpp?rev=r8133373#L123). BufferProfotol в Python нужен, чтобы протаскивать какие-то низкоуровневые объекты в python вьюшки памяти, в частности, [memoryview](https://docs.python.org/3/library/stdtypes.html#memoryview). Хорошие библиотеки, работающие с байтами, умеют работать не только с ```bytes```, но и с ```memoryview```, к таким библиотекам относится aiohttp. BufferProtocol позволяет в параллельном C++ коде формировать некоторые блобы и отсылать их по http **без копирований и блокирующих созданий bytes**. На этом принципе работает вся отгрузка данных в YT. [Пример](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/yt/uploader.py?rev=r8133373#L198)

## TensorPipe
Рабочая лошадка для передачи тензоров между подпроцессами, один из основных примитивов, позволяющих быстро обучаться в multiprocessing.

### CPU: SharedMemory
```torch.Tensor``` из коробки поддерживает аллокацию в ```//dev/shm```. PyTorch при этом сам следит за тем, чтобы подчищать открытые дескрипторы shm и т.д. Если тензор находится в shared memory, то можно организовать zero-copy передачу данных между двумя процессами:
1. В первый раз посылаем тензор по multiprocessing.Queue. Это медленная операция, но ее нужно проделать один раз. Читаем тензор в другом процессе
2. В следующие разы просто пишем данные в тензор. Они сразу будут доступны в соседнем процессе

### GPU: CudaSharedMemory
**Все** cuda-тензоры в PyTorch по дефолту shared. Для них справедлива вся та же логика, что и для CPU, за исключением одной важной детали: синхронизация CUDA Stream перед посылкой сигнала другому процессу (напомним, вся работа с GPU асинхронная).

### NestedTensorStructure
До сих пор мы передавали только одиночные тензоры в пайпах. Очевидно, это не самый удобный способ коммуникации. Для этого мы разрешаем передавать NestedTensorStructure. Это:
1. None
2. torch.Tensor
3. Python-коллекции ```list[nested_tensor_structure], tuple[nested_tensor_structure, ...], dict[str, nested_tensor_structure]```. Коллекции должны быть ordered, чтобы можно было воспроизводимо zip-нуть по двум коллекциям.
4. dataclass, в котором все поля являются nested_tensor_structure

Ниже - все примеры nested_tensor_structure:
```python
s1 = None
s2 = torch.rand(100)
s3 = [s1, s2, torch.rand(10)]
s4 = [s1, s2, {"x1": torch.rand(10)}, [torch.rand(50, 60)]]

import dataclasses

@dataclasses.dataclass
class NestClass:
    x1: List[torch.Tensor]
    x2: Dict[str, torch.Tenso]

NestClass(x1=[torch.rand(1)], x2={"a": torch.rand(2, 3)})
```

### Эффективность передачи nested_tensor_structure между процессами
1. TensorPipeWriter в методе coro_send сначала сравнивает **структуру** nested_tensor_structure со своим внутренним состоянием.
Если структуры разные - посылает nested_tensor_structure по тормозной очереди

Если структуры одинаковые - смотрит, может ли он сериализовать каждый тензор в новой структурке в структуре состояния:
1. **Zero-copy**: если storage тензора-входа совпадает со storage тензора в состоянии, то просто запоминаем метаинформацию-вьюшку
2. **Copy**: если storage не совпадают, но размер входного тензора меньше размера в тензоре состояния
3. **Queue**: если входной тензор больше тензора-состояния. В этом случае принимающий процесс должен прочесть дескриптор нового увеличенного буфера-тензора

Первые два пункта могут разниться от тензора к тензору внутри одной nested_structure. Если же случился хотя бы один Queue - посылается сразу все. Простейший совет по эффективности такой: не меняйте структуру тензора. В остальном TensorPipe, в общем-то, справится сам: при необходимости перепослать тензор по очереди из-за маленького буфера он выделит буфер с запасом, чтобы пореже так делать.

### Часто возникающие проблемы
#### Чтение CUDA тензоров из очереди в посылающем процессе
Нельзя читать cuda тензор из очереди в том же процессе:
```python
import torch
import multiprocessing

t = torch.tensor([1, 2, 3]).cuda()
queue = multiprocessing.Queue()
queue.put(t)
# Segmentation fault
t1 = queue.get()
```

То же самое автоматом применяется на tensor pipe:
```python
import torch
from ads_pytorch.model_calcer.utils.tensor_pipe import TensorPipeReader, TensorPipeWriter
async def main(reader: TensorPipeReader, writer: TensorPipeWriter):
    tt = torch.tensor([1, 2, 3]).cuda()
    await writer.coro_send(tt)
    # Segmentation fault
    tt2 = await reader.coro_recv()
```

## BaseAsyncWorkerPool
Асинхронный пул stateful воркеров. Пользоваться надо так:

```python
pool = MyWorkerPool(2)
async with pool:
    future1 = await pool.assign_job(1)
    future2 = await pool.assign_job(2)
    future3 = await pool.assign_job(3)
```

Что тут происходит:
1. ```async with pool``` -  входим в контекст. Гарантируется, что в WorkerPool джобы исполняются **только** внутри контекста. При выходе из контекста ```__aexit__``` пул ждет всех воркеров. После выхода из асинхронного контекста в пуле ничего не происходит
2. ```assign_job(*args, **kwargs)``` - форвардит данные аргументы любому свободному воркеру. Возвращает future на результат. **assign_job возвращает сразу после того, как смог найти свободный воркер и передать ему джобу. Блокируется до тех пор, пока все воркеры заняты**.

**Политика исключений**. При любом непойманном исключении в любом воркере pool войдет в режим ```die_mode``` и начнет выбрасывать **это же исключение** на любую попытку вызова метода assign_job, а также при выходе из асинхронного контекста. Происходит это по следующей причине: если писать каждую ошибку в разных местах, пользователи обучалки начинают охреневать от происходящего. Здесь же мы не печатаем явным образом ни одно исключение ни в одном воркере. Вместо этого, мы начинаем швырять его во всех местах и рано или поздно оно выбросится в основной управляющей корутине. Ни в каких других местах мы также исключения не печатаем. Таким образом, мы реализовывает надежный отстрел всего обучения вкупе с чистыми и понятными stderr логами. Альтернативой являются exception_handler'ы в event_loop, но у них тонна недостатков, про это неплохо написано [вот тут](https://www.roguelynn.com/words/asyncio-exception-handling/).

## [ExtendableStream](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/tools/extendable_stream.py)

Абстракция над ```AsyncIterable``` объектом, позволяющая доливать в него данные или выбрасывать исключения в вызывающем коде. Избавляет озера от необходимости самому ручками настраивать event'ы и пр.

С пользовательской стороны есть следующие методы:
1. ```put```: положить что-то в стрим. Метод **обычный**, не async - для реализации асинхронного ожидания каких-то данных можно класть future и await'ить, пример будет ниже
2. ```stop```: сказать стриму, что больше новых данных не будет. После команды ```stop``` вызовы метода ```put``` будут бросать исключения. Более привычный аналог в низкоуровневых стримах байтов будет посыл EOF.
3. ```throw```: выбросить исключение в стрим. Если мы выбрасываем в стрим исключение, это исключение затем выбрасывается в коде, который итерирует по стриму. Это механизм передачи ошибок от producer'a данных, кладущего сюда данные через ```put```, consumer'у
4. ```cancel```: по факту легами, просто делает ```stream.throw(asyncio.CancelledError)```
5. ```__aiter__ & __anext__```: consumer-side код, читает из стрима. Привычный питонячий интерфейс итератора

### Пример
```python
import dataclasses
import collections
from ads_pytorch.tools.extendable_stream import BaseAsyncExtendableStream

# Мы назвали его Sorted, потому что он выдает данные в том же порядке, в котором мы их пушим
@dataclasses.dataclass
class SortedExtendableStream(BaseAsyncExtendableStream):
    queue: collections.deque = dataclasses.field(init=False, default_factory=collections.deque)
    def _async_iterator_put_impl(self, data):
        self.queue.append(data)

    async def _async_iterator_next_impl(self):
        return self.queue.popleft()

    def _empty_impl(self) -> bool:
        return len(self.queue) == 0


stream = SortedExtendableStream()


async def producer(stream):
    try:
        for i in range(10):
            stream.put(i)
    except Exception as ex:
        stream.throw(ex)
        raise
    else:
        stream.stop()

loop = asyncio.get_running_loop()
loop.create_task(producer(stream))
async for x in stream:
    print(x)  # 1, 2, ... 9
```

Особенности:
1. Инстансы ExtendableStream должны быть проитерированы **ровно один раз**. Они не предназначены для множественного использования. Метод [__aiter__](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/tools/extendable_stream.py?rev=r6223500#L43) возвращает самого себя. Вот так делать нельзя:
```python
import asyncio
stream = MyExtendableStream()

async def _iterate_foo(stream):
    # Вот тут в обеих корутинах мы в методе __aiter__ вернем self, значит, итератор будет один и тот же в двух корутинах.
    # На практике эффект будет такой: мы хрен пойми как разделим поток между двумя корутинами. Сплит итерируемых сущностей
    # из одного стрима по нескольким обработчикам надо делать по-другому
    async for r in stream:
        print(r)

# ПЛОХО! Один и тот же стрим в двух параллельных корутинах!
await asyncio.gather(
    _iterate_foo(stream),
    _iterate_foo(stream)
)
```
