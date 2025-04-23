# Tickets API

## Intro {#intro}

В данном документе описывается RPC интерфейс сервиса Nanny. В реальности система предоставляет один RPC endpoint для работы с релизами, очередями и тикетами.

## Доступ {#access}

Базовый URL для всех RPC сервисов — `https://nanny.yandex-team.ru/api/tickets/`.

## Python Client {#python-client}

* Для использование необходимо установить 2 пакета (с `pypi.yandex-team.ru`):
    * `nanny_rpc_client`
    * `nanny_tickets`

### Пример использования {#python-client-example}

```python
from nanny_rpc_client import RequestsRpcClient
from nanny_tickets import tickets_api_stub
from nanny_tickets import tickets_api_pb2

client = RequestsRpcClient('http://nanny.yandex-team.ru/api/tickets',
                           request_timeout=3,
                           oauth_token="Please provide your token here")
tickets_stub = tickets_api_stub.TicketServiceStub(client)
tickets_stub.list_queues(tickets_api_pb2.ListQueuesRequest(limit=100),
                         request_timeout=10,  # We have overridden parameter
)
```

### Закрытие всех открытых релизов по фильтру {#python-client-close-release-by-filter}

```python
"""
Закрытие всех открытых релизов старше двух дней, которые в описании содержат "ranking_models"
"""
import datetime

from nanny_rpc_client import RequestsRpcClient
from nanny_tickets import tickets_api_stub
from nanny_tickets import tickets_api_pb2
from nanny_tickets import releases_pb2

# Инициализируем клиент
client = RequestsRpcClient('http://nanny.yandex-team.ru/api/tickets',
                           request_timeout=3,
                           oauth_token="Please provide your token here")
tickets_stub = tickets_api_stub.TicketServiceStub(client)

d = datetime.datetime.now() - datetime.timedelta(days=2)

# Заполняем объект запроса
req = tickets_api_pb2.FindReleasesRequest()
req.limit = 1000
req.query.status.append(releases_pb2.ReleaseStatus.OPEN)
req.query.text_contains = 'ranking_models'
req.query.creation_time_lte.FromDatetime(d)
# Выполняем запрос
resp = tickets_stub.find_releases(req)
# Печатаем ответ
print resp.total
for i in resp.value:
    print i.spec.title
    req = tickets_api_pb2.UpdateReleaseStatusRequest()
    req.id = i.id
    req.comment = 'Closing release due to https://st.yandex-team.ru/USEREXP-2803 request'
    req.status.CopyFrom(i.status)
    req.status.status = releases_pb2.ReleaseStatus.CLOSED
    print i.id
    # Выполняем запрос на закрытие тикета
    # tickets_stub.update_release_status(req)
```

### Фильтрация тикетов {#python-client-tickets-filter}

```python
"""
Выборка всех тикетов конкретного релиза
"""
from nanny_rpc_client import RequestsRpcClient
from nanny_tickets import tickets_api_stub
from nanny_tickets import tickets_api_pb2
from nanny_tickets import releases_pb2

# Инициализируем клиент
client = RequestsRpcClient('http://nanny.yandex-team.ru/api/tickets',
                           request_timeout=3, oauth_token='Your OAuth token here')

tickets_stub = tickets_api_stub.TicketServiceStub(client)

# Заполняем объект запроса
req = tickets_api_pb2.FindTicketsRequest()
req.limit = 1000
req.query.release_id = 'SANDBOX_RELEASE-65627126-STABLE'
# Выполняем запрос
resp = tickets_stub.find_tickets(req)
# Печатаем ответ
print resp.total
for i in resp.value:
    print i
```

## Описание сервиса {#service-definition}

Самая актуальная информация содержится [в исходном коде](https://a.yandex-team.ru/arc_vcs/infra/nanny/nanny_tickets/nanny_tickets/tickets_api.proto?rev=r9313573).
