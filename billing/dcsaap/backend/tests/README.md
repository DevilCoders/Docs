# Тесты проекта billing.dcsaap.backend

Для тестирования используется [pytest](https://wiki.yandex-team.ru/yatool/test/#python) с использованием [pytest-django](https://pytest-django.readthedocs.io/en/latest/).

## Структура тестов

Проект использует два вида тестов, разделенных размером:
- пакет `small/`:
  - небольшие модульные тесты, проверяющие точечные места в проекте и выполняющиеся в совокупности не больше минуты.
- пакет `medium/`:
  - среднего размера тесты, проверяющие функциональность проекта и смежных систем, а так же модульные тесты, занимающие длительное время

Дополнительно, в `tests` расположены 2 библиотеки (`PY3_LIBRARY`), которые содержат общий код, используемый во всех пакетах тестов:
- библиотека `strategies/`:
  - [стратегии](https://hypothesis.readthedocs.io/en/latest/data.html), используемые для генерации данных в тестах
- библиотека `utils`:
  - различные утилиты для тестов (использование tvm, создание django-моделей, и т.д.)

## Переопределение Django-settings

При использовании `django.test.TestCase` есть возможность переопределить требуемые настройки через `with self.settings(SOMETHING='SOMETHING')`. В `pytest-django` для этого нет специальных средств, поэтому требуется использовать возможности Django напрямую, например:
```python
from django.test import override_settings
...
with override_settings(SOMETHING='SOMETHING'):
    pass
...
```

## Использование БД в тестах

По-умолчанию в тестах для Django используется специальную БД, обозначаемая как `django-db`. Работа с ней выполняется неявно, при использовании `django.test.TestCase`, который берет на себя всю работу по её созданию и настройке.

В `pytest-django` этот подход немного отличается, авторы библиотеки считают что мы должны явно указывать, в каких тестах используется БД и
по-умолчанию использование БД тестом невозможно. Для обхода этого ограничения мы создали фикстуру `enable_db_for_all_tests` (находится в `conftest.py`), которая автоматически активируется перед запуском любого теста и включает доступ до БД.

Фикструа `enable_db_for_all_tests` работает только для тестов, поэтому для использования БД в фикстурах требуется подключать фикстуру `db`:

- `db`
  - Фикстура c `scope='function'`, явно разрешает использование БД.
  - Основное назначение: использование в других фикстурах, т.к. в них невозможно использовать метки или `pytest.mark.usefixtures`.
  - Пример использования:
  ```python
  @pytest.fixture
  def some_data(db):
      SomeModel.objects.create(value=1)
  ```

Больше информации можно найти на странице документации `pytest-django`: [о работе с базой данных](https://pytest-django.readthedocs.io/en/latest/database.html)

## Описание используемых фикстур

Общее описание работы `conftest.py` можно найти [здесь](https://docs.pytest.org/en/latest/writing_plugins.html#conftest-py-local-per-directory-plugins).

Основные фикстуры, доступные для Django в `pytest-django`: [django helpers](https://pytest-django.readthedocs.io/en/latest/helpers.html)

### requests_mock

Фикстура, которая позволяет подменять HTTP-запросы, выполняемые через библиотеку `requests`.

Пример использования:
```python
import requests

def test_request(requests_mock):
    requests_mock.register_uri('GET', 'http://yandex.ru', text='OK')
    assert requests.get('http://yandex.ru').text == 'OK'
```

[Документация](https://requests-mock.readthedocs.io/en/latest/overview.html).

### rf

Фабрика запросов Django. Позволяет создать объект `Request`, который может быть использован для тестирования представлений.

Пример использования:
```python
def test_view(rf):
    request = rf.get('/my/view')
    response = my_view(request)
    assert response.content == b'Hello, world'
```

[Документация](https://pytest-django.readthedocs.io/en/latest/helpers.html#rf-requestfactory)

[Документация Django](https://docs.djangoproject.com/en/2.2/topics/testing/advanced/#django.test.RequestFactory)

