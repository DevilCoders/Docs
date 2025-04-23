# Тесты united-dispatch

## Структура
В *plugins* TODO

В *united_dispatch* хранятся тесты инфраструктурных компонент, тесты Доставочного планера

В *united_dispatch_grocery* хранятся тесты Лавочного юнита

В *united_dispatch_eats* хранятся тесты юнита Еды

## Юниты
В *conftest.py* каждого юнита должна быть определна фикстура *united_dispatch_unit*(пример для юнита Лавки):
```python
@pytest.fixture(name='united_dispatch_unit')
def _united_dispatch_unit(taxi_united_dispatch_grocery):
    return taxi_united_dispatch_grocery
```
Эта фикстура необходима для использованию любой фикстуры из *plugins*, поскольку в testsuite нет фикстуры сервиса с названием не зависящим от юнита.
