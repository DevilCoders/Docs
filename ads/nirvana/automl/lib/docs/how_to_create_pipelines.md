# Как создавать пайплайны?

Весь код с интерфейсом/запускалками пайплайнов лежит в библиотеке [batch_processor](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/automl/lib/batch_processor).

## Toolchain

В библиотеке интенсивно используются следующие библиотеки:
1. trollius - бекпорт библиотеки [asyncio](https://docs.python.org/3/library/asyncio.html) на python 2.7. С ней можно не знакомиться - в библиотеке есть полноценный синхронный API, позволяющий пользоваться уже имеющимися процессорами и создавать новые процессоры через обычное питоновое API без корутин
2. attr - библиотека датаклассов. [dataclasses](https://docs.python.org/3/library/dataclasses.html) выросли именно из библиотеки attr. Рекомендуется к ознакомлению в любом случае

## Создание блоков пайплайнов

В первую очередь необходимо ознакомиться с [интерфейсом](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/automl/lib/batch_processor/interface.py). Там есть два класса: ```AbstractBatchProcessor``` и ```BatchProcessorResultHandle``` .

### AbstractBatchProcessor

AbstractBatchProcessor - это абстракция над асинхронным обработчиком задач. Является главной единицей исполнителя кода в пайплайне. Каждый обработчик задач (т.е. каждый наследник AbstractBatchProcessor) может выполнять только один вид задач. Каждой задаче соответствует свой дескриптор задачи - некий питонячий объект, содержащий исчерпывающую информацию о том, как нужно исполнять задачу. 

* feed_new: попросить исполнить какие-то джобы. Принимает на вход дескрипторы задач
* get_ready: взять уже готовые результаты. Возвращает ```Set[BatchProcessorResultHandle]```. Гарантируется, что любая future уже выполнена

Остальные методы служат для убийства/остановки процессора и проверки его состояния, их документацию лучше смотреть в коде. Конечному пользователю они понадобятся только в крайнем случае.

### BatchProcessorResultHandle

Инстанс, который возвращается из ```AbstractBatchProcessor``` для задачи, исполнение которой завершено. Завершено - значит:
* Успешно выполнено
* Упало
* Было отменено (во время исполнения либо до него)

Содержит в себе два поля: 
* ```descriptor``` - Дескриптор задачи, результаты которого содержатся в данном handle
* ```future``` - объект trollius.Future. Он подчиняется стандартному интерфейсу future, описанному в библиотеке ```concurrent.futures```

С точки зрения потребителя результатов какого-то ```AbstractBatchProcessor```, для future имеет смысл вызывать только методы ```.result()``` и ```.exception()```. 

Метод ```.result()``` отдает результат, если задача была выполнена успешно, в противном случае бросает исключение, выброшенное при исполнении задачи. Если исполнение задачи было отменено (в документации по trollius/asyncio это cancelled), то будет выброшен ```trollius.CancelledError```.

Метод ```.exception()``` выдает исключение, если задачу упала, либо None, если задача выполнена успешно. Полезно, чтобы отсеять успешные/неуспешные результаты.

## Связывание блоков пайплайна и их запуск

Тут надо ознакомиться с [кодом запуска](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/automl/lib/batch_processor/execution.py).

```AbstractBatchProcessor```'ы могут быть легко скомбинированы в виде стандартного dataflow graph. Каждый процессор может много раз принимать на вход новые джобы и много раз отдавать уже выполненные другим процессорам, все это - полностью асинхронно. Управление тем, когда и как группируются результаты процессоров, определяет пользователь в своей реализации процессора.

**Можно ли граф из процессоров вывезти в Нирвану с сохранением асинхронности?** Да, можно, если отказаться от циклов. Стримовое API в Нирване есть, но оно непубличное и пользуется им вроде как только Hitman. Можно каким-то образом поддержать его в Вальхалле. Скорее всего, это будет совсем новое API, так как стримовые операции - это генераторы, а не функции.

### BatchProcessorsGraph

```BatchProcessorsGraph``` - это пользовательский интерфейс для создания dataflow graph'а из ```AbstractBatchProcessor```. Имеет два метода:
* ```add_processor``` - добавить один процессор в граф
* ```add_connected_processors``` - добавить два процессора и функцию преобразования данных между ними

При попытке добавить один и тот же процессор дублирования в графе не произойдет.

Функция преобразования принимает на вход ```BatchProcessorResultHandle```'ы из source-процессора и возвращает список дескрипторов задач для destination процессора

Пример:
```python
from ads.nirvana.automl.lib.batch_processor import BatchProcessorsGraph, BatchProcessorResultHandle
graph = BatchProcessorsGraph()
my_processor = Processor()

# instance of my_processor will be added only once
for _ in range(3):
    graph.add_processor(my_processor)
    
def my_converter(*handles):
    # type: (*BatchProcessorResultHandle) -> Any
    return [h.future.result() for h in handles]

# Добавит вилку - результаты процессора поедут на вход каждому из дочерних процессоров
destination_processors = [Processor() for _ in range(3)]
for dst in destination_processors:
    graph.add_connected_processors(my_processor, dst, my_converter)
```

За более интересными (а главное - поддерживающимися в рабочем состоянии) примерами - идите и смотрите на [тесты](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/automl/lib/batch_processor/ut/test_execution.py)

### Запуск

Весь API для запуска сейчас синхронный. Есть три метода:
* [run_batch_processors_graph](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/automl/lib/batch_processor/execution.py?rev=5058684#L48) - запустить асинхронный граф процессоров. Возвращает словарь вида "процессор -> список BatchProcessorResultHandle".
* [run_batch_processor](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/automl/lib/batch_processor/execution.py?rev=5058684#L68) - запустить один процессор. Возвращает список BatchProcessorResultHandle.
* [run_batch_processor_single](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/automl/lib/batch_processor/execution.py?rev=5058684#L88) - запустить процессор с одним дескриптором. Странное легаси, надо выпилить, но мне лень.

Примеры запусков - в [тестах](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/automl/lib/batch_processor/ut/test_execution.py)

# Как писать новые batch_processor'ы без корутин

В asyncio есть замечательный метод [loop.run_in_executor](https://docs.python.org/3/library/asyncio-eventloop.html#id14). Этот метод позволяет запустить обычную питонофункцию в каком-нибудь пуле потоков/процессов (как правило, это пулы из ```concurrent.futures```), и корректно подождать результатов исполнения в асинхронном коде.

В библиотеке уже есть специализированные базовые классы, инкапсулирующие в себе весь корутинный код:
* [SeparateBatchProcessorSynchronous](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/automl/lib/batch_processor/separate.py?rev=5058684#L39)
* [SequentialBatchProcessorSynchronous](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/automl/lib/batch_processor/sequential.py?rev=5058684#L154)

Пример:
```python
from ads.nirvana.automl.lib.batch_processor import SeparateBatchProcessorSynchronous, run_batch_processor_single
from ads.nirvana.automl.lib.util import UnsafeThreadPoolExecutor

class SomeSeparateProcessor(SeparateBatchProcessorSynchronous):
    @property
    def _executor(self):
        # We create a new separate thread for each job
        return UnsafeThreadPoolExecutor(1)
        
    def _run_one_job_synchronous(self, job_descriptor):
        # type: (int) -> int
        return job_descriptor + 1

if __name__ == '__main__':
    res = run_batch_processor_single(
        batch_processor=SomeSeparateProcessor(),
        descriptor=25
    )
    print(res.descriptor)
    print(res.future.result())
```
