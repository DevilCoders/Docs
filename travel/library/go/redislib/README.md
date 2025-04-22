# Библиотека полезных утилит для работы с клиентом redis

1. Для сбора метрик работы редиса написан `MetricsHook`.

```golang
redisClient.AddHook(redislib.NewMetricsHook(redislib.Prefix("my-service")))
```

2. TODO. По аналогии можно реализовать трассировку, - отправку спанов в jaeger.
