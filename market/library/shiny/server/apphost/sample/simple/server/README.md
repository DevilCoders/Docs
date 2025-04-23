### Как пощупать? ###
1. Собрать этот простенький пример: `ya make`. Сервер содержит реализацию источника с 2мя ручками: `/hello` и `/bye`.
1. Запустить: ```./server -c cfg```. Сервис для аппхоста поднимется на двух портах: `2509` для HTTP-запросов и `2510` для gRPC-запросов, а также для классического HTTP на `2508`. Если порты заняты, то либо освободите, либо поправьте конфиг.
1. Собрать [servant_client](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/tools/servant_client) – через него будем делать запросы в HTTP-порт
1. Собрать [grpc_client](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/tools/grpc_client) – через него будем делать запросы в gRPC-порт. gRPC в Аппхосте считается предпочтительным протоколом для общения.
1. Делаем hello-запрос по HTTP: `$ARCADIA/apphost/tools/servant_client/servant_client localhost:2509/hello request.json --proto-to-json`
1. Делаем hello-запрос по gRPC: `$ARCADIA/apphost/tools/grpc_client/grpc_client localhost:2510/hello request.json --proto-to-json`
1. Также можно убедиться, что обычный HTTP также работает: `curl localhost:2508/hello?name=yuraaka`
