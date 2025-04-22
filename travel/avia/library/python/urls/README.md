# URLs

Библиотека формирования URL-ов на страницы авиа части портала путешествий.

Фабрики в `__init__.py` можно использовать, когда известно окружение (testing/production). Имя хоста будет выбрано в
зависимости от окружения.

## Лэндинги направлений (travel_avia_route_landing)

Использование

```python
from travel.avia.library.python.urls import travel_avia_route_landing, Environment

travel_avia_route_landing(Environment.TESTING).url("moscow", "paris")
```

Сформирует ссылку на направление Москва-Париж. Значение slug-ов не проверяется на корректность, только на наличие. В
случае, если один из slug-ов будет пустой, будет
выкинуто `travel.avia.library.python.urls.errors.MalformedUrlParameterValue`

## Ссылки на поиск (travel_avia_search)

Использование

```python
from travel.avia.library.python.urls import travel_avia_search, Environment

travel_avia_search(Environment.TESTING).url(213, 2, "2020-01-02")
```

Cформирует ссылку на поиск Москва - Санкт-Петербург. Значение id городов и даты не проверяется на корректность, только
на наличие. В случае, если один из параметров будет пустой, будет
выкинуто `travel.avia.library.python.urls.errors.MalformedUrlParameterValue`

## Прямое использование

Можно использовать соответствующие классы (`TravelAviaRouteLanding`, `TravelAviaSearch`)
напрямую, если хочется задать конкретный host для портала путешествий.
