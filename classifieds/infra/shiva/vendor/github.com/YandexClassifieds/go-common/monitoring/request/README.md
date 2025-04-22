## Middleware для мониторинга времени выполнения grpc запросов

### Usage
```go
import "github.com/YandexClassifieds/go-common/monitoring"
...
middleware := monitoring.NewMiddleware()

myGrpcServer := grpc.NewServer(
    grpc.StreamInterceptor(grpcMiddleware.ChainStreamServer(
    	middleware.StreamServerInterceptor()),
    grpc.UnaryInterceptor(grpcMiddleware.ChainUnaryServer(
    	middleware.UnaryServerInterceptor())),
)
```
### Metric
`request_duration_seconds` - метрика типа histogram

#### Labels
* `method` - имя grpc метода
* `provide` - имя сервера в котором загеристрирован хендлер. Необходимо если хендлер зарегистрирован более чем в одном сервере для разделения запросов к разным серверам.
Не пишется по умолчанию
  
### Options
#### WithServiceName
Добавляет к имени метода имя сервиса. `method` будет иметь вид: `ServiceName.MethodName`
```go
middleware := monitoring.NewMiddleware(monitoring.WithServiceName())
```
#### WithProvide
В label `provide` будет писаться указанное имя
```go
middleware := monitoring.NewMiddleware(monitoring.WithProvide("ProvideName"))
```

