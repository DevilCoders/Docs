## Tracing Library from Yandex.Travel

Библиотека состоит из нескольких частей:

 - django
 - global_context
 - gunicorn
 - instrumentation
 - sampling

Все эти библиотеки могут быть использованы по отдельности. Все они полагаются на АПИ opentracing, так что могут быть 
использованы с другими opentracing библиотеками.


### django

Эта библиотека предлагает:

**traced_view**
Декоратор, который позволяет автоматически трассировать django вьюхи. Извлекает из request и складывает в tags: path, query, method.
Правильно вычисляет имя вьюхи.

**TracingMiddleware**
Эта миддлвара извлекает из request reqid и складывает ее в tags спана.

### global_context

Позволяет сохранять в некий глобальный контекст данные, которые потом могут быть положены в tags спанов.

**set_context**
Устанавливает контекст в переданный.

**add_context_to_span**
Добавляет все данные из глобального контекста трассировки в tags переданного спана.

**set_qloud_image_version**
Добавляет в глобальный контекст текущую версию приложения qloud'а. 
Данные о версии берет из QLOUD_DOCKER_IMAGE
TODO: унести куда то.

### gunicorn

В случае если мы используем трассировку в приложении которое форкается - нам нужно руками запустить трассировку после форка.

**build_post_fork** 
как раз это и делает. В него можно передать wrapper_cls=travel.library.python.tracing.django.Tracing для django приложений.
Пример использования (gunicorn_cong.py):
```
from travel.library.python.tracing.django import Tracing
from travel.library.python.tracing.gunicorn import build_post_fork

jaeger_sampler_type = os.environ.get('JAEGER_SAMPLER_TYPE', 'probabilistic')
jaeger_sampler_parameter = os.environ.get('JAEGER_SAMPLER_PARAMETER', 0.001)
jaeger_config = Config(
    config={
        'sampler': {
            'type': jaeger_sampler_type,
            'param': jaeger_sampler_parameter,
        },
        'logging': True,
    },
    service_name='train-wizard-api',
    validate=True,
)

post_fork = build_post_fork(jaeger_config, wrapper_cls=Tracing)

```

Включать/выключать трассировку можно при помощи переменной окружения:
TRACING_IS_TRACING_ON {False, True} - False by default

### instrumentation

**child_span**
Контекстный менеджер позволяющий затрассировать произвольный кусок кода.

**traced_function**
Декоратор, позволяющий затрассировать произвольную функцию. Правильным образом строит имя спана.

### sampling

Содержит реализацию сэмплера, собирающего только самые длинные спаны.

Переменные окружения:
TRACING_SAMPLING_LONG_SPANS {False, True) - False by default. Report all long spans (with rate limit)
TRACING_SAMPLING_TIME_THRESHOLD - 0.15 by default.
TRACING_SAMPLING_LONG_SPANS_RATE_LIMIT - 1 per second.

## Вики:

https://wiki.yandex-team.ru/travel/tracing/

## Примеры использования 
смотри тут https://a.yandex-team.ru/arc/trunk/arcadia/travel/wizards/

## Что нужно чтобы подключить 

### django

gunicorn_cong.py
```
from travel.library.python.tracing.django import Tracing
from travel.library.python.tracing.gunicorn import build_post_fork

jaeger_config = Config(
    config={
        'sampler': {
            'type': probabilistic,
            'param': 0.001,
        },
        'logging': True,
    },
    service_name='train-wizard-api',
    validate=True,
)

post_fork = build_post_fork(jaeger_config, wrapper_cls=Tracing)
```

settings
```
OPENTRACING_TRACE_ALL = True  # опционально, возможно проще развешивать руками @traved_view
OPENTRACING_TRACED_ATTRIBUTES = ['path', 'method']

INSTALLED_APPS += ['django_opentracing']
MIDDLEWARE_CLASSES = (
    'django_opentracing.OpenTracingMiddleware',
    'travel.library.python.tracing.django.TracingMiddleware',
)
```

views.py
```

@traced_view
def my_cool_view(request):
	...

```
