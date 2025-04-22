## Envoy-api (техническая часть реализации)

### Общее

Envoy-api - реализация [XDS](https://www.envoyproxy.io/docs/envoy/latest/api-docs/xds_protocol) для вертикального envoy-proxy.  

Генерирует конфигурацию для envoy используя данные из shiva, из консула и [статичного конфига](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/envoy-api/files/etc/envoy-api/testing-clusters.yaml?rev=r9474266) (используем для сервисов, которые не живут в докере). Статичный конфиг считаем deprecated. Данные из статичного конфига подтягиваются без рестарта envoy-api. 

Развернут на отдельных серверах (группы: [vertis_vtest_envoy_api](https://c.yandex-team.ru/groups/vertis_vtest_envoy_api)/[vertis_vprod_envoy_api](https://c.yandex-team.ru/groups/vertis_vprod_envoy_api)).  

Графики: [ссылка](https://grafana.vertis.yandex-team.ru/d/zmG4lpIik/envoy-api).  
Исходные коды: [ссылка](https://a.yandex-team.ru/arcadia/classifieds/infra/envoy-api).  
Ansible роль для наливки/обновления кластеров: [ссылка](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/envoy-api).  


### API
Текущая поддерживаемая версия - [v3](https://www.envoyproxy.io/docs/envoy/latest/api-v3/api#envoy-v3-api-reference) (на порту 1701).  
Предыдущая (deprecated) версия - v2 (порт 1700).  

Состоит из компонентов:  
LDS - [listener configuration](https://www.envoyproxy.io/docs/envoy/latest/api-v3/listeners/listeners) (как принимать трафик, какой порт слушать и тп).  
RDS - [route configuration](https://www.envoyproxy.io/docs/envoy/latest/api-v3/http_routes/http_routes) (логика обработки трафика, по каким заголовкам в какой кластер слать трафик, как распределять проценты трафика (канареечный трафик)).  
CDS - [cluster configuration](https://www.envoyproxy.io/docs/envoy/latest/api-v3/clusters/clusters) (проверки живости, лимиты на коннекты/запросы, политика балансировки).  
EDS - [edpoint configuration](https://www.envoyproxy.io/docs/envoy/latest/api-v3/config/endpoint/v3/endpoint.proto) (набор эндпоинтов (ip+порт+приоритет) куда слать трафик).

Примеры конфигураций, запросов и ответов XDS:
- [LDS](examples/lds.md)
- [RDS](examples/rds.md)
- [CDS](examples/cds.md)
- [EDS](examples/eds.md)

### Как это работает

1. Запрос поступает на один из listener-ов  
2. Listener  
Принимает трафик, содержит глобальные настройки по таймаутам, опциям протоколов (http/tcp) и прочему.  
Как правило, все запросы в общекоммунальный envoy идут на порт 80. Listener для этого порта описан в бутстрап конфиге envoy, это http listener, а правила обработки запросов в него формируются в RDS.  
Часть listener-ов на других портах генерируется из статичного конфига envoy-api ([пример](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/envoy-api/files/etc/envoy-api/testing-clusters.yaml#L44)). Обычно это tcp listener-ы, rds в них не используется, а в конфиге листенера сразу указан кластер в который надо отправить запрос.  
При необходимости в бутстрап конфиг envoy можно добавить статичные http/tcp listener-ы со своими статичными конфигами routers/clusters.
3. RDS  
   Формирует роуты (набор роутов) для каждого сервиса. Роуты содержат в себе правила по которым трафик надо направлять в тот или иной кластер. 
   1. Формирование по данным из шивы.
      1. Основной роут.  
      Для всех сервисов в шиве в статусе run: из имени сервиса, названия бранча (если сервис запущен в бранче) и его provides формируется набор routes c основным роутом который все запросы с заголовком ``Host`` равным ``<service_name>-<branch_name>-<provides>.vrts-slb.[test|prod].vertis.yandex.net`` направляет в кластер ``<service_name>-<branch_name>-<provides>``.  
         <details>  
         <summary>Пример:</summary>  

          ```
          {
            "name": "<service_name>-<branch_name>-<provides>",
            "domains": [
              "<service_name>-<branch_name>-<provides>.vrts-slb.[test|prod].vertis.yandex.net",
              "<service_name>-<branch_name>-<provides>.vrts-slb.[test|prod].vertis.yandex.net:80"
            ],
            "routes": [
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
                  "cluster": "<service_name>-<branch_name>-<provides>",
                  "timeout": "120s"
                },
                "decorator": {
                  "operation": "<service_name>-<branch_name>-<provides>.vrts-slb.[test|prod].vertis.yandex.net"
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
                        "name": "<service_name>-<branch_name>-<provides>",
                        "weight": 100
                      }
                    ]
                  },
                  "timeout": "120s"
                },
                "decorator": {
                  "operation": "<service_name>-<branch_name>-<provides>.vrts-slb.[test|prod].vertis.yandex.net"
                }
              }
            ]
          }
          ```
          </details>  

      2. Роуты сервисов не в бранче обогащаются роутами бранчей (если они запущены). Т.е. в набор роутов которые обрабатывают заголовки ``Host`` вида ``<service_name><provides>.vrts-slb.[test|prod].vertis.yandex.net`` добавляются правила заворачивания трафика в бранч по заголовку ``x-branch-name`` с именем бранча.  
         <details>  
         <summary>Пример:</summary>   

         ```
         {
           "match": {
             "prefix": "/",
             "headers": [
               {
                 "name": "x-branch-name",
                 "safeRegexMatch": {
                   "googleRe2": {},
                   "regex": "(?i)<branch_name>"
                 }
               }
             ]
           },
           "route": {
             "cluster": "<service_name>-<branch_name>-<provides>",
             "timeout": "120s"
           },
           "decorator": {
             "operation": "<service_name>-<branch_name>-<provides>.vrts-slb.[test|prod].vertis.yandex.net"
           }
         },
         ``` 
         </details> 

      3. Канареечный трафик.  
        Во всех основных роутах сервиса последним указан роут с весами у кластеров (``weightedClusters``).  
         <details>  
         <summary>Пример:</summary>   

         ```
         "route": {
           "weightedClusters": {
             "clusters": [
               {
                 "name": "<service_name><provides>",
                 "weight": 100
               }
             ]
           },
           ...
         }
         ```  
         </details>  

         Если в шиве есть данные про канарейку у сервиса, то в `weightedClusters` в секцию ``clusters`` добавляются канареечные ``<service_name>-<branch_name>-<provides>``, их вес составляет % трафика который необходимо направить в канарейку, а вес основного кластера (по умолчанию это 100) уменьшается на эту величину.  
        4. В описаниях кластеров (в которые надо направить трафик) указывается таймаут на время выполнения запроса к эндпоинтам этого кластера. Для сервисов в шиве этот таймаут равен 120 секундам (``"timeout": "120s"``), для сервисов в дженкинсе этот таймаут берется из KV консула, текущее значение - 10 секунд, но при необходимости его можно переопределить (подробнее про kv консула в описании кластеров, ниже по тексту).  
   2. Legacy формирование для сервисов живущих не в шиве.
      - в консуле ищутся сервисы с тегом ``domain-slbname``. Для каждого такого сервиса формируется route, который обрабатывает запросы с заголовком ``Host`` равным ``slbname`` (часть тега без начального ``domain-``).        

4. Clusters  
  Кластера формируются из сервисов в шиве/консуле(для legacy сервисов). Каждому сервису соответствует свой кластер. Каждый кластер содержит набор эндпоинтов(ip+port всех инстансов сервиса) и описывает проверки живости, лимиты на коннекты/запросы, тип балансировки и протокол (http/grpc) для работы с эндпоинтами.  

    -  Тип протокола для работы с кластером - это опция с пустым значением. Для ``http`` это ``http_protocol_options``, для ``grpc`` - ``http2_protocol_options``.  
       <details>  
       <summary>Пример:</summary>   

       ```
         "explicitHttpConfig": {
            "http2ProtocolOptions": {}
          }
       ```  
       </details>

    - Тип балансировки, лимиты на коннекты/запросы и проверки живости у всех кластер одинаковые. Хранятся в KV консула (пример: [https://consul.test.vertis.yandex.net/ui/vla/kv/envoy/defaultSettings/edit](https://consul.test.vertis.yandex.net/ui/vla/kv/envoy/defaultSettings/edit)). Важно(!) KV в консуле не синхронизируется между дц, если есть необходимость внести правки, то их нужно вносить в KV во всех дц.  
      Содержимое kv на момент написания доки:  
        <details>  
        <summary>Пример:</summary>   

         ```
         {
           "cds": {
             "connect_timeout": "0.4s",
             "refresh_delay": "1s",
             "lb_policy": "LEAST_REQUEST",
             "drain_connections_on_host_removal": "true",
             "health_checks": {
               "timeout": "1s",
               "interval": "2s",
               "unhealthy_threshold": 1,
               "healthy_threshold": 3
             },
             "circuit_breakers": {
               "thresholds": {
                 "max_connections": 5120,
                 "max_pending_requests": 5120,
		         "max_requests": 5120,
                 "max_retries": 3
               }
             }
           },
           "rds": {
             "route": {
               "upstream_timeout": "10s"
             }
           }
         }
        ```
        </details>   

5. Edpoints  
  Эндпоинты представляют собой набор из одной или двух групп адресов инстансов сервиса (IP адрес + порт). Формируются из данных про сервис в консуле. Группы делятся по приоритетам, самый высокий приоритет - "0". По умолчанию трафик направляется в группу с наивысшим приоритетом. Часть трафика может отправляться в наборы с большим приоритетом, если в наборах с наименьшим приоритетом % эндпоинтов не прошел проверку живости (подробнее в [EDS](examples/eds.md)).  
  Envoy-api, собирая информацию про инстансы сервиса в консуле, формирует две группы по принципу:
    - инстансы сервиса в текущем ДЦ объединяются в группу с приоритетом "0"  
    - инстансы из других ДЦ - в группу с приоритетом "1"  
    - если в текущем ДЦ нет живых инстансов в консуле, то из всех оставшихся живых инстансов в других дц формируется одна группа с приоритетом "0"  
  
   Таким образом, envoy, запрашивая информацию из EDS, получает набор эндпоинтов с наивысшим приоритетом из ДЦ  envoy-api в который попал запрос. Как правило, при штатной работе, эти ДЦ совпадают.  
    <details>
    <summary>Пример  эндпоинтов для сервиса у которого по одному инстансу в каждом ДЦ:</summary>

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
    </details>

### Прочее  
1. Команды для получения данных из envoy-api  

   1. Запрос информации про динамические **листенеры** от envoy-api на сервере "host_name"  
      ```
      host="<host_name>"
      grpcurl -plaintext -d '{"node":{"cluster":"vertis-cluster","id":"wtf"}}' ${host}:1701 envoy.service.listener.v3.ListenerDiscoveryService.FetchListeners| jq '.resources[]'
      ```  
       
   2. Запрос информации про **роуты** "route_name" от envoy-api на сервере "host_name" 
      ```
      host="<host_name>"
      grpcurl -plaintext -d '{"node":{"cluster":"vertis-cluster","id":"wtf"}}' ${host}:1701 envoy.service.route.v3.RouteDiscoveryService.FetchRoutes| jq '.resources[0].virtualHosts[] | select(.name | contains("<route_name>"))'
      ```  

   3. Запрос информации про **кластер** "cluster_name" от envoy-api на сервере "host_name"
      ```
      host="<host_name>"
      grpcurl -plaintext -d '{"node":{"cluster":"vertis-cluster","id":"wtf"}}' ${host}:1701 envoy.service.cluster.v3.ClusterDiscoveryService.FetchClusters| jq '.resources[] | select(.name | contains("<cluster_name>"))'
      ```

    4. Запрос информации про **эндпоинты** для кластера "cluster_name" от envoy-api на сервере "host_name"
      ```
      host="<host_name>"
      grpcurl -plaintext -d '{"node":{"cluster":"vertis-cluster","id":"wtf"},"resource_names":["<cluster_name>"]}' ${host}:1701 envoy.service.endpoint.v3.EndpointDiscoveryService.FetchEndpoints | jq '.'
      ```

2. На каждом инстансе envoy поднят административный интерфейc, доступен по адресу: ``http://<fqdn>:8001/``.  
В нём можно посмотреть:
    - текущий конфиг (без enpdoints): ``http://<fqdn>:8001/config_dump``
    - информацию про кластера (c endpoints): ``http://<fqdn>:8001/clusters``
    - информацию про envoy (аптайм, параметры запуска): ``http://<fqdn>:8001/server_info``
    - прочее

3. Для сервисов не в шиве часть настроек можно переопределить выставив определенный тег консула:  

    | Тег | Что делает | Значение по умолчанию |
    |------|:---------:|:---------------------:|
    | envoy.settings.upstream.timeout=<время_в_секундах>s | Переопределяет таймаут на выполнение запроса | 10s |
    | envoy.settings.upstream.max_connections=<число> | Переопределяет максимум соединений к кластеру | 5120 |
    | envoy.settings.upstream.max_pending_requests=<число> | Переопределяет максимальное количество ожидающих запросов | 5120 |
    | envoy.settings.upstream.max_requests=<число> | Переопределяет максимальное число параллельных запросов | 5120 |
    | envoy.settings.upstream.max_retries=<число> | Переопределяет максимальное количество повторных попыток | 3 |

    





