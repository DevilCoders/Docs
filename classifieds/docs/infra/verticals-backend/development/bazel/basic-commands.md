# Bazel

[Официальная документация](https://bazel.build/)

## Основные команды

### Сборка таргета

`bazel build //services/comeback/storage:storage` – сборка отдельного таргета

`bazel build //services/comeback/...` – сборка всех таргетов в директории

Сборка инкрементальная, результаты всех промежуточных таргетов кешируются локально.

### Запуск тестов

`bazel test //services/comeback/storage:filters_tests --test_output=streamed`

Параметр `--test_output=streamed` нужен для того, чтобы логи выводились на консоль в процессе работы, а не в самом конце.

Результаты тестов также кешируются. Если хочется запустить все тесты без кеша, укажите `--cache_test_results=no`.

Для запуска конкретного теста нужно указывать:
- для `zio_test`: 
    `--test_filter=auto.c2b.lotus.storage.test.LotsDaoSpec` – запуск всех тестов в классе. 
    `--test_filter=auto.c2b.lotus.storage.test.LotsDaoSpec##update` – запуск всех suite/test в классе, в лейблах которых встречается подстрока `update`.

- для `scala_test`: `--test_filter=ru.yandex.vertis.broker.distribute.strategy.ExtraDataLocalDistributionStrategySpec` - полное имя Spec-класса. Также поддерживается wildcard (`--test_filter=ru.yandex.vertis.broker.distribute*`).

### Запуск кода

`bazel run //general/gost/api:service` – просто запуск (для `scala_binary` и `shiva_service` таргетов)

`bazel run //general/gost/api:service -- --debug` – дебаг на 5005 порту

`bazel run //general/gost/api:service -- --debug=1337` – дебаг на 1337 порту

### Когда все пошло не так

`bazel clean --expunge` – чистит кеши базеля

## Buildbuddy

Все bazel-команды шлют данные в [buildbuddy](https://www.buildbuddy.io/) (ссылку на свой запуск можно найти в логах сборки). 
Buildbuddy дает более наглядное представление о том, что происходило во время вызова.
При возникновении проблем лучше давать ссылку именно на него, а не делиться выводом в консоли.
