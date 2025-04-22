# ErrorBooster (Client)

Обертка над отправкой сообщений в error-booster.


## Deploy

Обертка для использованием в deploy.
Про настройку deploy для использования данного клиента [тут](https://clubs.at.yandex-team.ru/infra-cloud/2587).


```go
errorBoosterClient, err := errorbooster.NewDeployClient(
    errorbooster.DeployConfig{...},
    logger,
    string(app.Cfg.EnvType),
)
```

Логи будут уходить в error-booster c текстом:

```
[YATRAVEL][METAVERTICAL][METASERVICE] This is error message
```

Пример:

```
[YATRAVEL][APP][BACKEND] Error 500: backend'y chisto pofig
```

Если хочется получать логи локально, то нужно запустить:
```shell
while true; do { echo -e 'HTTP/1.1 200 OK\r\n'; } | nc -l 12345; done
```

И прописать переменные окружения:
```shell
ERROR_BOOSTER_HTTP_PORT=localhost
ERROR_BOOSTER_HTTP_HOST=12345
```

## GRPC

Есть возможность сделать интерцептор:

```go
grpcErrorBoosterInterceptor := errorbooster.NewGrpcUnaryInterceptor(
    errorbooster.DefaultGrpcInterceptorConfig,
    logger,
    errorBoosterClient,
)
```

