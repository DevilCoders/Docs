# Disclaimer

Адаптация [logrus](.com/YandexClassifieds/go-common/log/logrus) к
нашему [формату](https://wiki.yandex-team.ru/vertis-admin/logs/logsformat/?from=%252Fvertis-admin%252Flogs_format%252F).

Подробнее: https://wiki.yandex-team.ru/vertis-admin/logs/

## Logger Options

### Level
Устанавливает уровень логирования
```go
log := logrus.New(logrus.WithLevel("debug"))
```
### Sentry
Включает sentry на уровнях логирования error, fatal, panic
```go
log := logrus.New(logrus.WithSentry())
log.Error("msg to sentry")
```
### Metrics
Включает метрики на уровне warn.
Поддерживают лейблы "_context", "reason", "method" (будет взят автоматически).
Для указания лейблов используйте константы logrus.Context и logrus.Reason. logrus.Context и logrus.Reason необязательны, метрика будет считаться по указанным лейблам
```go
log := logrus.New(logrus.WithMetrics("namespace"))
log.WithField(logrus.Context, "context").WithField(logrus.Reason, "reason")
```
### Hooks
Позволяет передать hook в логер
```go
log := logrus.New(logrus.WithHook(logrus.NewMetricHook("namespace")))
```
### Module Pass
Позволяяет передать модули которые будут игнорироваться при получении метода. Если вы используете обертку над логером, необходимо передать модуль в котором находится обертка
```go
log := logrus.New(logrus.WithModuleIgnore("github.com/YandexClassifieds/module-to-ignore"))
```