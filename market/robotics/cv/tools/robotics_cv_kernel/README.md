Jupyter kernel with arcadia python3 and Robotics CV modules
======================

**HOWTO**: https://wiki.yandex-team.ru/jupyter/docs/customarcadiakernel/

1. Собрать kernel (если виртуалка слабая, то использовать лучше внешний сервер, а потом нести бинарь в виртуалку с Jupyter):

* `ya make`

2. Установить jypyter kernel (с мощной виртуалки):

* `make`

3. Готово, можно запускать jupyter ноутбуки

Пример использования представлен в файле [example_kernel_usage.ipynb](example_kernel_usage.ipynb). 

В ноутбуке открывается TSV разметка и демонстрируется возможность использования нашей либы для чтения разметки из Толоки.

