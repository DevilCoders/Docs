# Probes

В библиотеке реализован общий подход к проверкам живости приложения
и политике остановки

## Usage
```
state := probes.NewState(logger)
state.Ready() // true
state.Stop(time.Second)
```
## Хуки
Также можно передать хуки реагирующие на события
```
state := probes.NewState(
    logger,
    probes.OnReady(func() bool {<check something>}),
    probes.OnStopBefore(func() {<notify your app>}),
)
```
### OnReady
Вызывается при проверке readiness.
Проверка считается успешной если все хуки OnReady отвечают успехом
Вызываются лениво.

### OnStopBefore
Вызываются перед остановкой

### OnStopAfter
Вызываются после остановки

## Bindings
Для подключения библиотеки к серверу приложения,
реализованы биндинги для применяемых серверов (chi, echo ...).
```
probes.ChiBind(&probes.DefaultConfig, chi.NewRouter(), state)
```

Каждый биндинг регистрирует в сервере:
- проверку живости бекенда по адресу `probes.Config.ReadinessRoute` (по умолчанию `/ping`)
- api остановки по адресу `probes.Config.ShutdownRoute` (по умолчанию `/shutdown`)
