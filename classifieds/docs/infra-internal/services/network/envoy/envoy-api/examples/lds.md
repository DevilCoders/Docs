#### Listener configuration (LDS)
Listener-ы бывают tcp и http. Могут быть статично описаны в бутстрап конфиге envoy, могут быть получены запросом в LDS. 

1.Пример запроса в LDS на получение динамических listener-ов
```
host="envoy-api-01-sas.test.vertis.yandex.net:1701"
grpcurl -plaintext -d '{"node":{"cluster":"vertis-cluster","id":"wtf"}}' ${host} envoy.service.listener.v3.ListenerDiscoveryService.FetchListeners| jq '.resources[]'
```
Пример ответа:
```
{
  "@type": "type.googleapis.com/envoy.config.listener.v3.Listener",
  "address": {
    "socketAddress": {
      "address": "::",
      "portValue": 1221
    }
  },
  "filterChains": [
    {
      "filters": [
        {
          "name": "envoy.filters.network.tcp_proxy",
          "typedConfig": {
            "@type": "type.googleapis.com/envoy.extensions.filters.network.tcp_proxy.v3.TcpProxy",
            "cluster": "auto2-wizard-main-api",
            "statPrefix": "auto2-wizard-main-api"
          }
        }
      ]
    }
  ],
  "name": "auto2-wizard-main-api"
}
```
Расшифровка ответа:  
- tcp listener, который слушает порт 1221 и пересылает трафик в кластер auto2-wizard-main-api


2.Пример статичного listener-a из бутстрап конфига envoy:

```
static_resources:
  listeners:
  - name: listener_lb_int
    address: { socket_address: { address: "::", port_value: 80 } }
    filter_chains:
    - filters:
      - name: envoy.filters.network.http_connection_manager
        typed_config:
          "@type": type.googleapis.com/envoy.extensions.filters.network.http_connection_manager.v3.HttpConnectionManager
          stat_prefix: ingress_http
          codec_type: AUTO
          common_http_protocol_options: { idle_timeout: 120s }
          http2_protocol_options: { max_outbound_frames: 20000 }
          tracing:
            provider:
              name: envoy.tracers.dynamic_ot
              typed_config:
                "@type": type.googleapis.com/envoy.config.trace.v3.DynamicOtConfig
                library: /usr/local/lib/libjaegertracing.so.0.4.2
                config:
                  service_name: loadbalancer
                  sampler: { type: const, param: 1 }
                  reporter:
                    localAgentHostPort: 127.0.0.1:6831
          rds:
            route_config_name: local_route
            config_source: *xds_config
          http_filters:
          - name: envoy.filters.http.router
```
Расшифровка ответа:  
- http listener слушает 80-й порт, для дальнейшей маршрутизации трафика использует динамические роуты из RDS
