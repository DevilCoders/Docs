### Обертка для использования zap-логгера и простого протоколирования в stderr.

Понимает параметры и переменные окружения:

```
$ ./example -help
Usage of ./example:
  -debug
      Turn on debug logging [Environment variable: DEBUG]
  -log-level string
      Logging level: DEBUG, INFO, WARN, ERROR, DPANIC, PANIC, FATAL [Environment variable: LOG_LEVEL] (default "INFO")
  -log-style string
      Force log style to be: console, json or auto. Default is auto. [Environment variable: LOG_STYLE] (default "auto")
```

Пример использования:

```(go)
package main

import (
  "flag"

  "a.yandex-team.ru/market/sre/library/golang/logger"
)

func main() {
  flag.Parse()
  logger.ProceedFlags()

  // Let's log start and stop
  logger.Log.Debugw("Parameters parsing finished. Main program starting")
  defer func() {
    logger.Log.Debugw("Program finished")
    _ = logger.Log.Sync()
  }()
}
```
