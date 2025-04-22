## Flask opentracing helpers

Библиотека для настройки трассировки в проектах на Flask.

Что делает библиотека:
- инициализирует глобальный трейсер, инициализирует трейсинг Flask
- прокидывает трассировку в вызовы requests и других библиотек
- фильтрует запросы, например, можно не трассировать ping
- включает в теги версию и переменные окружения, например, ['QLOUD_ENVIRONMENT', 'QLOUD_DATACENTER', 'QLOUD_COMPONENT']

Пример использования (в gunicorn_conf.py):
```python
import os

VERSION = os.getenv('QLOUD_DOCKER_IMAGE', ':unknown').rsplit(':', 1)[-1]
TRACING_SERVICE_NAME = 'avia-backend'


def post_fork(server, worker):
    from flask_opentracing_helpers import setup_tracing
    
    from wsgi import application

    server.log.info('Setup tracing...')
    try:
        setup_tracing(
            flask_application=application, 
            service_name=TRACING_SERVICE_NAME, 
            version=VERSION, 
            include_env_variables=['QLOUD_ENVIRONMENT', 'QLOUD_DATACENTER', 'QLOUD_COMPONENT'],
            filter_paths=['ping'],
            jaeger_sampler_type=os.environ.get('JAEGER_SAMPLER_TYPE', 'probabilistic'), 
            jaeger_sampler_parameter=float(os.environ.get('JAEGER_SAMPLER_PARAMETER', 0.001))
        )
    except Exception:
        server.log.exception('Failed to setup tracing')
    else:
        server.log.info('Done setup tracing successfully')
```

### Про сборку и заливку pip-пакетов
https://wiki.yandex-team.ru/pypi/
