# prometheus-juggler
Delivers Prometheus alerts as events to Juggler

## Idea

Having `Prometheus` as alerting source it's possible to use `Juggler` as alert manager
(for notification/suspending/deduplicating alerts).
Use of `Juggler` is inevitable during transition period while one part of applications is covered by
`Prometheus` monitorings and the other is covered by `Juggler`.

## Usage
One can configure the application via command line arguments or configuration file in YAML.

### Configuration file
Application configuration by file is recommended for prodution usage.
File should follow the net format.
Suppose file is called `./prometheus-juggler.yaml`
```yaml
# Address of Prometheus server to fetch alerts from.
prometheus-address: http://prometheus-01-sas.test.vertis.yandex.net:9090

# Address of Juggler server to submit events to.
juggler-address: http://jmon01h.paysys.yandex.net:8999

# How frequent to sync Prometheus alerts with Juggler.
sync-period: 10s

# Listens address for serving HTTP API
listen-address: ":2525"
```

For run application with config you should pass the config file name via `config-file` argument:
```
./prometheus-juggler --config-file=./prometheus-juggler.yaml
```

### Command line arguments
 For debug purposes it may be convenient to configure the application via CL arguments.
 The supported arguments are (and its can be listed by `-h` option):

```
-config-file string
    path to configuration file to run with
-juggler-address string
    Juggler address for submit events to (http://<host>:<port>)
-prometheus-address string
    Prometheus address for get alerts from (http://<host>:<port>)
-sync-period duration
    period between subsequent systems syncs (default 1m0s)
-listen-address string
    Net address for serve HTTP API (default ":2525")
```

For example one could run the next configuration:
```
./prometheus-juggler \
--instance=prometheus-01-sas.test.vertis.yandex.net \
--prometheus-address=http://prometheus-01-sas.test.vertis.yandex.net:9090 \
--juggler-address=http://jmon01h.paysys.yandex.net:8999 \
--sync-period=5s
```
