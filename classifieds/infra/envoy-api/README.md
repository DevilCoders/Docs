# Disclaimer

Cluster, route, endpoint discovery service for envoy

## Settings

### Priority

- flags
- env
- config

### Flags

- `-config=/etc/yandex/vertis-datasources/datasources.properties`: path to config file (datasource.properties format)
- `-clusters-static-config`: cluster static config json file
- `-consul-address`
- `-consul-token`
- `-consul-cache-path=/tmp`
- `-log`
- `-debug-log`
- `-listener-http-log`: log file path for lds http listener
- `-listener-tcp-log`: log file path for lds tcp listener

### ENV vars
- `DC`: defaults to dc from hostname of form `host-01-myt.layer.vertis.yandex.net`
- `FETCH_DCS`: DCs to balance, defaults to: `myt|sas|vla`
- `API_PORT`: http api port, defaults to: `1700`
- `CONSUL_ADDRESS`
- `CONSUL_TOKEN`
- `LISTENER_HTTP_LOG`: log file path for lds http listener, defaults to `/var/log/envoy/envoy.log`
- `LISTENER_TCP_LOG`: log file path for lds tcp listener, defaults to `/var/log/envoy/tcp_access.log`

### Config file

```
envoy-api.consul.address=addr:port
envoy.api.consul.token=token
```
