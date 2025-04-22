# suburban_tasks
Скрипты для получения данных от РЖД

## ibm_db драйвер в Аркадии
https://st.yandex-team.ru/CONTRIB-926#5d544ad64b92d7001f15982d

Чтобы запустить бинарник локально:
- скачиваем архив библиотек драйвера из sandbox-ресурса для нужной оси https://a.yandex-team.ru/arc/trunk/arcadia/contrib/python/ibm-db/clidriver/ya.make
- разархивируем, получаем директорию clidriver
- при запуске бинарника устанавливаем перменную окружения, указывающую на путь к библиотеке:
Для linux: LD_LIBRARY_PATH=./clidriver/lib:$LD_LIBRARY_PATH
Для macos: DYLD_LIBRARY_PATH=./clidriver/lib:$DYLD_LIBRARY_PATH

Для MacOs:
Если не дает использовать либы из-за подписи
```
./clidriver/lib/libdb2.dylib: code signature in (./clidriver/lib/libdb2.dylib) not valid for use in process using Library Validation: library load disallowed by system policy
```
то заходим в настройки Security & Privacy, и там апрувим её. Это скорее всего потребуется для нескольких библиотек

## Тесты
Для запуска тестов требуется mongdb, mysql с правильной схемой базы, а так же shared library libdb2 под соотвествующую платформу.
Для этого используется bin/tests_recipe, он:
1) запускает базы с помоющью common_recipe
2) загружает схему базы как в common_recipe, но со схемой из другого ресурса
3) притаскивает libdb2 и устанавливает энв-переменные LD_LIBRARY_PATH/DYLD_LIBRARY_PATH

Ресурс схемы автоматом не обновляется, поэтому при изменениях схемы надо заливать его руками:
```
mysqldump -uroot rasp_rzd > schema_rzd_dump
gzip schema_rzd_dump
ya upload --type=RASP_MYSQL_SCHEMA_DUMP --owner=RASP --ttl=inf --attr environment="rzd_dev" schema_rzd_dump.gz
```

## Запуск миграций

В случае изменения схемы данных РЖД нужно будет применить миграции с локальной машины.
Минимально необходимый local_settings.py:

```python
from travel.rasp.suburban_tasks.settings import *  # noqa
from common.settings.configuration import Configuration

YANDEX_ENVIRONMENT_TYPE = 'testing' # testing либо production
YANDEX_DATA_CENTER = 'dev' # чтобы не ходить в кондуктор
DISABLE_GROUP_CACHES = True

import os
os.environ['RASP_GEOBASE_DATA_PATH'] = 'путь/до/geodata4.bin'
os.environ['RASP_VAULT_OAUTH_TOKEN'] = 'токен для доступа к секретнице'

Configuration().apply(globals())

from django.core.management.base import BaseCommand
BaseCommand.requires_system_checks = False  # отключаем проверки, иначе Django будет ругаться на отсутсвие urls.py
```

Запускается коммандой:

```shell script
DYLD_LIBRARY_PATH=./clidriver/lib:$DYLD_LIBRARY_PATH Y_PYTHON_ENTRY_POINT=travel.rasp.suburban_tasks.app:manage ./app migrate --database rasp_rzd
```

## Проверка РЖД-проксей
local_settings.py такие же, как для миграций.
```shell script
DYLD_LIBRARY_PATH=./clidriver/lib:$DYLD_LIBRARY_PATH Y_PYTHON_ENTRY_POINT=travel.rasp.suburban_tasks.app:rzd_check_connect ./app

============== check results:
connection to yr54jotahyqucbxx.sas.yp-c.yandex.net is successfull
connection to ojr22alewzntxria.vla.yp-c.yandex.net is successfull
connection to sscw57b5fzxjgtlj.man.yp-c.yandex.net is successfull
```


