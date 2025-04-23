#### Сluster configuration  (СDS)

1.Пример запроса на получение информации про все кластера
```
grpcurl -plaintext -d '{"node":{"cluster":"vertis-cluster","id":"wtf"}}' envoy-api-01-sas.test.vertis.yandex.net:1701 envoy.service.cluster.v3.ClusterDiscoveryService.FetchClusters| jq '.resources[]'
``` 

2.Пример запроса на получение информации про кластер ``nomad-api``:
```
grpcurl -plaintext -d '{"node":{"cluster":"vertis-cluster","id":"wtf"}}' envoy-api-01-sas.test.vertis.yandex.net:1701 envoy.service.cluster.v3.ClusterDiscoveryService.FetchClusters| jq '.resources[] | select(.name | contains("nomad-api"))'
```
Пример ответа:
```
{
  "@type": "type.googleapis.com/envoy.config.cluster.v3.Cluster",
  "circuitBreakers": {
    "thresholds": [
      {
        "maxConnections": 5120,
        "maxPendingRequests": 5120,
        "maxRequests": 5120,
        "maxRetries": 3
      }
    ]
  },
  "commonLbConfig": {
    "zoneAwareLbConfig": {
      "minClusterSize": "1"
    }
  },
  "connectTimeout": "0.400s",
  "edsClusterConfig": {
    "edsConfig": {
      "apiConfigSource": {
        "apiType": "GRPC",
        "grpcServices": [
          {
            "envoyGrpc": {
              "clusterName": "xds_cluster"
            }
          }
        ],
        "setNodeOnFirstMessageOnly": true,
        "transportApiVersion": "V3"
      },
      "resourceApiVersion": "V3"
    }
  },
  "healthChecks": [
    {
      "timeout": "1s",
      "interval": "2s",
      "unhealthyThreshold": 1,
      "healthyThreshold": 3,
      "tcpHealthCheck": {},
      "eventLogPath": "/var/log/envoy/health_checks.log",
      "alwaysLogHealthCheckFailures": true
    }
  ],
  "ignoreHealthOnHostRemoval": true,
  "lbPolicy": "LEAST_REQUEST",
  "leastRequestLbConfig": {
    "choiceCount": 2
  },
  "name": "nomad-api-int",
  "type": "EDS"
}
```
Расшифровка ответа:
- лимиты запросов/коннектов на кластер:
```
        "maxConnections": 5120,
        "maxPendingRequests": 5120,
        "maxRequests": 5120,
        "maxRetries": 3
```
- живость эндпоинтов кластера проверяется tcp чеком на порт с интервалами/порогами:
```
      "timeout": "1s",
      "interval": "2s",
      "unhealthyThreshold": 1,
      "healthyThreshold": 3,
      "tcpHealthCheck": {},
```
-  кластер использует набор эндпоинтов из EDS с названием ``nomad-api-int``

