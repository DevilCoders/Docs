Setup
=====

Для работы нужна утилита `tvmknife` или `ya`.

```sh
# You can use taxi-python3

taxi-python3 ldtool.py

# Or setup your of virtualenv:

sh setup-env.sh
./.venv/bin/python ldtool.py --help
```

Получение справки
=================

```sh
ldtool.py --help
usage: ldtool.py [-h] [-e {testing,production}] command ...

positional arguments:
  command
    bg-job-dump         Dump bg job
    bg-job-list         List background jobs
    bg-job-ctl          Update bp_settings
    bg-job-update       Update bp_settings
    bg-job-upsert       Direct job upsert
    bg-job-remove       Remove bg job

optional arguments:
  -h, --help            show this help message and exit
  -e {testing,production}, --environment {testing,production}
```

Получение списка задач
======================

```sh
ldtool.py -e testing bg-job-list
```

Получение конфигурации задачи
=============================

```sh
# bp_settings only
ldtool.py -e production bg-job-dump p2p_allocation_robot

# целико все тело
ldtool.py -e production bg-job-dump --full p2p_allocation_robot
```

Управление bg задачами
======================


```sh
# Включить
taxi-python3 ldtool.py -e testing bg-job-ctl --enable job_name

# Выключить
ldtool.py -e testing bg-job-ctl --enable job_name

# Привязать к хосту
ldtool.py -e testing bg-job-ctl --host-pattern sas job_name
```


Переключение трафика московского шарда на ПРЕ
=============================================

```sh
# Получаем имя ПРЕ хоста
$ nuter hostlist taxi_logistic-dispatcher_pre_stable
c6a34s6vosw5ootd.sas.yp-c.yandex.net

# Переключаем p2p_allocation_robot_msk на пре
$ ldtool.py -e testing bg-job-ctl --host-pattern c6a34s6vosw5ootd p2p_allocation_robot_msk

# Переключаем p2p_allocation_robot_msk обратно
$ ldtool.py -e testing bg-job-ctl --host-pattern '' p2p_allocation_robot_msk
```
