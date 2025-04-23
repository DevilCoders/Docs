# @vertis/jaeger

Утилиты для подключения jaeger в проект.

В том числе решает проблему https://st.yandex-team.ru/VERTISADMIN-23963.

Модуль рассчитан на shiva и использует [переменные окружения оттуда](https://wiki.yandex-team.ru/vertis-admin/deploy/env/)

Экспортирует 3 компонента:
* `import { jaeger } from '@vertis/jaeger'` - инициализированный экземпляр `JaegerTracer` - результат вызова `jaeger.initTracer`.
* `import { createRootSpanMiddleware } from '@vertis/jaeger'` - middleware для express для создания req.rootSpan из заголовков сверху (обычно, nginx) или нового.  
* `import { startChildSpanByReq } from '@vertis/jaeger'` - небольшой хелпер для создания дочернего спана.  
