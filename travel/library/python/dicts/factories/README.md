# Фабрики для простого создания protobuf объектов в тестах

Например:

```python
from travel.library.python.dicts.factories.country import TCountryFactory

country_from_proto = TCountryFactory()
```

Пример реального использования:

https://github.yandex-team.ru/avia/admin/blob/d4715a689236dc4c421522b055ed1705217c5107/tests/avia_scripts/sync_with_rasp/test_sync_www_country.py#L19-L21


# Консистентные репозитории в тестах

Для тестов нужно иметь консистентные данные в репозиториях прото-объектов.
Аналогией служит база данных для тестов. В БД заполнена структура и некоторые начальные данные.

Для решения этой задачи служит класс RaspRepositories.

## Использование 

В conftest.py размещаем такой код:

```python
import pytest

from travel.library.python.dicts.factories.rasp_repositories import RaspRepositories

@pytest.fixture
def rasp_repositories():
    return RaspRepositories()
```

Тогда в тестах можно использовать так:

https://github.yandex-team.ru/avia/admin/pull/963/files#diff-392ebc4ccb510415f62bae66aedc8cd6R15-R30
