#### Edpoint configuration  (EDS)
1. Пример запроса на получение информации про endpoints с названием ``nomad-ui-http``
```
grpcurl -plaintext -d '{"node":{"cluster":"vertis-cluster","id":"wtf"},"resource_names":["nomad-ui-http"]}' envoy-api-01-sas.test.vertis.yandex.net:1701 envoy.service.endpoint.v3.EndpointDiscoveryService.FetchEndpoints | jq '.'
```
Пример ответа:
```
{
  "versionInfo": "62c5b429",
  "resources": [
    {
      "@type": "type.googleapis.com/envoy.config.endpoint.v3.ClusterLoadAssignment",
      "clusterName": "nomad-ui-http",
      "endpoints": [
        {
          "locality": {
            "zone": "sas"
          },
          "lbEndpoints": [
            {
              "endpoint": {
                "address": {
                  "socketAddress": {
                    "address": "2a02:6b8:c07:131d:0:1459:f:6848",
                    "portValue": 80
                  }
                }
              }
            },
            {
              "endpoint": {
                "address": {
                  "socketAddress": {
                    "address": "2a02:6b8:c02:900:1:d:f12:901",
                    "portValue": 80
                  }
                }
              }
            },
            {
              "endpoint": {
                "address": {
                  "socketAddress": {
                    "address": "2a02:6b8:c02:900:1:d:f18:67a6",
                    "portValue": 80
                  }
                }
              }
            },
            {
              "endpoint": {
                "address": {
                  "socketAddress": {
                    "address": "2a02:6b8:c02:900:1:d:f3:452",
                    "portValue": 80
                  }
                }
              }
            }
          ]
        },
        {
          "locality": {
            "zone": "vla"
          },
          "lbEndpoints": [
            {
              "endpoint": {
                "address": {
                  "socketAddress": {
                    "address": "2a02:6b8:c1f:108f:0:1459:f:172f",
                    "portValue": 80
                  }
                }
              }
            },
            {
              "endpoint": {
                "address": {
                  "socketAddress": {
                    "address": "2a02:6b8:c1f:1091:0:1459:f:13bb",
                    "portValue": 80
                  }
                }
              }
            },
            {
              "endpoint": {
                "address": {
                  "socketAddress": {
                    "address": "2a02:6b8:c0e:500:1:d:f40:617c",
                    "portValue": 80
                  }
                }
              }
            },
            {
              "endpoint": {
                "address": {
                  "socketAddress": {
                    "address": "2a02:6b8:c0e:500:1:d:f43:3493",
                    "portValue": 80
                  }
                }
              }
            }
          ],
          "priority": 1
        }
      ]
    }
  ],
  "typeUrl": "type.googleapis.com/envoy.config.endpoint.v3.ClusterLoadAssignment"
}
```
Расшифровка ответа:
- в ответе содержится два набора endpoint-ов
- каждый набор имеет разный приоритет ("priority")
- трафик отправляется в эндпоинты с меньшим приоритетом (например: ``"priority": 0``)
- если живых эндпоинтов с наименьшим приоритетом не осталось - используется следующий набор с наименьшим приоритетом (``"priority": 1``)

Часть трафика может отправляться в наборы с большим приоритетом, если в наборах с наименьшим приоритетом чать эндпоинтов не прошли проверку живости (подробнее тут: https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/upstream/load_balancing/priority).  
Как правило у нас такого не бывает, так как набор эндпоинтов формируется из инстансов сервиса в консуле, которые прошли проверку живости в консуле. 

(!) Проверка живости в консуле - не тоже самое, что проверка живости у envoy. Допустим у сервиса  было запущено 10 инстансов в SAS и 10 инстансов во VLA, затем 5 инстансов во VLA не прошли проверку живости в консуле. В таком случае envoy-api будет отдавать два набора эндпоинтов с 10 и 5 инстансами соответсвенно. А так как и 10 инстансов в SAS и оставшиеся 5 инстансов во VLA будут проходить проверку живости на envoy - envoy будет считать, что в каждом наборе endpoints живые все 100% инстансов.
