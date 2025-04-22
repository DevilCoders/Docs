# doberman
Production successor of mail/coon - shared folders synchronization service.

### Monitorings
* [Оповещения от Juggler](https://juggler.yandex-team.ru/?query=host%3Dqloud-ext.mail.doberman-corp.production.doberman%7Chost%3Dqloud-ext.mail.doberman-corp.prestable.doberman&view=tiles&limit=40)

* Графики в Golovan:
  * [Графики по ошибкам](https://yasm.yandex-team.ru/template/panel/doberman_log_errors)
  * [Графики по данным профилировщика](https://yasm.yandex-team.ru/template/panel/doberman_pa)
* Графики в Graphite:
  * [Графики по ошибкам](https://gr-mg.yandex-team.ru/dashboard/#mail_doberman_corp_log)
  * [Графики по данным профилировщика](https://gr-mg.yandex-team.ru/dashboard/#mail_doberman_corp_pa)
  * [Графики по статистике от добермана](https://gr-mg.yandex-team.ru/dashboard/#mail_doberman_corp_stat)

```
.
├── docker
│   └── base
│       ├── etc
│       │   └── monrun
│       │       └── doberman
│       │           ├── MANIFEST.json
│       │           ├── log_events.py
│       │           └── stat_events.py
│       └── usr
│           ├── local
│           │   └── doberman
│           │       ├── daemons
│           │       │   ├── stat_logger.py
│           │       │   └── unistat.py
│           │       ├── graphite_dasboard_log.json
│           │       ├── graphite_dasboard_pa.json
│           │       ├── graphite_dasboard_stat.json
│           │       └── python
│           │           ├── i_doberman_log.py
│           │           ├── i_doberman_pa.py
│           │           ├── i_doberman_stat.py
│           │           └── i_sharpei_stat.py
│           └── share
│               └── graphite-client
│                   ├── doberman_log.py
│                   ├── doberman_pa.py
│                   └── doberman_stat.py
└── tests
    └── monitorings
        ├── test_doberman_log_graphite.py
        ├── test_doberman_log_juggler.py
        ├── test_doberman_log.py
        ├── test_doberman_pa_graphite.py
        ├── test_doberman_pa.py
        ├── test_doberman_stat_graphite.py
        ├── test_doberman_stat.py
        └── test_sharpei_stat.py
```

Источники информации для мониторингов:
1. **log** - лог добермана (/var/log/doberman/doberman.tskv) - статистика по возникающим ошибкам ошибками
2. **pa** - лог профилировщика (/var/log/doberman/profiler.log) - статистика по выполняемым операциям
3. **stat** - ручка stat - статистика по имеющимся подключениям

* `./docker/base/usr/local/doberman/python/` - общие файлы (функции для чтения и парсинга логов, вызова ручек, построения статистики)
* `./docker/base/etc/monrun/doberman/` - скрипты, формирующие данные в формате juggler'а (используют общие функции для получения статистики)
* `./docker/base/usr/share/graphite-client/` - скрипты, формирующие данные в формате graphite'а (используют общие функции для получения статистики)
* `./docker/base/usr/local/doberman/daemons/stat_logger.py` - сохранение результатов stat в лог
* `./docker/base/usr/local/doberman/daemons/unistat.py` - HTTP сервер, реализующий ручку unistat на порту 26010 (для Golovan)
* `./docker/base/usr/local/doberman/*.json` - просто сохранил dahboard'ы для графита
* `./tests/monitorings/` - тесты, запускаются по цели monitorings-check:

```
$ make -j16 -C build monitorings-check
========================= test session starts =========================
platform linux2 -- Python 2.7.6, pytest-3.2.0, py-1.4.34, pluggy-0.4.0
rootdir: /home/gzalex/workspace/src/doberman, inifile:
collected 65 items 

../../tests/monitorings/test_doberman_log_graphite.py .
../../tests/monitorings/test_doberman_log_juggler.py ....
../../tests/monitorings/test_doberman_log.py .................
../../tests/monitorings/test_doberman_pa_graphite.py .
../../tests/monitorings/test_doberman_pa.py ..........
../../tests/monitorings/test_doberman_stat_graphite.py .
../../tests/monitorings/test_doberman_stat_juggler.py ...............
../../tests/monitorings/test_doberman_stat.py ......................
../../tests/monitorings/test_sharpei_stat.py .........
../../tests/monitorings/test_stat_logger.py ..
../../tests/monitorings/test_unistat.py ....

====================== 86 passed in 0.22 seconds ======================

```
