## DAAS


Сервис для сбора и обработки данных с маркетных источников.

#### Установка и запуск

Лучше всего все действия для установки проводить на виртуалке, например из cloud.yandex-team.ru.
Для корректной работы с репортами у пользователя robot-market-daas должны быть ssh-ключи на сервере.
Для работы с Yt у пользователя robot-market-daas должен быть токен https://wiki.yandex-team.ru/yt/gettingstarted/ (Роботные токены, п.2-5)

```# su robot-market-daas``` # Создать директорию пользователя

```robot-market-daas:~$ exit```

```# apt-get install -y git libxml2-dev libxslt1-dev python-dev zlib1g-dev python-pip gcc-multilib g++-multilib nginx subversion executer-perl```

```# pip install virtualenv```

```# mkdir /mnt/daas``` # Место где будут храниться все данные.

```# chown robot-market-daas:dpt_virtual_robots /mnt/daas```

```# ln -s /mnt/daas /var/lib/daas```

```# su robot-market-daas```

```robot-market-daas:~$ git clone git@github.yandex-team.ru:ld86/daas.git```

```robot-market-daas:~$ svn checkout svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/market/tools/develop/outcmp/dolbilo daas/daas/external/dolbilo```

```robot-market-daas:~$ svn checkout svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/market/tools/develop/report_deploy daas/daas/external/report_deploy```

```# cp /home/robot-market-daas/daas/nginx/daas /etc/nginx/sites-enabled/```

```# service nginx restart```

```robot-market-daas:~/daas$ virtualenv -p python2.7 env```

```robot-market-daas:~/daas$ source env/bin/activate```

```(env)robot-market-daas:~/daas$ pip install -r daas/requirements.txt```

```(env)robot-market-daas:~/daas$ pip install -i https://pypi.yandex-team.ru/simple/ yandex-yt```

```(env)robot-market-daas:~/daas$ mkdir /var/lib/daas/{db,tasks,yt_tasks,diffs,files,reports,serps,static,cluster_store,rb_report_path}```

```(env)robot-market-daas:~/daas$ mkdir /var/log/daas```

```(env)robot-market-daas:~/daas$ python daas/main.py```

Нужен пароль для чтения из Clickhouse в файле /home/robot-market-daas/.clickhouse_password.txt - можно взять у popov-ng@ или a-bocharov@ (выдавали в тикете https://st.yandex-team.ru/MARKETINFRA-4071)


#### FAQ

Если при управлении репортом возникают ошибки в логе:

```
FetchingReportError: Failed to run ['scp', '-o', 'StrictHostKeyChecking=no', u'dev-rep01wd.market.yandex.net:/home/a-bocharov/arcadia/market/report/report_bin/report_bin', '/var/lib/daas/reports/report_bin_1'] with code 1, err: "scp: /home/a-bocharov/arcadia/market/report/report_bin/report_bin: Permission denied
"
```
У robot-market-daas не хватает прав, чтобы достать этот файл. Попробуйте положить бинарник в ```/tmp/<FILENAME>```.

```
robot-market-daas@msh01hd.market.yandex.net! sudo: no tty present and no askpass program specified
                                     shmyax! Child for robot-market-daas@msh01hd.market.yandex.net exited with status 1
```
На хосте нет sudo для выполнения команды executer'ом. На данный момент sudo есть только на группе машин conductor.market_search-devel (msh{01..08}hd).

```
robot-market-daas@msh01hd.market.yandex.net! sudo: no tty present and no askpass program specified
                                     shmyax! Child for robot-market-daas@msh01hd.market.yandex.net exited with status 1
```
Хоста нет в ```~robot-market-daas/.ssh/known_hosts```. Нужно сходить пользователем robot-market-daas по ssh на нужный хост с daas-машины, чтобы он добавился в ```known_hosts```.

