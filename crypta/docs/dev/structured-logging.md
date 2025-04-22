Java
====

Для использования JSON логгирования в `logback.xml` должен использоваться:
```
<jsonGeneratorDecorator 
  class="ru.yandex.crypta.common.ws.logging.QloudAwareJsonGeneratorDecorator"
/>
```

Python
======

Для использования JSON логгирования модуль `logging` должен быть настроен с использованием:

```
crypta.lib.python.logging.json_logging.Formatter
```
