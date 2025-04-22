# Echo
В этой секции туториала мы попробуем реализовать Echo-сервис, отвечающий оригинальным запросом:

```bash
curl -X POST \
     -d '{"text": "Hello, Horadric!"}' \
     -H 'Content-Type: application/json' \
     http://localhost:8888/api/tutorial.Echo/respond
```
```json
{
    "text": "Hello, Horadric!"
}
```

## Новый проект в Аркадии
**Horadric** работает только в Аркадии – внутренности кодогенерации завязаны на `ya.make`.

Заводим корневую директорию для проекта (ограничений нет):
```bash
cd "$ARCADIA_ROOT"
mkdir -p horadric/echo
cd horadric/echo
```

Cоздадим скелет проекта:
```bash
mkdir proto bin
touch ya.make
touch inifuss.scroll 
touch README.md
```

## Описываем протоколы
Horadric работает поверх [protocol buffers](https://developers.google.com/protocol-buffers).
Начнем с описания модели данных нашего сервиса:

```bash
$EDITOR proto/data.proto
```

```protobuf
syntax = "proto3";

package tutorial;


message Request {
    string text = 1;
}

message Response {
    string text = 2;
}
```

Мы описали два сообщения – `Request` и `Response`, живущие в пакете `echo`.
`package` в proto3 опциональный, однако для Horadric он обязателен.

Теперь, когда у нас есть модель данных, опишем протокол сервиса:
```bash
$EDITOR proto/service.proto
```

```protobuf
syntax = "proto3";

package tutorial;

import "horadric/echo/proto/data.proto";


service Echo {
    rpc respond (tutorial.Request) returns (tutorial.Response);
}
```

Данные и сервис находятся в одном пакете, поэтому можно использовать короткие имена:
```protobuf
service Echo {
    rpc respond (Request) returns (Response);
}
```

Осталось только завести таргет для `ya.make` и с протоколами мы закончили:
```bash
$EDITOR proto/ya.make
```

```make
PROTO_LIBRARY()

OWNER(username)

SRCS(
    data.proto
    service.proto
)

END()
```

Попробуем собрать нашу библиотеку протоколов (просто проверим, что нигде не ошиблись):
```bash
ya make proto
```

## Пишем `inifuss.scroll`
`inifuss.scroll` это своего рода `ya.make` для Horadric.
Он описывает протоколы и зависимомости нашего проекта, а также генераторы, использующиеся внутри
(в Horadric они называются [Cairn Stones](https://diablo.fandom.com/wiki/Cairn_Stones)).

```bash
$EDITOR inifuss.scroll
```

```yaml
project:
    name: echo
    path: horadric/echo  # путь от корня Аркадии

# протоколы и зависимости
peers:
    - path: horadric/echo/proto

# генераторы
cairnStones:
    - name: chronicler  # генерация конфигов для локального балансера, о нем ниже
    - name: shadow      # генерация Python-аннотаций (.pyi), упростит жизнь в IDE
    - name: valet       # генерация интерфейсов сервисов, а также HTTP/gRPC-клиентов

# если ты обычно собираешь через `ya make -r` вместо `ya make`
releaseBuild: true
```

## Запускаем Horadric
Наконец мы можем запустить Horadric над нашими свеженаписанными протоколами!
```bash
ya tool horadric
```

Дожидаемся окончания сборки и генерации и смотрим в директорию проекта.
Там появились две новые директории – `services` и `serval_configs`.

## Пишем имплементацию
В этом туториале мы будем использовать модульную систему из [martylib](https://a.yandex-team.ru/arc/trunk/arcadia/search/martylib), чтобы писать поменьше boilerplate'а.
Подробнее про нее можно почитать [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/tutorial/ref/modules.md).

```bash
$EDITOR bin/main.py
```

```python
import argparse
import logging

from search.martylib.core.logging_utils import configure_binlog          # бинарные логи, о них ниже
from search.martylib.loop_utils import get_grpc_server

from search.martylib.modules import Daemon, ServiceModule, ServerModule
from horadric.echo.services.tutorial import EchoInterface                    # интерфейс нашего Echo-сервиса
from horadric.echo.proto import data_pb2                                 # протоколы данных


class Echo(EchoInterface):                # имплементация Echo-сервиса
    def respond(self, request, context):  # хэндлер как в протоколе сервиса (IDE подскажет)
        return data_pb2.Response(
            text=request.text,
        )


class EchoModule(ServiceModule):          # модуль для включения Echo-сервиса в итоговом бинарнике
    @classmethod
    def get_service(cls):
        return Echo()


class Server(ServerModule):               # модуль для включения gRPC-сервера
    @classmethod
    def get_server(cls):
        return get_grpc_server(f'[::]:{cls.args.port}', services=())  # про args ниже


def parse_args():                         # простенький парсер аргументов
    parser = argparse.ArgumentParser()
    parser.add_argument('-p', '--port', type=int, default=50051)
    parser.add_argument('modules', nargs='*', default=['Server', 'EchoModule'])
    return parser.parse_args()


def main():                               # entrypoint бинарника
    configure_binlog('tutorial')          # настройка бинарного логирования, о нем ниже
    Daemon(args=parse_args()).run()       # запускаем выбранные модули
```

Еще конечно нужен `ya.make`:

```bash
$EDITOR bin/ya.make
```

```make
PY3_PROGRAM(echo)

OWNER(username)

PY_SRCS(
    MAIN main.py
)

PEERDIR(
    search/martylib
    horadric/echo/services
)

END()
```

Вот, собственно, и все.

Попробуем запустить:
```bash
ya make bin && ./bin/echo
```

## Запускаем IPython в контексте проекта
Так, хорошо, что-то мы запустили, возможно это даже настоящий gRPC-сервер с нашей имплементацией.
Но как потыкать?

Все просто – чтобы задать запрос нам нужен gRPC-клиент.
К счастью Horadric уже сгенерировал его для нас, это `horadric.echo.services.tutorial.EchoClient`.

Запустим IPython в контексте нашего проекта и сможем использовать клиент:
```bash
./bin/echo shell
```

```python
from horadric.echo.proto import data_pb2
from horadric.echo.services.tutorial import EchoClient

client = EchoClient.from_address('localhost:50051')  # стандартный порт
response = client.respond(data_pb2.Request(text='Hello, Horadric!'))
response.text
```

Прекрасно, запросы ходят.
Но то gRPC, не у всех есть протоколы нашего сервиса и сгенерированный клиент
(хотя `PEERDIR` и на то и на другое может сделать кто угодно в Аркадии)!

Попробуем пойти по HTTP?

## Локальный балансер
И у нас ничего не получится – `echo` отвечает только на gRPC запросы.
Однако не все так плохо. Помнишь директорию `serval_configs`, которую сгенерировал Horadric?

Это конфиг для [Serval](https://a.yandex-team.ru/arc/trunk/arcadia/balancer/serval) – балансера, который мы можем собрать локально и запустить:
```bash
ya make "$ARCADIA_ROOT/balancer/serval"
"$ARCADIA_ROOT/balancer/serval/serval" -c serval_configs/serval_config.yaml
```

Serval запустится на порту `8888`.

Попробуем повторить с `curl`:
```bash
curl -X POST -d '{"text": "Hello, Horadric!"}' -H 'Content-Type: application/json' http://localhost:8888/api/tutorial.Echo/respond
```

## Как это работает
Horadric зашил сериализованные протоколы нашего сервиса в конфиг Serval'а.
Для локальной разработки этого достаточно, в проде похожим способом работает [Zephyr](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/tutorial/ref/zephyr.md).

Serval:
- получает наш HTTP-запрос с JSON-телом
- конвертирует его в gRPC-запрос с Protobuf-телом
- посылает в бекенд на дефолтном порту (50051)
- получает gRPC-ответ с Protobuf-телом
- конвертирует его в HTTP-ответ с JSON-телом
- и отдает нам

## Дальнейшие изменения протоколов
После изменения протоколов (добавления новых сервисов/хендлеров и любых изменениях внутри) нужно:
- убедиться что все `proto`-файлы добавлены в `PROTO_LIBRARY`
- запустить `ya tool horadric`
- пересобрать бинарник
- перезапустить бинарник
- перезапустить Serval – можно так: `curl http://localhost:9000/reload`
- перезапустить shell


## [2EZ! Го писать чат, я создал →](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/tutorial/2-chat.md)