# Исключения в модулях

Из модуля можно выбрасывать любые исключения. Все они будут сериализованы в строку при передаче на сервер,
кроме тех, что явно перечислены в
[этом](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/core/utils/exceptions.py) файле.

При использовании cython **необходимо** помечать плюсовые методы как `except +`
и добавлять обработчик исключений
[raisePyError](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/sdk/cython/exceptions.pxd?#L6).
Он нужен для корректной работы исключений, обрабатывающихся особым образом.
Пример использования есть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/ymapsdf/lib/geometry_collector/mapreduce.pyx?#5).

Общая рекомендация - использовать в плюсовом коде исключения, которые являются наследниками `maps::Exception`, потому как
обработчик в таком случае будет сохранять стек-трейс. Для того, чтоб стектрейс писался, необходимо в `ya.make` для бинарника
модуля указать опцию `ENABLE(NO_STRIP)`.

Далее перечислены исключения, обрабатывающиеся особым образом

## RetryTaskError

При получении исключения, не подразумевающего перезапуск, задача будет помечена неуспешной, а весь билд завершится с ошибкой.
Если есть необходимость перезапустить задачу, то необходимо выбрасывать исключение
[RetryTaskError](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/sdk/core/exceptions.py?#L29)

```python
from maps.garden.sdk.core import GardenError, RetryTaskError
raise RetryTaskError(exc=GardenError("This task must be retried"))
```

или же оборачивать метод `__call__()` в задаче декоратором
[retry](https://a.yandex-team.ru/arc/trunk/arcadia/maps/pylibs/utils/lib/common.py?#L172).

```python
from maps.pylibs.utils.lib.common import retry
from maps.garden.sdk.core import Task

class MyTask(Task):
    @retry(exceptions=(ExceptionClass1, ExceptionClass2))
    def __call__(self, res1, res2):
        pass
```

Так же задача будет автоматически перезапущена, если появится исключение,
связанное с недоступностью/проблемой YT или каких-то ресурсов Кипариса, которое было брошено из библиотеки yt.wrapper.

## AutotestsFailedError

[AutotestsFailedError](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/sdk/core/exceptions.py?#L68)
используется для индикации некорректности данных.

**Python**

```python
from maps.garden.sdk.core import AutotestsFailedError
raise AutotestsFailedError("Input data is invalid, id = 123321")
```

**C++**

```cpp
#include <maps/garden/sdk/cpp/exceptions.h>
throw maps::garden::AutotestsFailedError("Input data is invalid, id = 123321")
```

При возникновении такого исключения для соответствующего билда будет загораться
другой мониторинг [TODO](https://st.yandex-team.ru/MAPSGARDEN-18565).
Если исключение брошено в продакшен-окружении Огорода, то Огород автоматически
создаст тикет в очереди MAPSLSR вместо того, чтобы создать тикет в очереди
MAPSGARDEN.


## DataValidationWarning
[DataValidationWarning](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/sdk/core/exceptions.py?#L78)
используется для индикации некорректности данных. Использование аналогично AutotestsFailedError, но, в отличие от него,
может быть проигнорировано. В этом случае билд будет помечен как успешный.

{% note warning "Attention" %}

Таска, в которой выбрасывается исключение DataValidationWarning, не должна производить ресурсы,
которые будут использоваться другими тасками.
При возникновении исключения никакие ресурсы не будут созданы, соответственно, зависящие таски не будут запущены.

{% endnote %}


**Python**

```python
from maps.garden.sdk.core import DataValidationWarning
raise DataValidationWarning("Input data is invalid, id = 123321")
```

Так же для Python существует функция [add_validation_task()](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/sdk/extensions/validation_tools.py?#L33),
которой можно передать список ресурсов для валидации и функцию валидации. Пример:
```python
def _validation_function(example_map_output: PythonResource):
    # do some validation
    # ...

    if is_data_wrong():
        raise DataValidationWarning("wrong data")

add_validation_task(
    graph_builder=graph_builder,
    validation_function=_validation_function,
    example_map_output="example_map_output",
)
```

**C++**

```cpp
#include <maps/garden/sdk/cpp/exceptions.h>
throw maps::garden::DataValidationWarning("Input data is invalid, id = 123321")
```

Ошибку DataValidationWarning можно проигнорировать на страничке со всеми ошибками билда:

![](img/not_ignored.png)

После нажантия на кнопку `ignore` ошибка будет отображаться так:

![](img/ignored.png)

А билд, соответственно, станет завершённым.

{% note info %}

Если билд ещё пока выполняется, но ошибка DataValidationWarning уже возникла, и её проигнорировали,
то это действие можно отменить.

Если билд уже успешно завершился, то отменить игнорирование нельзя.

{% endnote %}
