# Monitoring

Данная библиотека удовлетворяет требованиям:
- [monitoring](https://docs.yandex-team.ru/classifieds-infra/conventions/service#monitoring)
- [healthcheck](https://docs.yandex-team.ru/classifieds-infra/conventions/service#healthcheck)

## How to use

Быстро включить хелс чек
```go
import github.com/YandexClassifieds/go-common/monitoring

func main(){
	...
	monitoring.Init()
}
```

Также возвращает компонент для использования в других апи в соответствии с [требованиями](https://docs.yandex-team.ru/classifieds-infra/service-map#protocol).
```go
healthCheck := monitoring.Init()
myHttpApi.HandleFunc("/ping", healthCheck.HTTP)
````

## Environment

- [_DEPLOY_METRICS_PORT](https://docs.yandex-team.ru/classifieds-infra/deploy/default-env#_deploy_metrics_port)


## Options

### WithShutdownSign

Позволяет передать канал для выключения хелс чеков.

```go
shutdown := make(chan struct)
go func(){
    signals := make(chan os.Signal, 1)
    signal.Notify(signals, syscall.SIGINT, syscall.SIGTERM)
    <-signals
    close(shutdown)
}()
monitoring.Init(WithShutdownSign(shutdown))
```

### WithPprof

Включает pprof на порту с метриками для удобной отладки приложения.

```
monitoring.Init(WithPprof())
```

### WithConf

Позволяет передать компонент для инициализации приложения (чтения переменных окружения). [Подробнее](go-common/conf)

```go
monitoring.Init(WithConf(conf))
```

### WithLog

Позволяет включить logger. Иначе сообщения библиотеки не будут выведены. [Подробнее](go-common/log)

```go
monitoring.Init(WithConf(conf))
```

### WithServer

Позволяет передать кастомный `http` сервер, чтобы иметь возможность повесить на него что-то дополнительное.

```go
http = http.NewServeMux()
monitoring.Init(WithServer(http))
```

### WithReadySign

Позволяет передать канал для отложенного включения хелс чеков.

```go
c := make(chan struct)
monitoring.Init(WithReadySign(c))
```

### WithPort

Позволяет заменить дефолтный `_DEPLOY_METRICS_PORT` на кастомное значение.

```go
monitoring.Init(WithPort(82))
```

###  WithPings

Позволяет передать отдельные компоненты для синхронизации ответов хелс чека приложения с доступностью его зависимостей.

```go
monitoring.Init(WithPings(time.Second, dbPing, tvmPing, consulPing))
```
