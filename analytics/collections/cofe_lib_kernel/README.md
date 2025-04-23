Jupyter kernel with arcadia python and modules
======================

https://wiki.yandex-team.ru/users/deshevoy/Arcadia-IPython-Kernel-for-Jupyter/

1. Собрать kernel с python2, collections_cofe_lib и полезными модулями:

* `ya make -r analytics/collections/cofe_lib_kernel --checkout`

2. Установить jypyter kernel:

* `make`

3. Готово, можно запускать jupyter ноутбуки

Пример работы с объектной моделью и расчётом метрик в [cofe_lib_arcadia.ipynb](cofe_lib_arcadia.ipynb) который формирует табличку:
![Alt text](https://jing.yandex-team.ru/files/nerevar/2019-05-18_collections_-_Navigation_-_Hahn_2019-05-20_19-01-31.png)
