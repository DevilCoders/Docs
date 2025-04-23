# Disclaimer

Адаптация [logrus](https://github.com/sirupsen/logrus) к
нашему [формату](https://docs.yandex-team.ru/classifieds-infra/conventions/logs).

Подробнее: https://docs.yandex-team.ru/classifieds-infra/logs/quick-start

## How to use

```go

import "github.com/YandexClassifieds/go-common/log/logrus"

func main(){
  log := logrus.New()
  log.Info("message")
}
```

## Logger Options

### Level
Устанавливает уровень логирования. 

Дефолтное значение: `info`
```go
log := logrus.NewLogger(logrus.WithLevel("debug"))
```

### Sentry
Включает sentry на уровнях логирования error, fatal, panic
```go 
log := logrus.NewLogger(logrus.WithSentryFromConf(conf))
log.Error("msg to sentry")
```

### Metrics
Включает метрики на уровне warn.
Поддерживают поля `_context`, `reason`, `method` (будет взят автоматически).
Для указания лейблов используйте константы `log.Context` и `log.Reason`. `log.Context` и `log.Reason` необязательны, 
метрика будет считаться по указанным лейблам
```go
log := logrus.NewLogger(logrus.WithMetrics())
log.WithField(vlog.Context, "context").WithField(vlog.Reason, "reason").Warn("message")
```

### Module Pass
Позволяет передать модули, которые будут игнорироваться при получении метода. 
Если вы используете обертку над логером, необходимо передать модуль в котором находится обертка
```go
log := logrus.NewLogger(logrus.WithModuleIgnore("github.com/YandexClassifieds/module-to-ignore"))
```