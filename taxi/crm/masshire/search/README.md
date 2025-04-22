# Модуль поиска для масснайма

## Форматирование кода

Для форматирования кода используется [`ktfmt`][ktfmt] с code style пресетом Kotlinlang.
Можно установить в виде плагина в IDEA и включить автоматическое форматирование при сохранении файла.

[ktfmt]: https://github.com/facebookincubator/ktfmt

## Генерация проекта для IDEA

Для генерации проекта используется следующий набор ключей:

```
ya ide idea --stat --yt-store --group-modules tree --omit-test-data --iml-in-project-root --local --separate-tests-modules --auto-exclude-symlinks -r PATH_TO_IDEA_PROJECT
```

## Логирование при локальном запуске

По умолчанию при запуске будет использоваться `logback.xml` для прода, который будет пытаться логировать в Unified Agent и на диск.
При локальном запуске это обычно не нужно, поэтому лучше использовать `logback-test.xml`, который используется в тестах и логирует только в консоль.
Чтобы использовать его при локальном запуске нужно передать в качестве параметра виртуальной машины:

`-Dlogback.configurationFile=/PATH-TO-LOGBACK-TEST/logback-test.xml`

В IDEA это можно сделать через "Edit Configurations... -> VM options".
При запуске в консоли нужно передавать параметры виртуальной машины перед именем запускаемого класса:

`./run.sh -Dlogback.configurationFile=... ru.yandex.taxi.crm.masshire.search.ServerKt`

## Секреты при локальном запуске

Бо́льшую часть секретов можно передавать через переменные окружения.
Секреты и имена переменных окружения, можно посмотреть в `Secrets.kt`.
В IDEA переменные окружения задаются через "Edit Configurations... -> Environment Variables"
