# Proto файлы

Proto файлы для работы с Logbroker.

## Директория kikimr

Публичное gRPC API [Logbroker]:
* [grpc/draft/persqueue.proto]

Структура сериализуемых сообщений:
* [protos/draft/persqueue.proto]
* [protos/draft/persqueue_error_codes.proto]

Скопированы из Аркадии с сохранением структуры файловой системы. 

## Директория chooser

Является упрощённой копией [protos/grpc.proto]. В `TGRpcServer` оставили только нужный нам метод ChooseProxy ради упрощенной компиляции proto файла. 

[Logbroker]: https://logbroker.yandex-team.ru/docs/
[grpc/draft/persqueue.proto]: https://a.yandex-team.ru/arc/trunk/arcadia/kikimr/public/api/grpc/draft/persqueue.proto
[protos/draft/persqueue.proto]: https://a.yandex-team.ru/arc/trunk/arcadia/kikimr/public/api/protos/draft/persqueue.proto
[protos/draft/persqueue_error_codes.proto]: https://a.yandex-team.ru/arc/trunk/arcadia/kikimr/public/api/protos/draft/persqueue_error_codes.proto
[protos/grpc.proto]: https://a.yandex-team.ru/arc/trunk/arcadia/kikimr/core/protos/grpc.proto
