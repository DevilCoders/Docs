# Grafana link builder

## Jaeger examples:

## panel links

```
http://grafana-redirect.vertis.yandex.net/g/?svc=<service>&operation=<op>&promenv=<promenv>
```
operation is optional

## data-links:
```
http://grafana-redirect.vertis.yandex.net/g/?svc=<service>&operation=<op>&promenv=<promenv>&ts=<datalink-timestamp>
```

## tags search:
```
http://grafana-redirect.vertis.yandex.net/g/?svc=<service>&operation=<op>&promenv=<promenv>&ts=<datalink-timestamp>&t=<mytag>=<myvalue>&t=<othertag>=<othervalue>
```