```
DYLD_LIBRARY_PATH=./clidriver/lib:$DYLD_LIBRARY_PATH Y_PYTHON_ENTRY_POINT=travel.rasp.suburban_tasks.app:rzd_check_data ./app

rzd_check_data from 2021-06-24 10:55:12.269883 to 2021-06-24 11:00:12.269883
Rows examples:
{'STNRASP': 941300, 'STOPER': 941009, 'NAMESTO': u'\u0425\u0418\u041b\u041e\u041a       ', 'NAMESTN': u'\u041c\u041e\u0413\u0417\u041e\u041d      ', 'NOMRP': 4, 'IDTR': 2004277, 'IDRASP': 2004278, 'DOR': 94, 'PRIORITY': '0', 'SOURCE': 1, 'NAMEP': u'                                                                                ', 'KODOP': 1, 'STNAME': u'\u0413\u042b\u0420\u0428\u0415\u041b\u0423\u041d                ', 'STNEX': 2050341, 'STOEX': 2050490, 'STOPEREX': 2050355, 'PRIORITY_RATING': '4', 'PRSTOP': '0', 'ID': 805809639, 'NOMPEX': u'6112          ', 'OTD': 1, 'KM': 17, 'TIMEOPER_F': datetime.datetime(2021, 6, 24, 10, 59), 'STORASP': 940909, 'TIMEOPER_N': datetime.datetime(2021, 6, 24, 11, 4)}
{'STNRASP': 941300, 'STOPER': 941009, 'NAMESTO': u'\u0425\u0418\u041b\u041e\u041a       ', 'NAMESTN': u'\u041c\u041e\u0413\u0417\u041e\u041d      ', 'NOMRP': 4, 'IDTR': 2004277, 'IDRASP': 2004278, 'DOR': 94, 'PRIORITY': '1', 'SOURCE': 2, 'NAMEP': u'                                                                                ', 'KODOP': 1, 'STNAME': u'\u0413\u042b\u0420\u0428\u0415\u041b\u0423\u041d                ', 'STNEX': 2050341, 'STOEX': 2050490, 'STOPEREX': 2050355, 'PRIORITY_RATING': '2', 'PRSTOP': '0', 'ID': 805809639, 'NOMPEX': u'6112          ', 'OTD': 1, 'KM': 17, 'TIMEOPER_F': datetime.datetime(2021, 6, 24, 10, 59), 'STORASP': 940909, 'TIMEOPER_N': datetime.datetime(2021, 6, 24, 11, 4)}
{'STNRASP': 36002, 'STOPER': 34702, 'NAMESTO': u'\u0421\u0418\u0412\u0415\u0420\u0421\u041a\u0410\u042f   ', 'NAMESTN': u'\u0421\u041f\u0431-\u0411\u0410\u041b\u0422\u0418\u0419\u0421\u041a', 'NOMRP': 11, 'IDTR': 2004399, 'IDRASP': 2043095, 'DOR': 1, 'PRIORITY': '1', 'SOURCE': 2, 'NAMEP': u'                                                                                ', 'KODOP': 1, 'STNAME': u'\u0412\u0415\u0420\u0415\u0412\u041e                  ', 'STNEX': 2004005, 'STOEX': 2004638, 'STOPEREX': 2005012, 'PRIORITY_RATING': '2', 'PRSTOP': '0', 'ID': 805809661, 'NOMPEX': u'6422          ', 'OTD': 2, 'KM': 34, 'TIMEOPER_F': datetime.datetime(2021, 6, 24, 10, 56), 'STORASP': 72507, 'TIMEOPER_N': datetime.datetime(2021, 6, 24, 10, 54)}
rows 865
```

## Именование переменных

У некоторых классов и аттрибутов имя представлено в верхнем регистре, частично или полностью.
Примеры:

 1. ``LGDPPR_SCALENDAR(models.Model)``<br>LGDPPR - это namespace, SCALENDAR - название таблицы у РЖД.
 2. ``VPUTI, STAN_TIP_ID`` - это аттрибуты классов, у них есть соотвествующее поле в базе DB2 от РЖД.

Это сделано для того, чтобы было проще искать аттрибут, или таблицу в файле документации РЖД.
Соответственно, чтобы что то править и изменять в эти таблицах и свойствах, нужно ознакомится с документацией.
[RASPADMIN-779](https://st.yandex-team.ru/RASPADMIN-779)

