# AbstractLogger
класс реализующий основные механизмы логирования в duffman-е.

[[src](../lib/abstract-logger.js)]

Он отвечает как за продакшн логирование в `syslog`, так и за отладочное логирование в [debug].

Логирование осуществляется с помощью набора методов. Каждому методу соответствует уровень `versbosity` при котором
он будет выводить данные (в консоль и syslog) и [`severity`][syslog-severity].

| verb | severity  | метод              |
| ---: | --------- | ------------------ |
|   -1 | `crit`    | `crit`             |
|    1 | `err`     | `error` (`err`)    |
|    2 | `warning` | `warn` (`warning`) |
|    3 | `notice`  | `log` (`notice`)   |
|    3 | `info`    | `info`             |
|    4 | `debug`   | `debug`            |

По умолчанию уровень verbosity максимальный, его можно понизить с помощью [настройки](./cli.md#-m---mute) `mute`.

В режиме разработки есть дополнительный способ фильтрации лога — переменная окружения `DEBUG`.
Так например чтобы увидеть только информацию об http запросах, нужно запустить сервер следующим способом:
```
DEBUG="core:http:*"
```

  [debug]: https://github.com/visionmedia/debug
  [syslog-severity]: https://en.wikipedia.org/wiki/Syslog#Severity_level
