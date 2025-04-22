# Repo API

## Intro {#intro}

В данном документе описывается RPC интерфейс Service Repo (репозиторий сервисов).

## Доступ {#access}

Базовый URL для доступа — `http(s)://nanny.yandex-team.ru/api/repo`.

## Python Client {#python-client}

Состоит из двух частей, лежащих в arcadia:

* [nanny_rpc_client](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/nanny_rpc_client)
* [nanny_repo](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/nanny_repo)

### Пример использования {#python-client-example}

```python
"""
Получение описания конкретной политики очистки старых конфигураций.
"""
from nanny_rpc_client import RequestsRpcClient
from nanny_repo import repo_api_stub
from nanny_repo import repo_api_pb2

client = RequestsRpcClient('https://nanny.yandex-team.ru/api/repo',
                           request_timeout=3,
                           oauth_token="Please provide your token here")
repo_stub = repo_api_stub.RepoServiceStub(client)

repo_stub.get_cleanup_policy(repo_api_pb2.GetCleanupPolicyRequest(policy_id='production_nanny'))
```

#### Описание сервиса {#service-definition}

Самая актуальная информация содержится [в исходном коде](https://a.yandex-team.ru/arc_vcs/infra/nanny/nanny_repo/proto/repo_api.proto?rev=r9313573).
