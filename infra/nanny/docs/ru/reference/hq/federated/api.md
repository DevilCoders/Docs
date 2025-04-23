# API

##  Intro {#intro}
В данном документе описывается RPC интерфейс сервиса _Federated_. На данный момент сервис предоставляет простейший API для получения информации о кластерах HQ.

##  Доступ {#access}
* Для доступа необходимо использовать `https://federated.yandex-team.ru/rpc/federated/`
* Оригинальный путь оставлен для обратной совместимости `https://federated.n.yandex-team.ru/rpc/federated/`

##  Python Client {#python-client}
* Для использование необходимо установить 2 пакета (с `pypi.yandex-team.ru`):
    * `nanny_rpc_client` - реализация RPC.
    * `clusterpb` - интерфейсы для удалённых вызовов и protobuf определения объектов.

###  Пример использования {#python-client-example}

```python
"""
В этом примере мы получим список всех кластеров HQ, известных сервису.
"""
from nanny_rpc_client import RequestsRpcClient
from clusterpb import federated_stub  # Интерфейс удалённого RPC сервера
from clusterpb import federated_pb2  # Определения запросов и ответов сервера

# Создаём реализацию клиента, указывая URL и прочие настройки
client = RequestsRpcClient('http://federated.n.yandex-team.ru/rpc/federated/', request_timeout=10)
# Инициализируем клиент для Federated Service'а
f_client = federated_stub.FederatedClusterServiceStub(client)
# Создаём объект запроса, без параметров
find_req = federated_pb2.FindClustersRequest()
# Выполняем запрос
resp = f_client.find_clusters(find_req)
# Печатаем результат (список доступных кластеров)
for i in resp.value:
    print i
```

##  Описание сервиса {#service-definition}

```
message ClusterMeta {
    string name = 1;
    string uuid = 2;
    string version = 3;
    int64 generation = 4;
}

message ClusterEndpoint {
    string url = 1;
}

message ClusterSpec {
    string desc = 1;
    ClusterEndpoint endpoint = 2;
}

message ClusterCondition {
    string status = 1; // One of: True, False, Unknown
    string reason = 2;
    string message = 3;
    google.protobuf.Timestamp last_probe_time = 4;
    google.protobuf.Timestamp last_transition_time = 5;
}

message ClusterStatus {
    ClusterCondition ready = 1;
    string version = 2;
}

message Cluster {
    ClusterMeta meta = 1;
    ClusterSpec spec = 2;
    ClusterStatus status = 3;
}

message CreateClusterRequest {
    Cluster value = 1;
}

message CreateClusterResponse {

}

message DeleteClusterRequest {
    string name = 1;
}

message DeleteClusterResponse {

}

message FindClustersRequest {

}

message FindClustersResponse {
    repeated Cluster value = 1;
}

message GetClusterRequest {
    string name = 1;
}

message GetClusterResponse {
    Cluster value = 1;
}

service FederatedClusterService {
    rpc CreateCluster(CreateClusterRequest) returns (CreateClusterResponse);
    rpc DeleteCluster(DeleteClusterRequest) returns (DeleteClusterResponse);
    rpc FindClusters(FindClustersRequest) returns (FindClustersResponse);
    rpc GetCluster(GetClusterRequest) returns (GetClusterResponse);
}

```
