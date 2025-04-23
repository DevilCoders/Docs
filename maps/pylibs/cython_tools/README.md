# Библиотека для облегчения работы с cython

## Exceptions

Содержит в себе обработчик исключений `raisePyError()`. Использование:

```python
# in your .pyx file
from maps.pylibs.cython_tools.exceptions cimport raisePyError

# for some c++ imported functions:
   foo() except +raisePyError

# in your ya.make where is "PROGRAM()":

ENABLE(NO_STRIP)
```

В этом случае, исключения, которые выкинутся из функции будут обработаны функцией `raisePyError`.
1. У исключений-наследников `std::exception` `e.what()` упакуется в `RuntimeError` из `cython`
2. у исключений-наследников `maps::Exception` стектрейс сохранится в сообщение `RuntimeError` из `cython`
