# Monitoring

Данная библиотека удовлетворяет требованиям:
- [monitoring](https://docs.yandex-team.ru/classifieds-infra/service-preparation/service-requirements#monitoring)
- [healthcheck](https://docs.yandex-team.ru/classifieds-infra/service-preparation/service-requirements#healthcheck)

## How to use

Быстро включить хелс чек
```go
import github.com/YandexClassifieds/go-common/monitoring

func main(){
	...
	monitoring.NewHealthChecker()
}
```

Также возвращает компонент для использования в других апи в соответствии с [требованиями](https://docs.yandex-team.ru/classifieds-infra/service-map#protocol).
```go
healthCheck := monitoring.NewHealthChecker()
myHttpApi.HandleFunc("/ping", healthCheck.HTTP)
````

## Environment

- [_DEPLOY_METRICS_PORT](https://docs.yandex-team.ru/classifieds-infra/service-preparation/default-env#_deploy_metrics_port)


## Options

### WithWait

Вызов функции `NewHealthChecker` будет залочен до прихода `kill` сингнала

### WithShutdownSign

Позволяет передать канал для выключения хелс чеков и остановки работы.

```go
shutdown := make(chan struct{})
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
monitoring.NewHealthChecker(WithPprof())
```

### WithConf

Позволяет передать компонент для инициализации приложения (чтения переменных окружения). [Подробнее](go-common/conf)

```go
monitoring.NewHealthChecker(WithConf(conf))
```

### WithLog

Позволяет включить logger. Иначе сообщения библиотеки не будут выведены. [Подробнее](go-common/log)

```go
monitoring.NewHealthChecker(WithLog(conf))
```

### WithServer

Позволяет передать кастомный `http` сервер, чтобы иметь возможность повесить на него что-то дополнительное.

```go
http = http.NewServeMux()
monitoring.NewHealthChecker(WithServer(http))
```

### WithReadySign

Позволяет передать канал для отложенного включения хелс чеков.

```go
c := make(chan struct)
monitoring.NewHealthChecker(WithReadySign(c))
```

### WithPort

Позволяет заменить дефолтный `_DEPLOY_METRICS_PORT` на кастомное значение.

```go
monitoring.NewHealthChecker(WithPort(82))
```

###  WithPings

Позволяет передать отдельные компоненты для синхронизации ответов хелс чека приложения с доступностью его зависимостей.

```go
monitoring.NewHealthChecker(WithPings(time.Second, dbPing, tvmPing, consulPing))
```
