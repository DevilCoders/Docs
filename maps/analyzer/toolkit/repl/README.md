### repl анализатора
---
Уже включены в `PEERDIR` и импорнуты популярные библиотеки анализатора (см. [`maps/analyzer/toolkit/lib/prelude.py`](../lib/prelude.py)).

Правильный способ запуска: `Y_PYTHON_ENTRY_POINT=:repl ./repl`.

---

IPython можно запускать с любым бинарем, достаточно лишь добавить в `PEERDIR` путь до ipython: `contrib/python/ipython`.<br>
Запуск: `Y_PYTHON_ENTRY_POINT=:repl ./your_binary_file`.

Чтобы не писать всегда `Y_PYTHON_ENTRY_POINT=:repl` можно сделать специальный скрипт, аргументом которого будет путь до бинаря.
Скрипт может выглядеть так:
```bash
#!/bin/bash
Y_PYTHON_ENTRY_POINT=:repl "$@"
```
Добавьте его в `/home/your_username/bin/`, например, с названием `dev`.<br>
Тогда запускать `ipython`-версию вашего бинаря следует так: `dev ./your_binary_file`.
