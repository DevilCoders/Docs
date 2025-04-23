#### Route configuration (RDS)
1.Пример запроса для получения всех роутов для всех:
```
grpcurl -plaintext -d '{"node":{"cluster":"vertis-cluster","id":"wtf"}}' envoy-api-01-sas.test.vertis.yandex.net:1701 envoy.service.route.v3.RouteDiscoveryService.FetchRoutes| jq '.resources[0]'
```
2.Пример запроса на получение всех роутов с фильтром по имени
```
grpcurl -plaintext -d '{"node":{"cluster":"vertis-cluster","id":"wtf"}}' envoy-api-01-sas.test.vertis.yandex.net:1701 envoy.service.route.v3.RouteDiscoveryService.FetchRoutes| jq '.resources[0].virtualHosts[] | select(.name | contains("nomad-api"))'
```
Пример ответа:
```
{
  "name": "nomad-api-int",
  "domains": [
    "nomad-api-int.vrts-slb.test.vertis.yandex.net",
    "nomad-api-int.vrts-slb.test.vertis.yandex.net:80"
  ],
  "routes": [
    {
      "match": {
        "prefix": "/"
      },
      "route": {
        "cluster": "nomad-api-int",
        "timeout": "10s"
      },
      "decorator": {
        "operation": "nomad-api-int.vrts-slb.test.vertis.yandex.net"
      },
      "name": "nomad-api-int"
    }
  ]
}
```
Расшифровка ответа:  
- если был запрос с заголовком host равным ``nomad-api-int.vrts-slb.test.vertis.yandex.net`` или ``nomad-api-int.vrts-slb.test.vertis.yandex.net:80``, то его надо направить в кластер ``nomad-api-int``

3. Пример чуть более сложного набора роутов, с сервисами в бранчах:
<details>

```
{
  "name": "af-desktop-web",
  "domains": [
    "af-desktop-web.vrts-slb.test.vertis.yandex.net",
    "af-desktop-web.vrts-slb.test.vertis.yandex.net:80"
  ],
  "routes": [
    {
      "match": {
        "prefix": "/",
        "headers": [
          {
            "name": "x-branch-name",
            "safeRegexMatch": {
              "googleRe2": {},
              "regex": "(?i)AUTORUFRONT-22263"
            }
          }
        ]
      },
      "route": {
        "cluster": "af-desktop-AUTORUFRONT-22263-web",
        "timeout": "120s"
      },
      "decorator": {
        "operation": "af-desktop-AUTORUFRONT-22263-web.vrts-slb.test.vertis.yandex.net"
      }
    },
    ...
    ...
    ...  
    {
      "match": {
        "prefix": "/",
        "headers": [
          {
            "name": "x-sticky-uid",
            "safeRegexMatch": {
              "googleRe2": {},
              "regex": "1|[yY]es|[tT]rue"
            }
          }
        ]
      },
      "route": {
        "cluster": "af-desktop-web",
        "timeout": "120s"
      },
      "decorator": {
        "operation": "af-desktop-web.vrts-slb.test.vertis.yandex.net"
      }
    },
    {
      "match": {
        "prefix": "/"
      },
      "route": {
        "weightedClusters": {
          "clusters": [
            {
              "name": "af-desktop-web",
              "weight": 100
            }
          ]
        },
        "timeout": "120s"
      },
      "decorator": {
        "operation": "af-desktop-web.vrts-slb.test.vertis.yandex.net"
      }
    }
  ]
}

```
</details>  
<p>

Расшифровка ответа:
- данный набор роутов обрабатывает запросы с заголовком ``host`` равным либо ``af-desktop-web.vrts-slb.test.vertis.yandex.net`` либо ``af-desktop-web.vrts-slb.test.vertis.yandex.net:80``
- если есть заголовок ``x-branch-name`` совпадающий с ``"regex": "(?i)AUTORUFRONT-22263"``, то запрос надо отправить в кластер ``af-desktop-AUTORUFRONT-22263-web``
- если есть заголовок ``x-sticky-uid`` совпадающий с ``"regex": "1|[yY]es|[tT]rue"``, то запрос надо отправить в кластер ``af-desktop-web``
- если все вышеуказанные правила не подошли, то 100% трафика направляется в кластер ``af-desktop-web`` (это правило используется, например, для канарейки, когда надо направить % трафика в другой кластер)
