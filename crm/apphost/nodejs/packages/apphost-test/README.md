## Установка grpc_client

Код требует установленного [grpc_client](https://a.yandex-team.ru/arcadia/apphost/tools/grpc_client).

Делаем `npm run install-grpc-client <директория аркадии> <директория, куда поместится собранный бинарник>`.

Например, `npm run install-grpc-client ~/arcadia ~/bin`.
По окончанию скрипт добавит `~/bin` из примера выше в PATH, чтобы nodejs код мог просто выполнять `grpc_client` через shell.
