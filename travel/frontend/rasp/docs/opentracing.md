# Opentracing

Реализация в путешествиях на [wiki](https://wiki.yandex-team.ru/travel/tracing/).

Все запросы трассируются с вероятностью 0.1%.
Запросам из внутренней сети Яндекса присваивается jaeger-debug-id и все такие запросы трассируются. Ссылка на поиск данного запроса в jaeger появляется в косоли браузера.
Чтобы ваш запрос был трассирован можно передать http-заголовок Jaeger-Debug-ID при запросе.

## При локальной разработки можно запустить jaeger локально.

При первом запуске создаем контейнер:

```bash
docker run -d --name jaeger \
  -e COLLECTOR_ZIPKIN_HTTP_PORT=9411 \
  -p 5775:5775/udp \
  -p 6831:6831/udp \
  -p 6832:6832/udp \
  -p 5778:5778 \
  -p 16686:16686 \
  -p 14268:14268 \
  -p 14250:14250 \
  -p 9411:9411 \
  jaegertracing/all-in-one:1.18
```

Затем вызываем поднимаем его командой `docker container start jaeger` и тушим командой `docker container stop jaeger`

Посмотреть трейсы можно в UI: http://localhost:16686
