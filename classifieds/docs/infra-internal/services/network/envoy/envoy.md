## Общее
### Про ansible роль

Роль для наливки: [envoy](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/envoy)  
1. В [tasks/main.yml](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/envoy/tasks/main.yml?rev=r9489974#L17) указываются основные параметры для конфигурирования:  
  a) версия пакета с envoy (envoy_ver) 
  b) название конфига для кластера из ``files/etc/envoy/<>`` (envoy_file_name)
  c) имя сервиса в консуле для инстансов envoy (consul_service_name) , желательно указывать одинаковые для прода и тестинга по названию кластера (примеры: lb-int-envoy, cme-proxy-envoy). В дальнейшем это имя используется на дашборде с графиками envoy в  ``переменной prometheus job name``  
 2. Роль включает в себя закрытие и открытие для нагрузки, для работы роли требуется [lb-mngr.sh](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/lb-mngr). 
 3. Если сервер еще не конфигурировали (например, если сервер только что переналили), то он будет полностью сконфигурирован с помощью ansible-pull. Если сервер уже был сконфигурирован, и были внесены изменения в конфигурацию envoy - ansible-pull не будет применять изменения, при этом загорится мониторинг. Если изменения включают в себя только новую версию пакета с envoy - он будет обновлен, но без рестарта.  
 4. Так как роль включает в себя закрытие от нагрузки, в плейбуках с этой ролью крайне желательно указывать ``serial`` во избежание одновременного закрытия всех хостов группы.
 5. Для удобства работы перед закрытием хоста от нагрузки на нем отключается ansible-pull, и включается при открытии для нагрузки ( включается, даже если был отключён не автоматикой).  


### Про конфиги  
Все конфиги содержат обязательные части:  

1.Имя кластера  
```
node:
  cluster: <cluster_name>
```

2.Настройки UI администратора:  
```
admin:
  access_log_path: <path_to_log>
  address:
    socket_address: { address: "::", port_value: 8001 }
 ```   
Если логи не нужны, то можно указать ``/dev/null`` 

3. Listener на 81 порту для отдачи метрик  
```
  - name: listener_<имя_кластера>_stats_prometheus
    address: { socket_address: { address: "::", port_value: 81 } }
    filter_chains:
    - filters:
      - name: envoy.filters.network.http_connection_manager
        typed_config:
          "@type": type.googleapis.com/envoy.extensions.filters.network.http_connection_manager.v3.HttpConnectionManager
          stat_prefix: ingress_http
          codec_type: AUTO
          common_http_protocol_options: { idle_timeout: 120s }
          route_config:
            name: <имя_кластера>_stats_prometheus_router
            virtual_hosts:
            - name: <имя_кластера>_metrics
              domains: ["*"]
              routes:
              - match: { prefix: "/metrics" }
                route: { cluster: local-admin, prefix_rewrite: "/stats/prometheus" }
          http_filters:
          - name: envoy.filters.http.router
```          
4.Listener c http ручкой со статусом готовности envoy (он же ``readiness check``, используется, например, в проверках живости для NOC SLB). Listener может отсутствовать у старых кластеров, но крайне желательно делать его для всех новых.  
```
  # https://github.com/envoyproxy/envoy/issues/16425
  # NOC SLB check
  - name: listener_readiness_check_
    address: { socket_address: { address: "::", port_value: 8002 } }
    filter_chains:
    - filters:
      - name: envoy.filters.network.http_connection_manager
        typed_config:
          "@type": type.googleapis.com/envoy.extensions.filters.network.http_connection_manager.v3.HttpConnectionManager
          stat_prefix: ready_http
          codec_type: AUTO
          common_http_protocol_options: { idle_timeout: 120s }
          route_config:
            name: <имя_кластера>_readiness_check_router
          http_filters:
          - name: envoy.filters.http.health_check
            typed_config:
              "@type": type.googleapis.com/envoy.extensions.filters.http.health_check.v3.HealthCheck
              pass_through_mode: false
              headers:
                - name: ":path"
                  exact_match: "/ready"
          - name: envoy.filters.http.router
```          
5.Статичный сервисный кластер для listener-a на 81-м  порту. Указывает в localhost, на порт с UI администратора:  
```
  clusters:
  - name: local-admin
    connect_timeout: 0.25s
    type: STRICT_DNS
    lb_policy: LEAST_REQUEST
    typed_extension_protocol_options:
      envoy.extensions.upstreams.http.v3.HttpProtocolOptions:
        "@type": type.googleapis.com/envoy.extensions.upstreams.http.v3.HttpProtocolOptions
        explicit_http_config:
          http_protocol_options: {}
    load_assignment:
      cluster_name: local-admin
      endpoints:
      - lb_endpoints:
        - endpoint:
            address: { socket_address: { address: localhost, port_value: 8001 }}
```

Все остальные настройки - специфичные на эту кондукторную группу. Как правило - это еще один listener (обслуживающий сервисный трафик) и набор статичных/динамичных сервисных кластеров.  

## Про общекоммунальный envoy, динамическое обновление конфигурации и envoy-api
В группах lb_int используется динамическое обновление конфигурации c помощью XDS (секция в конфиге - xds_config). В роли XDS выступает envoy-api ([исходные коды](https://a.yandex-team.ru/arcadia/classifieds/infra/envoy-api?rev=r9474266),[ansible роль](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/envoy-api?rev=r9474266))  
Envoy-api:  
- развернут на отдельных серверах (группы: vertis_vprod_envoy_api/vertis_vtest_envoy_api)  
- генерирует конфигурацию для envoy используя данные из shiva, из консула и [статичного конфига](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/envoy-api/files/etc/envoy-api/testing-clusters.yaml?rev=r9474266) (используем для сервисов, которые не живут в докере). Статичный конфиг считаем deprecated.
- умеет отвечать по v2 протоколу (на порту 1700) и по v3 протоколу (порт 1701). Протокол v2 считается legacy, в будущем его поддержка будет удалена из исходных кодов envoy-api.  

Данные из статичного конфига подтягиваются без рестарта envoy-api.  

Больше технических подробностей про envoy-api можно получить [тут](envoy-api/envoy-api.md)

## Про графики 

Метрики со всех инстансов envoy автоматически попадают на [дашборд](https://grafana.vertis.yandex-team.ru/d/000000610/envoy). В ``Prometheus job name``, при необходимости, можно выбрать нужный кластер инстансов envoy.
