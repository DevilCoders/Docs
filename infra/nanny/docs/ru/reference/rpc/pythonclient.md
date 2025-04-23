# Python Client

## Intro {#intro}

Так как устройство RPC моделирует реализацию от Google, то и реализация клиента похожа принципами на Google Stubby и [gRPC](http://grpc.io). Эти библиотеки оперируют понятиями `Channel`, `Stub` и другими. Мы же попробуем сделать проще (т.к. планируем использовать библиотеку `requests`, которая внутри содержит пул соединений и другие удобные вещи). Потеряем в общности, но выйграем в простоте использования и реализации.

Используем только 2 сущности:
* `RPC Client` — универсальная библиотека на Python, которая является коннектором к любому серверу, реализующему RPC.
* `ServiceStub` — автоматически генерируемая библиотека, которая экспортирует все методы пользователю и требует для своей работы RPC Client.

В данном разделе мы описываем реализацию RPC Client для Python.

## Дизайн {#design}

Требования к RPC Client следующие, клиент умеет:
* сериализовать запрос;
* сформировать корректный урл для вызова API метода;
* отправить запрос на сервер;
* получать и десериализовывать ответ;
* выставлять таймаут на запрос;
* выставлять заголовки для аутентификации.

## API {#api}

Так как основным потребителем клиента будет автоматически сгенерированный код заглушки (`Stub`), то интерфейс должен быть минимальным. 

Принято решение, что клиент должен реализовывать следующий интерфейс:

```python
class IHttpRpcClient(object):
    """
    Interface which every HTTP RPC client must complain.
    """
    def call_remote_method(self, method_name, request_protobuf, response_protobuf, **kwargs):
        """
        Invokes remote method on server by issuing properly crafted HTTP POST request.
        :param method_name: remote method name (e.g. 'SayHello')
        :param request_protobuf: request object - protobuf message
        :param response_protobuf: response object, which will be filled with server response
        :param kwargs: additional information depending on actual implementation (e.g. override parameters)
        """
        raise NotImplementedError
```

## Реализация {#implementation}

На данный момент реализован один клиент — `RequestsRpcClient`. Он использует библиотеку `requests` для реализации протокола HTTP.

Особенности:
* поддержка аутентификации — можно передать OAuth token, либо Session_id Cookie.
* таймаут на ожидание ответа сервера.

Не реализовано:
* HTTP Keep-Alive.
* Перезапросы.

## Установка клиента {#installation}

* [Исходный код](https://git.qe-infra.yandex-team.ru/projects/NANNY/repos/nanny/browse/clients/nanny_rpc_client).
* Зависимости:
    * `protobuf>=3.0.0b2`
    * `requests>=2.5.0`
* Установка: `pip install -i https://pypi.yandex-team.ru/simple nanny_rpc_client`.

## Использование клиента {#usage}

### Базовое использование {#basics}

```python
from http_rpc_client import RequestsRpcClient

client = RequestsRpcClient('http://nanny.yandex-team.ru/api/tickets',  # RPC endpoint URL
                           oauth_token='f2e2570bb52f3deb9ac33b48a5b20a44',  # Optional: OAuth token
                           request_timeout=10,  # Request timeout
                           )
```

### Переопределение параметров {#override-params}

Параметры, установленные при создании объекта (кроме URL), можно переопределить в каждом отдельном вызове.

Рассмотрим пример с использованием заглушки (`stub`) для работы с очередями в Nanny:

```python
from http_rpc_client import RequestsRpcClient
from nanny_tickets import tickets_api_stub
from nanny_tickets import tickets_api_pb2

client = RequestsRpcClient('http://nanny.yandex-team.ru/api/queues', request_timeout=3)
tickets_stub = tickets_api_stub.TicketServiceStub(client)
tickets_stub.list_queues(tickets_api_pb2.ListQueuesRequest(),
                         request_timeout=10,  # We have overridden parameter
)
```
