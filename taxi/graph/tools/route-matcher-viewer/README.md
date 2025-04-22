# route-mathcer-viewer

## Usage example
```
curl http://graph.taxi.tst.yandex.net/route -d \
    {"route":[[37.642674, 55.734042], [37.59315, 55.738158]], "detailed_info": true} \
    | ./route-matcher-viewer -t 55.730512 -n 37.635634 \
    | easyview -P 56683
```

```
curl http://graph.taxi.tst.yandex.net/route -d \
    {"route":[[37.642674, 55.734042], [37.59315, 55.738158]], "detailed_info": true} \
    | ./route-matcher-viewer \
        -p [[37.636, 55.731512], [37.634, 55.730512]] \
    | easyview -P 56683
```
