# luster-prometheus

luster extension for prometheus integration

## Install

```
$ npm install --save luster-prometheus
```

### Configure

Add `luster-prometheus` to the list of your luster extensions:

~~~
// luster.conf.json

{
  "app": "worker.js",
  ···
  "extensions": {
    "luster-prometheus": {
      "port": 3131
    }
  }
}
~~~

`luster-prometheus` starts HTTP server and creates `/metrics` endpoint. 

Check it after start:
```
$ curl -s "http://localhost:3131/metrics"
```

