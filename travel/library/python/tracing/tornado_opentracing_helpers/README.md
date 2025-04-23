## Tornado opentracing helpers

Библиотека для настройки трассировки в проектах на Tornado.

Что делает библиотека:
- инициализирует глобальный трейсер, инициализирует трейсинг Tornado
- прокидывает трассировку в вызовы requests и других библиотек
- фильтрует запросы, например, можно не трассировать ping
- включает в теги версию и переменные окружения, например, ['QLOUD_ENVIRONMENT', 'QLOUD_DATACENTER', 'QLOUD_COMPONENT']

Пример использования:
```python
import os

from jaeger_client.constants import SAMPLER_TYPE_PROBABILISTIC
from tornado.web import Application
from tornado_opentracing_helpers import setup_tracing

VERSION = os.getenv('QLOUD_DOCKER_IMAGE', ':unknown').rsplit(':', 1)[-1]
TRACING_SERVICE_NAME = 'your-service-name'


tornado_application_tracing_kwargs = setup_tracing(
    service_name=TRACING_SERVICE_NAME,
    version=VERSION,
    traced_attributes_of_tornado_request=['method', 'path', 'query', 'query_arguments', 'body_arguments'],
    filter_paths=['/ping'],
    jaeger_sampler_type=os.getenv('JAEGER_SAMPLER_TYPE', SAMPLER_TYPE_PROBABILISTIC),
    jaeger_sampler_parameter=float(os.getenv('JAEGER_SAMPLER_PARAMETER', 0.001))
)

application = Application(
    ...,  # your args and kwargs
    **tornado_application_tracing_kwargs
)
```

### Про сборку и заливку pip-пакетов
https://wiki.yandex-team.ru/pypi/
