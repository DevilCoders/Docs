# Трассировка запросов

Документация
* [Документация админов](https://wiki.yandex-team.ru/vertis-admin/tracing/)

Инсталяции
* [Testing jaeger](https://jaeger.test.vertis.yandex.net/search?service=loadbalancer&tags=%7B%22guid%3Ax-request-id%22%3A%22%22%7D)
* [Production jaeger](https://jaeger.vertis.yandex.net/search?service=loadbalancer&tags=%7B%22guid%3Ax-request-id%22%3A%22%22%7D)

> `trace-id` равен `x-request-id`

Обрати внимание, что у нас есть [интеграция с Grafana](https://wiki.yandex-team.ru/vertis-admin/tracing/#integracijasgrafana),
т.е., например, с графиков пятисоток можно сразу перейти к трейсам([см. видео](https://jing.yandex-team.ru/files/fresk/2019-10-25%2015.42.13.mov)).
