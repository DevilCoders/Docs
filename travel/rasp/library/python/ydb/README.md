# Cache

Базовый py2/py3 класс для кеширования в ydb. Имеет key/value интерфейс работы.

Таблица имеет 3 поля:

```
key - Utf8
value - JsonDocument
expire_at - Timestamp
```

Подробнее о типах [смотрите](https://ydb.yandex-team.ru/docs/yql/reference/types/primitive) документацию.
Поле expire_at указывается в микросекундах.
Важно: тип JsonDocument хранит числа в Double для выполнения арифметических опрераций.

Данные в кеше будут храниться до конца времени, указанного в поле expire_at.
[Не гарантируется](https://ydb.yandex-team.ru/docs/concepts/ttl), что удаление произойдёт именно в expire_at, поэтому для исключения из выборки лучше использовать фильтрацию на уровне запроса.

Пример использования в коде:

```python
import json
from travel.rasp.library.python.ydb import Cache, session_pool_context, ensure_table_exists
from common.data_api.ydb.instance import ydb_driver_config

class TaxiCache(Cache)
    PATH = 'vehicle/taxi/driver'
    NAME = 'cache'

driver_config = ydb.DriverConfig(
    endpoint='ydb-ru-prestable.yandex.net:2135',
    database='/ru-prestable/rasp/development/rasp',
    auth_token='AA-...'  # yql auth token
)  # или воспользоваться ydb_driver_config из instance модуля

with session_pool_context(driver_config) as context:
    cache = TaxiCache(context)

    ensure_table_exists(cache)  # create table if not exists

    cache.add([{
        'key' : 'hyundai:creta:a222aa:196',
        'value' : json.dumps({'driver':'Василий','disadvetages':'курит в салоне'}),
        'expire_at' : 1645124400000000  # 2022-02-18 00:00:00 in microseconds
    }, {
        'key' : 'renault:kaptur:b333bb:172',
        'value' : json.dumps({'driver':'Алексей','disadvetages':'засыпает за рулём'}),
        'expire_at' : 1645124400000000
    }])

    row = cache.get('hyundai:creta:a222aa:196')
    if row is not None:
        value = json.loads(row.value)
        print('car = {}, driver = {}'.format(row.key, value['driver']))
```

В данном случае таблица создастся по такому пути: `/ru-prestable/rasp/development/rasp/vehicle/taxi/driver/cache`.

# Новые таблицы

Для новых таблиц нужно отнаследоваться от BaseTable, определив метод `description`, который задаёт схему таблицы и используется в функции `ensure_table_exists` для создания таблицы.

# Общие вопросы по работе с YDB:

1. Почему код не работает с процессами (с fork-ами)

    На момент написания данного кода sdk driver ydb для python был не fork-safe.

2. Как получить токен

    [Прочитать](https://ydb.yandex-team.ru/docs/getting_started/auth#get_oauth_token) документацию.

3. Зачем используется `session_pool_context`. Почему бы `driver_config` не передать прямо в конструктор класса `BaseTable`.

    В случае, если будет много таблиц в ydb, то в таком сценарии не будет общего ConnectionCache и SessionPool.
