# Jaeger

О архитектуре Jaeger: [Architecture](https://www.jaegertracing.io/docs/1.7/architecture/).

## Ручной запуск

1. загрузить jaeger-agent в требуемую директорию **dir**: `curl https://proxy.sandbox.yandex-team.ru/1317359659 > /{dir}/jaeger-agent && chmod +x /{dir}/jaeger-agent`;
2. Запустить командой `/{dir}/jaeger-agent --config-file /{project_dir}/deploy/jaeger/testing/agent.yaml`;
3. В `server/configs/development.js`, выставить флаг `travelTracing.config.disabled = false`.
4. Запустить проект.

## Провязка с бэком

Для связи трасс на ноде и бэках используется стандратное встраивание в заголовок запросов span id:
https://github.com/opentracing/opentracing-javascript/blob/cb74683fefe5bd4d711eaa0c273f3fc17a6c3781/src/tracer.ts#L124

Id записывается в заголовок `'uber-trace-id'`.

## Debug Id

Для отладки jaeger используется `jaeger-debug-id` который выставляется для Яндексоидов из сессионной куки `ya_travel_uid`.
Либо берется из заголовка `jaeger-debug-id` запроса.

## Ссылки

-   Дока: https://wiki.yandex-team.ru/travel/tracing
-   UI тестового Jaeger: https://jaeger.yt.yandex-team.ru/travel-test/search
-   UI продуктового Jaeger: https://jaeger.yt.yandex-team.ru/travel/search
