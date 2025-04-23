## Добавляем проксирование для сервисов CME в сервисы Вертикалей через кластер "cme-proxy"

### Исходные данные

Для доступа из сервисов CME в сервисы Вертикалей используются два кластера с envoy-proxy:  
тестинг: [vertis_vtest_cme_proxy](https://c.yandex-team.ru/groups/vertis_vtest_cme_proxy)   
прод: [vertis_vprod_cme_proxy](https://c.yandex-team.ru/groups/vertis_vprod_cme_proxy)  

Над кластерами подняты NOC SLB:  
тестинг: http://cme-proxy-test-int.noc-slb.vertis.yandex.net  
прод: http://cme-proxy-prod-int.noc-slb.vertis.yandex.net  

Для каждого NOC SLB созданы ``CNAME`` днс записи:  
тестинг: ``*.cme-slb.test.vertis.yandex.net``  
прод: ``*.cme-slb.prod.vertis.yandex.net``  

### Добавляем проксирование

Конфигурационные файлы лежат в ``vertis-ansible/roles/envoy/files/etc/envoy``. Файлы называются по имени кластера.  
Тестинг: [vertis_vtest_cme_proxy.yaml](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/envoy/files/etc/envoy/vertis_vtest_cme_proxy.yaml)  
Прод: [vertis_vprod_cme_proxy.yaml](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/envoy/files/etc/envoy/vertis_vprod_cme_proxy.yaml)  

##### 1. Добавялем роут в конфигурационные файлы

В секцию route_config/virtual_hosts добавляем строчки:  
```
            - name: cmeproxy-<service_name-provides>
              domains: ["<service_name-provides>.cme-slb.<env>.vertis.yandex.net","<service_name-provides>.cme-slb.<env>.vertis.yandex.net:80"]
              routes:
              - match: { prefix: "/" }
                route: { cluster: cmeproxy-<service_name-provides>, timeout: "3600s" }
```
Где:
- вместо ``<service_name-provides>`` указываем ``имя сервиса`` из карты сервисов и его ``provides`` (для проверки pr: указывается в четырех местах).  
- вместо ``<env>`` указываем нужное окружение (test/prod)  

Пример:
```
            - name: cmeproxy-broker-api-grpc
              domains: ["broker-api-grpc.cme-slb.prod.vertis.yandex.net","broker-api-grpc.cme-slb.prod.vertis.yandex.net:80"]
              routes:
              - match: { prefix: "/" }
                route: { cluster: cmeproxy-broker-api-grpc, timeout: "3600s" }
```

##### 2. Добавляем кластер в который проксирует этот роут.

В секцию ``clusters`` добавялем строчки:
```
  - name: cmeproxy-<service_name-provides>
    connect_timeout: 0.25s
    type: STRICT_DNS
    ignore_health_on_host_removal: true
    dns_refresh_rate: 10s
    lb_policy: LEAST_REQUEST
    typed_extension_protocol_options:
      envoy.extensions.upstreams.http.v3.HttpProtocolOptions:
        "@type": type.googleapis.com/envoy.extensions.upstreams.http.v3.HttpProtocolOptions
        explicit_http_config:
          # http2 for grpc/http
          <httpX_protocol_options>
    load_assignment:
      cluster_name: cmeproxy-<service_name-provides>
      endpoints:
      - lb_endpoints:
        - endpoint:
            address: { socket_address: { address: <адрес куда проксируем>, port_value: <порт> }}
    health_checks:
    - timeout: 1s
      interval: 2s
      unhealthy_threshold: 1
      healthy_threshold: 3
      tcp_health_check: {}
    circuit_breakers:
      thresholds:
      - max_connections: 5120
        max_pending_requests: 5120
        max_requests: 5120
```  
Где:  
- вместо ``<service_name-provides>`` указываем ``имя сервиса`` из карты сервисов и его ``provides`` (для проверки pr: указывается в двух местах).
- вместо ``<адрес куда проксируем>``, ``<порт>`` - указываем адрес и порт назначения, пример:  
```address: { socket_address: { address: shiva-deploy.query.consul, port_value: 80 }}```
-  вместо ``<httpX protocol options>`` указываем:
``http_protocol_options: {}`` - для проксирования по http  
``http2_protocol_options: {}`` - для проксирования по GRPC  
пример:
```
    typed_extension_protocol_options:
      envoy.extensions.upstreams.http.v3.HttpProtocolOptions:
        "@type": type.googleapis.com/envoy.extensions.upstreams.http.v3.HttpProtocolOptions
        explicit_http_config:
          # http2 for grpc
          http2_protocol_options: {}
```          
Пример готового конфига для проксирования по ``grpc`` в сервис ``broker-api`` и его provides - ``grpc``:  
```
   - name: cmeproxy-broker-api-grpc
    connect_timeout: 0.25s
    type: STRICT_DNS
    ignore_health_on_host_removal: true
    dns_refresh_rate: 10s
    lb_policy: LEAST_REQUEST
    typed_extension_protocol_options:
      envoy.extensions.upstreams.http.v3.HttpProtocolOptions:
        "@type": type.googleapis.com/envoy.extensions.upstreams.http.v3.HttpProtocolOptions
        explicit_http_config:
          # http2 for grpc
          http2_protocol_options: {}
    load_assignment:
      cluster_name: cmeproxy-broker-api-grpc
      endpoints:
      - lb_endpoints:
        - endpoint:
            address: { socket_address: { address: broker-api-grpc-api.query.consul, port_value: 80 }}
    health_checks:
    - timeout: 1s
      interval: 2s
      unhealthy_threshold: 1
      healthy_threshold: 3
      tcp_health_check: {}
    circuit_breakers:
      thresholds:
      - max_connections: 102400
        max_pending_requests: 102400
        max_requests: 102400
```

##### 3. Раскатываем новые конфиги  
Пока не сделана автоматика на rundeck ( https://st.yandex-team.ru/VERTISADMIN-27971 ), раскатывать можно с помощью ansible плейбук c указанием роли в теге. Раскатывать желательно сначала на один хост, потом на один дц, потом везде. Примеры:  
тестинг:  ``ansible-playbook vertis_vtest_cme_proxy.yml --tags "envoy" -l "*sas*"``  
прод: ``ansible-playbook vertis_vprod_cme_proxy.yml --tags "envoy" -l "*01-vla*"``  


##### 4. Доступ до нового сервиса
После раскатки конфигов доступ до сервиса будет по адресу: 
```
fqdn: <service_name-provides>.cme-slb.<env>.vertis.yandex.net   
port: 80
```  

Где:  
- вместо ``<service_name-provides>`` указываем ``имя сервиса`` из карты сервисов и его ``provides``  
- вместо ``<env>`` указываем нужное окружение (test/prod)  
