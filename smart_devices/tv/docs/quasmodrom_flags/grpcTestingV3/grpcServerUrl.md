# grpcServerUrl
**Type:** nan
**Default:**
```json
{
    "grpcTestingV3": {
        "useGrpcRequests": false,
        "loggingEnabled": false,
        "timeoutMs": 5000,
        "grpcServerUrl": "https://grpc.alice.yandex.net",
        "srcrwr": []
    }
}
```

**Related tickets**
[TVANDROID-5165](https://st.yandex-team.ru/TVANDROID-5165)

**Context**
```json
{
  "grpcTestingV3": {
    "useGrpcRequests": true,
    "loggingEnabled": true,
    "grpcServerUrl": "http://192.168.178.25:8886",
    "timeoutMs": 600000,
    "srcrwr": [
      "GPROXY_INPUT:alex-garmash-dev.vla.yp-c.yandex.net:40007",
      "GPROXY_MM_SETUP:alex-garmash-dev.vla.yp-c.yandex.net:40007",
      "GPROXY_OUTPUT:alex-garmash-dev.vla.yp-c.yandex.net:40007"
    ]
  }
}
```

**Description**


`useGrpcRequests` - включает/отключает весь конфиг grpc. При выключенном grpc используется старая дройдечная ручка.

`loggingEnabled` - включает логирование запросов и ответов (и заголовки и тело).

`timeoutMs` - таймаут на все grpc запросы. 

`grpcServerUrl` - нужен для проксирования grpc-запросов через ваш ноут.
Для этого на ноуте нужно запустить `socat -v -lh tcp-l:8886,fork,reuseaddr tcp:grpc-testing.alice.yandex.net:80`.
В штатных ситуациях это вам не понадобится, не указывайте этот ключ. Лучше использовать srcrwr.

`srcrwr` - доп.заголовки, которые добавляются к запросу. Позволяют использовать нестандартные сборки бека, гранулярно для отдельных функций. Доступно только для ограниченного списка девайсов (список в процессе сбора)
