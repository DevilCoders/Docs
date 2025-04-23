Архитектура
===========

Вся логика по отправке данных в статистику находится в файле ``rep/common.py``.
Но суть проста:

  * взять данные из БД
  * добавить к полученным данным мета описание отчета
  * сделать HTTP POST запрос по URL статистики

В настоящий момент есть 2 поднятых сервиса статистики:

  * [Продакшен](https://stat.yandex-team.ru)
  * [Тест](https://stat-beta.yandex-team.ru)

Деплоймент
==========

Все отчеты выезжают вместе со основным биллингом.
Собирается отдельный deb-пакет: ``yandex-balance-statreports``.
На сервер код «выезжает» в директорию:

  * ``/usr/share/python-support/balance-statreports``
  
Собирается пакет в TeamCity:

  * https://teamcity.yandex-team.ru/project.html?projectId=Billing_Reports_StatReports&tab=projectOverview

Как добавить новый отчет
========================

Чтобы добавить новый отчет, необходимо добавить python-скрипт в директорию
``rep``. Например, ``reps/CompletionsTotal.py``. Скелет скрипта:

```python
# -*- coding: utf-8 -*-
import common

class Updater(common.StatsReportUpdater):
    pass

if __name__ == '__main__':
    Updater().do()
```

Далее реализуем класс, унаследованный от ``common.StatsReportUpdater``.
В классе должно быть, как минимум, 2 переменные:

  * ``path`` — URL отчета в статистике (без хоста/порта)
  * ``header`` — список полей, которые будут отправлять в статистику

А так же необходимо реализовать 2 метода:

  * ``get_conf`` — конфигурация отчета для указанного среза (параметр ``scale``)
  * ``get_data`` — метод, возвращающий данные для отправки в статистику
                   (формат: значения, разделенные табуляцией)

Каждый отчет может быть представлен в 3 срезах:

  * ежедневный
  * еженедельный
  * ежемесячный

См. ``StatsReportUpdater.scales``. Тим среза в качестве параметра передается в
оба метода ``get_conf``/``get_data``.

Если для отчета нужные не все срезы, то необходимо в класс добавить список,
описывающий нужные срезы. Например, для дневного и месячного срезов,
необходимо добавить:

```python
class Updater(common.StatsReportUpdater):
    scales = ['daily', 'monthly']
```

Полный пример реализации отчета:

```python
class Updater(common.StatsReportUpdater):

    #: URI отчета.
    path = 'Completions/Total'

    #: Заголовок данных, передаваемых в статистику.
    header = ['fielddate', 'amt_rub']

    def get_conf(self, scale='daily'):
        conf = [
            "access_by_list: billing_stats",
            "dimensions:",
            "- fielddate: date",
            "graphs:",
            "- fields:",
            "  - amt_rub",
            "  title: Открутки",
            "  type: area",
            "measures:",
            "- amt_rub: number",
            "titles:",
            "  amt_rub: открутки"
        ]
        if scale == 'daily':
            conf.append("  fielddate: день")
        if scale == 'weekly':
            conf.append("  fielddate: неделя")
        if scale == 'monthly':
            conf.append("  fielddate: месяц")
        return conf

    def get_data(self, scale='daily'):
        trunc_mask = {
            'daily': 'DD',
            'weekly': 'IW',
            'monthly': 'MM'
        }

        # запрос на получение данных
        q = """
        select to_char(trunc(start_dt, '{mask}'), 'DD.MM.YYYY')   as fielddate,
               sum(completion_rub_sum_wo_nds)                     as amt_rub
          from bo.mv_compl_30_days h
         where start_dt >= trunc(sysdate - :days_ago, '{mask}')
         group by trunc(start_dt, '{mask}')
        """.format(mask=trunc_mask[scale])

        # данные
        d = ''
        for r in self.exc(q):
            d += '%s\t%s\n' % (r.fielddate, r.amt_rub)

        return d
```

Далее, необходимо добавить расписание для pycron'a:

```sql
-- Описание запуска
insert into bo.t_pycron_descr(
name,                           command,
timeout,
description,                    total_count,
terminate,                      owner_login)
values(
'statreports-completionstotal', 'yb-python -pysupport statreports/CompletionsTotal.py',
600,
'statreports-completionstotal', 1,
0,                              'shorrty');

-- Расписание запуска
insert into bo.t_pycron_schedule(name, crontab, enabled)
values('statreports-completionstotal', '0 7 * * *', 1);

commit;
```

Периодиность обновления данных
==============================

Периодичность обновления регулируется через [pycron](https://wiki.yandex-team.ru/balance/cron).

Конфигурационные файлы
======================

Каждый конфиг кладётся на каждый хост.

/etc/yandex/balance-statreports/statreports.cfg.xml
---------------------------------------------------

Это основной конфиг, который подключает все остальные конфиги.

/etc/yandex/balance-common/environment.cfg.xml
----------------------------------------------

Настройка окружения.

/etc/yandex/balance-common/statreports.cfg.xml
----------------------------------------------

Содержит настройки для отправки данных в статистику:

    * DaysAgo — за сколько дней отправлять данные в статистику. Данные
      переписываются.
    * StatRobotUser — логин пользователя, от имени которого отправляются данные
    * StatRobotPassword — пароль пользователя
    * StatBaseUrl — базовый URL статистики
    * StatSection — подраздел в статистике

/etc/yandex/balance-common/db-conn-statreports.cfg.xml
------------------------------------------------------

Содержит информацию о том, из какой БД забирать данные:

    * Host — хост БД
    * User — пользователь
    * Pass — пароль

Исходники
---------

Исходники конфигов находятся в текущем репо:

  * ``/common_config/(dev|test|prod)/``


Полезности
==========

Статус последнего обновления
----------------------------

Чтобы посмотреть статус последнего запуска, необходимо в БД Баланса выполнить:

```sql
select * from bo.v_pycron where name like 'statreports-%';
```

Как запустить руками обновление
-------------------------------

```bash
$ sudo su yb
$ . /etc/oraprofile
$ yb-python -pysupport statreports/DiscountsAvg.py
```

Возможные ошибки
================

Permission denied: '/var/log/yb/balance-statreports.log'
--------------------------------------------------------

Запуск выполняется от неверного пользователя. Необходимо делать это от
пользователя ``yb`` (см. выше)

ORA-12154: TNS:could not resolve the connect identifier specified
-----------------------------------------------------------------

Необходимо проверить строку подключения в конфиге:
``/etc/yandex/balance-common/db-conn-statreports.cfg.xml``
